# Examlet 6
## Example problem: Averate memory access time
### Consider a system with a main memory access time of 100 ns is supported by an L1 cache having a 10 ns access time and a hit rate of 90% and an L2 cache having a 20 ns access time and a hit rate of 80%.
### What is the average memory access time for a **look aside cache**?
- AMAT = 10(0.9) + 0.1*(20*0.8 + 100*0.2) = 12.6 ns
What is the average memory access time for a **look through cache**?
- AMAT = 10 + 0.1(20 + 0.2*100) = 14 ns

## Example problem: finding address part sizes
### A system has a main memory of 65,536 bytes and is split into blocks of 512 bytes.

How many bits wide is the address? 
- $log_2 (main Memory Size)$ 
- $65,536 = 2^{16}$
- $log_2 (2^{16}) = 16$ 

How many bits wide is the offset field?
- $log_2 (blockSize)$
- $512 = 2^9$
- $log_2 (2^9) = 9$

How many bits describe the block? 
- $Width - offset$
- $16 - 9 = 7$

### The system has a cache that is 8192 bytes.
How many lines does the cache have?
- bytes in cache $\div$ block size
- $8192 = 2^{13}$
- $512 = 2^9$
- $\frac{2^{13}}{2^9} = 2^4 = 16 $

If the cache is fully associative, into how many possible lines can a block be placed?
- any block can go to any line
- 16 lines

How many bits are in the tag field for a fully associative cache?
- same as the block number
- 7

If the cache is direct mapped, into how many possible lines can a block be placed?
- Each block maps to one line in the cache.
- 1

How many bits are in the line field and the tag field?
- split the block number into tag and line
- number of bits in the line field is $log_2(numLines)$
  - $log_2(numLines)$
  - numLines = 16 = $2^4$
  - $log_2(2^4) = 4$
- tag will have what is left ( I don't grock this)
  - 16 - 9 - 4 = 3

If the cache is 2-way set associative, into how many possible lines can a block be placed?
- 2

---
Fully associattive, how many places can a byte be in a cache?
- bytes per cache $\div$ bytes per line

---
## Example: Direct Maped
### A system has a main memory with $2^{32}$ bytes has a block size of 16 bytes and a cache size of $2^{12}$ bytes.

If address 0x123123FF is requested, and the cache is **direct mapped**.
- What is the offset?
  - $log_2 (blockSize)$
  - $16 = 2^4$
  - $log_2 (2^4) = 4$
  - 4 bits, so first hex char
  - 0x123123F**F**
- what is the line?
  - $log_2(numberOfLines)$
  - number of lines = Line size is cache size $\div$ block size
  - $\frac{2^{12}}{2^4} = 2^8$
  - $log_2(2^8) = 8 bits$
  - 8 bits, so next two hex chars
  - 0x12312**3F**F
- What is the tag?
  - remaining bits
  - 0x**12312**3FF

Where will the system look in the cache for the tag?  How may possible places could this byte be if it is in the cache?
- There is only one possible place where this byte could be in a direct-mapped cache because each block of main memory is mapped to exactly one line in the cache. In a direct-mapped cache, the cache lines are divided into three fields: tag, line, and offset. The line field indicates the unique cache line where a specific block of main memory can be stored.

## Example: Set Associative
### A system has a main memory with $2^{32}$ bytes has a block size of 16 bytes and a cache size of $2^{12}$ bytes. If address 0x123123FF is requested, and the cache is 4-way set associative:

#### What is the offset?
- $log_2 (blockSize)$
- $log_2 (2^4) = 4 bits$

#### Number of Sets?
- bytes in cache $\div$ byes in line * lines in set
- $2^{12} \div (2^4 * 4) = 2^6 sets/cache$

#### Set field length?
- $log_2 (sets/cache)$
- $log_2 (2^6) = 6$ bits

#### Tag field length?
- memory size - set field size - offset size
- 32 - 6 - 4 = 22 bits

What is the tag?
- 0x123123FF = 0001 0010 0011 0001 0010 0011 1111 1111
- **0001 0010 0011 0001 0010 00**11 1111 1111

What is the line? (she calls it set in slide)
- 0001 0010 0011 0001 0010 00**11 1111** 1111

What is the offset?
- 0001 0010 0011 0001 0010 0011 1111 **1111**


Where will the system look in the cache for the tag?
- Will look at set 111111, which has four lines. Wach line's tag is checked for a match.

How may possible places could this byte be if it is in the cache? 
- 4 lines in set, so 4 possible places

