# Primes
A tool for working with prime numbers.

![alt text](https://github.com/RoyalXXX/primes/blob/main/screenshot.png)

When calculating prime numbers, highly efficient algorithms are usually employed, often based on sieves (such as the sieve of Eratosthenes). Yet even these algorithms struggle with very large primes, as memory usage grows rapidly when building a sieve. A partial remedy is the use of segmented sieve algorithms, though they too lose efficiency when constructing extremely large sieves.

This program serves as a demonstration that prime numbers need not always be computed at runtime – they can instead be precomputed and embedded directly into the program. The idea is that primes can be stored efficiently in binary form, allocating just **4 bytes** per number.

> [!CAUTION]
> By contrast, attempting to save space by allocating fewer bytes for smaller primes (e.g., 1 byte for the smallest primes, then 2, 3, and finally 4 bytes) offers only a negligible reduction in the overall database size.

For example, **Primes** comes with a built-in database containing `203 280 221` prime numbers. The final entry, `4 294 967 291`, is the largest prime representable in a **32-bit unsigned integer**.

Storing such a dataset uncompressed would require:
`203 280 221 × 4 bytes = 813 120 884 bytes` (**~775.45 MB**).
However, thanks to compression (**LZMA2:25**), the **Primes** program itself is only **172 MB** in size. At runtime, the data is decompressed directly into memory without creating temporary files.

To run, the program requires **RAM** equal to the size of the prime database (**~775.45 MB**) plus a small overhead – totalling up to **778 MB**. Decompression needs an additional **32 MB** (because **LZMA2:25** requires **2²⁵** bytes for decompression.), meaning a peak memory requirement of about **810 MB** during startup. Once running, it uses **778 MB**.

No known algorithm can, with this amount of memory, compute the `203 280 221st` prime nearly as quickly.

> [!TIP]
> The program’s size could be reduced further by using **RAR5** instead of **LZMA2**, as **RAR5** compresses the prime database around **16%** more efficiently. However, the **UnRAR** library does not allow the data to be decompressed directly into memory without creating temporary files on disk.


