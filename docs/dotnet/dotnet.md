# C#
## 8.0
- No need to indent using statements. New syntax would be "using var reader = file.OpenText();"  
- Switch expressions (not switch statements) with pattern matching  
- async streams   
https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-8  
## 7+
### Span<T> and Memory<T>
- Span<T> is a value type   
  public readonly ref struct Span<T>  
{  
  private readonly ref T _pointer;  
  private readonly int _length;  
  ...  
}  
  ref T cannot be actually created, but Span<T> uses special internal type in the runtime that’s treated as a just-in-time (JIT) intrinsic, with the JIT generating for it the equivalent of a ref T field. Types that contain such refs directly or indirectly are called ref-like types.So, indexing into a span doesn’t require computation to determine the beginning from a pointer and its starting offset, as the ref field itself already encapsulates both. 
Span<T> instances can only live on the stack, not on the heap otherwise there is a chance of tearing (overwriting by multiple threads at same time. One more reason, is to limit the number of intrinsic pointers that can be created by span. Why? Coz intrinisic pointers are expensive and stack has implicit limit on the number of intrinsic pointers.   
This means we can’t box spans. Also, it means we can’t have Span<T> fields in classes, or even in non-ref-like structs.  

Span<T> can’t be stored to the heap and thus can’t be persisted across asynchronous operations, what’s the answer? Memory<T>.  
Memory<T> looks very much like an ArraySegment<T>:  
public readonly struct Memory<T>  
{  
  private readonly object _object;  
  private readonly int _index;  
  private readonly int _length;  
  ...  
}  
You can create a Memory<T> from an array and slice it just as you would a span, but it’s a (non-ref-like) struct and can live on the heap. Then, when you want to do synchronous processing, you can get a Span<T> from it. 
For details, https://msdn.microsoft.com/en-us/magazine/mt814808.aspx 

# .Net Core 
## 3.0
- .net standard 2.1 introduced
- new Ranges and Index syntax  
- Supporting TLS 1.3 and OpenSSL 1.1.1  
- import and export of asymmetric public and private keys from standard formats, without needing to use an X.509 certificate  
- dotnet build now copies dependencies (dotnet publish may not be needed always)  
- Applications now have executables by default.  
  An app can be either using 'myconsole.exe' or 'dotnet myconsole.dll'  
- fast in-box JSON Writer & JSON Document  
- docker images will be published to Microsoft Container Registry (MCR) (mcr.microsoft.com)
- default implementations are available for interfaces
