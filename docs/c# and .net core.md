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
