# Module 5
## Muhammad Albyarto Ghazali

## JMeter Report and Test Results

### Endpoint /all-student
Before Optimization:
![image](https://github.com/user-attachments/assets/3f8f6797-5132-4c19-bf41-06d474814c5f)
![image](https://github.com/user-attachments/assets/af70346d-4e28-4039-af8f-084a3775b43d)

After Optimization:
![image](https://github.com/user-attachments/assets/0b266bb7-f243-4e8d-bc01-cff65145ef88)
![image](https://github.com/user-attachments/assets/2b68e0e4-1549-40bc-9235-2330650cd2b3)

### Endpoint /all-student-name
Before Optimization:
![image](https://github.com/user-attachments/assets/2b4aa609-1c75-48ce-ba35-9ae617d615b6)
![image](https://github.com/user-attachments/assets/f962cc71-adac-4d53-b979-94bdcc4b2e00)

After Optimization:
![image](https://github.com/user-attachments/assets/a92d7080-6b41-4ab5-95a8-2a88095df8fb)
![image](https://github.com/user-attachments/assets/15c81c55-5fde-46c4-b41f-8505b288f39e)


### Endpoint /highest-gpa
Before Optimization:
![image](https://github.com/user-attachments/assets/75705783-711a-4408-8dbd-eb04a319f8ef)
![image](https://github.com/user-attachments/assets/a6331e90-5fbc-4907-807b-4d8ca879d86c)

After Optimization:
![image](https://github.com/user-attachments/assets/1fbb7d5c-826b-4d61-8192-d3059eb0c939)
![image](https://github.com/user-attachments/assets/7c35d85a-8474-4a13-8946-a4a8c1482d89)

### Kesimpulan
Refaktorisasi telah memberikan peningkatan performa yang cukup signifkan. Aplikasi sekarang dapat menangani lebih dari dua kali throughput sebelumnya dengan waktu respons kurang dari setengahnya.
Optimasi ini sangat berharga seiring pertumbuhan database mahasiswa, karena implementasi asli memiliki karakteristik performa yang akan menurun secara non-linear dengan peningkatan ukuran data.

## Refleksi

> What is the difference between the approach of performance testing with JMeter and profiling with IntelliJ Profiler in the context of optimizing application performance?

Perbedaan utama antara pengujian performa menggunakan JMeter dan profiling dengan IntelliJ Profiler terletak pada fokus dan tujuan masing-masing alat. JMeter digunakan untuk melakukan uji beban pada aplikasi, mengevaluasi kinerjanya di berbagai tingkat penggunaan, dan mensimulasikan skenario pengguna secara bersamaan. Sementara itu, IntelliJ Profiler berfungsi sebagai alat analisis kinerja kode yang membantu mendeteksi penggunaan CPU, konsumsi memori, serta aktivitas thread untuk mengidentifikasi potensi bottleneck dalam aplikasi.

> How does the profiling process help you in identifying and understanding the weak points in your application?

Profiling memungkinkan saya untuk mengidentifikasi metode yang berjalan lambat dan membebani program. Dengan mengukur waktu eksekusi setiap metode atau fungsi dalam aplikasi, profiler dapat menunjukkan bagian kode yang paling lambat sehingga dapat dioptimalkan. Selain itu, profiler juga membantu dalam mendeteksi penggunaan memori dengan melacak alokasi dan konsumsi memori dalam aplikasi, sehingga dapat mencegah terjadinya kebocoran memori.

> Do you think IntelliJ Profiler is effective in assisting you to analyze and identify bottlenecks in your application code?

Ya, IntelliJ Profiler sangat efektif dalam mengidentifikasi bottleneck dalam aplikasi. Alat ini dapat menemukan metode dengan waktu eksekusi terlama, mendeteksi kebocoran memori, menganalisis performa thread, serta mengoptimalkan penggunaan CPU agar aplikasi berjalan lebih responsif.

> What are the main challenges you face when conducting performance testing and profiling, and how do you overcome these challenges?

Karena ini pertama kali saya melakukan performance testing dan profiling di IntelliJ, saya masih belum terbiasa dengan berbagai informasi teknis yang ditampilkan oleh profiler, seperti stack trace, alokasi memori, serta grafik CPU/Memori. Banyaknya data tersebut membuat saya kesulitan menentukan bagian mana yang menjadi beban bagi program. Untuk mengatasinya, saya berusaha lebih sering menggunakan profiler di IntelliJ dan memanfaatkan fitur flame graph yang dirancang agar mempermudah pengguna dalam menemukan kelemahan dalam kode.

> What are the main benefits you gain from using IntelliJ Profiler for profiling your application code?

Dengan IntelliJ Profiler, saya dapat dengan cepat mengidentifikasi bottleneck dan inefisiensi dalam kode berdasarkan waktu eksekusi setiap metode atau fungsi. Selain itu, saya juga bisa memantau alokasi memori secara real-time serta mengawasi aktivitas thread. Profiling di IntelliJ terasa intuitif dan mudah digunakan karena sudah terintegrasi langsung dengan IntelliJ IDEA.

> How do you handle situations where the results from profiling with IntelliJ Profiler are not entirely consistent with findings from performance testing using JMeter?

Jika saya menemukan perbedaan dalam hasil pengujian, langkah pertama yang saya lakukan adalah memastikan bahwa pengujian di IntelliJ Profiler dilakukan dalam kondisi yang sama seperti di JMeter. Misalnya, saya akan memeriksa jumlah thread untuk memastikan aplikasi diuji dengan beban yang setara. Perbedaan jumlah thread atau jumlah pengguna pada masing-masing profiler dapat menyebabkan hasil yang tidak konsisten. Selain itu, saya juga akan mengecek kembali rute ke URL localhost di JMeter agar sesuai dan akurat terhadap skenario pengujian yang ingin diuji.

> What strategies do you implement in optimizing application code after analyzing results from performance testing and profiling? How do you ensure the changes you make do not affect the application's functionality?

Karena metode yang paling banyak memakan waktu dalam program adalah `getAllStudentWithCourses()` di `StudentService.java`, saya mengoptimalkannya dengan mengganti seluruh isi metodenya menjadi `return studentCourseRepository.findAll()`, yang memiliki fungsi serupa tanpa memerlukan loop berlebih. Setelah itu, saya menganalisis metode lain yang juga memiliki waktu eksekusi tinggi, seperti `findStudentWithHighestGPA()` dan `joinStudentNames()`. Setelah optimasi dilakukan, saya menjalankan kembali profiler dan melihat bahwa waktu eksekusi metode-metode tersebut telah berkurang.  

Untuk memastikan tidak ada perubahan dalam fungsionalitas, saya menjalankan metode-metode tersebut dan membandingkan hasilnya dengan versi sebelumnya. Namun, praktik terbaiknya adalah melakukan pengujian sebelum dan sesudah optimasi untuk memastikan bahwa tidak ada perubahan yang memengaruhi fungsionalitas aplikasi.
