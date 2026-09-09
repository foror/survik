At the beginning of each text file (or variable of String type), a control byte is stored:

**0-3** bits indicate the Windows-CP125x encoding (9 variants)

**4-6** bits indicate the string parsing algorithm:

000 - each character is encoded using one byte 
```
if the first bit of the character is 0, then its remaining 7 bits are encoded as US-ASCII
if the first bit of the character is 1, then it is encoded as Windows-CP125x (depending on the first control byte)
```

001 - each character occupies exactly 2 bytes

010 - each character occupies exactly 4 bytes

011 - mixed character size (effectively, this is UTF-8)
```
if the first bit of the character is 0, then this is a 1-byte character and is encoded as US-ASCII
if the first bit of the character is 1, then this is a character occupying 2 bytes (or more) and is encoded according to the UTF-8 rules
```

100 - mixed character size, but if the first bit is 0, then this character occupies 1 byte and is encoded as Windows-CP125x (depending on the first control byte). Other characters (include US-ASCII) occupying 2 bytes (or more)

The last bit is always set to 1. If it is 0, then the string is read as a US-ASCII sequence starting from the first byte.
