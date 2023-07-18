# File-scoped Namespaces

File-scoped namespaces allow you to declare them for the whole file and without using a block.
This feature is available on C# 10 and above.

## Example

### Block-scoped Namespaces Example

```cs
namespace ECommerceApplication
{
    class OrderProcessor
    {

    }
}
```

Traditional of block-scoped namespaces required one level of identation.

### File-scoped Namespaces Example

```cs
namespace ECommerceApplication;

class OrderProcessor
{

}
```

By using file-scoped namespaces, one level of indentation is reduced which improve the readability.