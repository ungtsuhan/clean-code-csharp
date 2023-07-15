# Early Return Principle

Avoiding deep nesting.
Check for certain condition as early as possible and return or throw exception immediately if those conditions are not met. This will improve readability and reduce complexity.

## Example

### Bad Example

```cs
public class OrderProcessor
{
    public void Process(Order? order)
    {
        if (order != null)
        {
            if (order.IsVerified)
            {
                if (order.Items.Any())
                {
                    if (order.Items.Count > ProcessableNumberOfLineItems)
                    {
                        throw new OrderHasTooManyLineItemsException(order.Id);
                    }
                    
                    if (order.Status != OrderStatus.ReadyToProcess)
                    {
                        throw new OrderNotReadyForProcessingException(order.Id);
                    }

                    order.IsProcessed = true;
                }
            }
        }
    }
}
```

Many level of deep nesting make it hard to read.

### Good Example

```cs
public class OrderProcessor
{
    public void Process(Order? order)
    {
        if (order is null || !order.IsVerified || !order.Items.Any())
            return;
        
        if (order.Items.Count > ProcessableNumberOfLineItems)
            throw new OrderHasTooManyLineItemsException(order.Id);

        if (order.Status != OrderStatus.ReadyToProcess)
            throw new OrderNotReadyForProcessingException(order.Id);

        order.IsProcessed = true;
    }
}
```

Early return ane merge multiple if statement eliminate unnecessary nesting and flatten the control flow lead to more readable code.