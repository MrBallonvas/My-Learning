## data types
`int` - 4 bytes
`short` - 2 bytes
`float` - 4 bytes
`double` - 8 bytes
`char` - 1 byte (store 1 letter)
`long` - 8 bytes

## Specific facts
### Volatile
tells to compiler don't optimize some var
## Features
### How to swap values without temporary variable
1. Sum:
```C
a = a + b;
b = a - b;
a = a - b;

```
2. XOR
```C
a = a ^ b;
b = a ^ b;
a = a ^ b;
```