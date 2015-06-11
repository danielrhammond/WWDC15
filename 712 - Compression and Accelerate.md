Low Energy, High Performance: Compression and Accelerate (712)
Eric Bainville, Steve Canon, Luke Chang

# Overview
## Accelerate
vImage, vDSP, vForce, BLAS, LAPACK, Linear Algebra
Sparse BLAS (new)
## Other Libraries
libm
simd - vector types that map directly to cpu vector units
compression (new)
# Compression
Lossless data compression
Unified API
Selection of algorithms with high efficiency and performance
## Algorithms
All compared against `zlib`
`lzma` better compression, ratio lower speed
`lz4` better speed, lower compression ratio
`lbfse` (new) slightly better speed and better compression ratio to `zlib`
### LZFSE
Replaces hoffman in zlib with “Finate State Entropy” better performance characteristics on modern micro-architectures. Same compression ratio but significant performance and energy usage wins
#### Buffer API
`compression_algorithm algorithm = COMPRESSION_LZFSE;
size_t dst_size = compression_encode_buffer(destination, destination_capacity, source, source_size, NULL, algorithm)`
#### Stream API
Similar to buffer API, more state
# simd
- 2,3,4 dimensional vectors and matrices, closely mirrors Metal shading language
- (new) added swift support
```
let x = float3(1,2,3)
var y = float3(1,3,5)
y += 2*x
```
## Vector types
Vectors of floats, doubles, and 32-bit integers
Lengths 2,3, and 4
### Arithmetic
```
func reflect(x: float3, n: float3) -> float3 {
  return x - 2*dot(x,n)*n;
}
```
### Built in Geometry functions for vectors
dot,project,length,norm_one,norm_inf,normalize,distance,cross,reflect,refract
## Matric types
floatNxM and doubleNxM
N is number of columns
M is number of rows
N and M are both 2, 3 or 4
### Arithmetic
```
var m = float4x4(2) // 2s on diagonal
m[3] = [1,2,3,1]
let x = float4x4(3) * m
```
### Conversion
No conversions required between objective c for vectors, do need to initialize swift matrices from objective c matrix
# LAPACK, BLAS, and LinearAlgebra
Industry standard interfaces for linear algebra, descended from FORTRAN
## LinearAlgebra
Introduced in Yosemite and iOS 8, greatly simplified interfaces for a few commonly used operations
## LINPACK Benchmark
How fast can you solve a system of equations, use accelerate it crushes everything
# SparseBlas
New in iOS 9, single and double precision for linear algebra on sparse matrices. Available operations:
- Products
- Triangular solves
- Norms
- Trace
- Permutes
- Insert/Extract
## Storage
Only store non-zero values with indices/number of non-zero values. 
## Sparse Matrix Data Type
Opaque pointer (Create, operate, destroy)
Memory is managed for you
Storage format is decided for you, and conversions handled automatically
### Delayed commit
Data insertion is batched, forced by commit function or automatically when you perform matrix operations

