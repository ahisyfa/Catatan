# Java

## Daftar Isi
1. Exception Handling


## Exception Handling
### Kapan Menggunakan Exception Handling?
Jawab : 
- Exception handling didesain untuk menangani synchronous errors yang terjadi saat 
suatu statement dieksekusi. 
- Exception handling TIDAK didesain untuk menangani masalah yang
 berkaitan dengan asynchronous events (e.g., disk I/O completions, network message arrivals, mouse clicks and keystrokes).
 
 
### Hirarki Exception Java
- Semua exception yang ada di java merupakan turunan langsung atau tidak langsung dari class `Exception`.
- Superclass dari `Exception` adalah kelas `Throwable`. Hanya objek `Throwable` (dan turunannya) yang dapat digunakan dalam
mekanisme Exception handling. Kelas `Throwable` memiliki 2 kelas turunan, yaitu `Exception` dan `Error`. 
- Kelas `Error` dan turunannya menggambarkan kondisi abnormal yang terjadi pada JVM.
- Kebanyakan `Error` terjadi sangat jarang dan tidak bisa ditangani oleh aplikasi, sangat tidak mungkin untuk aplikasi recovery dari `Error`.

### Gambar Hirarki Exception
```
                                               Throwable
                                                  /\
                                                 /  \ 
                                       Exception      Error
                                          /\
                                         /  \
                         RuntimeException   (Checked Exception)
                      (Unchecked Exception)    
```

### Checked vs. Unchecked Exceptions
- Semua exception yang diturunkan kelas `RuntimeException` adalah Unchecked Exception. Terjadi karena cacat yang ada pada kode kita, contoh saat terjadi `ArrayIndexOutOfBoundsException`.
- Semua exception yang diturunkan kelas `Exception` (kecuali kelas `RuntimeException`) adalah Checked Exception.

