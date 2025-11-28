# 🌲 Karakter Tabanlı Hayatta Kalma Simülatörü

Bu proje, **Algoritma ve Programlama** dersi kapsamında C programlama dili kullanılarak geliştirilmiş metin tabanlı bir hayatta kalma oyunudur.

## 🎯 Projenin Amacı
Oyuncu; sağlık, enerji ve yemek kaynaklarını yöneterek hayatta kalmaya çalışır. Verilen komutlarla avlanabilir, sığınak arayabilir veya dinlenebilir. Amaç, sağlık değerini 0'ın üzerinde tutarak mümkün olduğunca yüksek puan toplamaktır.

## 🎮 Oynanış ve Komutlar

Simülasyon aşağıdaki tuş komutları ile yönetilir:

* **A (Avlan):** Enerji harcayarak yemek arar. Yaralanma riski vardır.
* **S (Sığınak Ara):** Enerji harcayarak sığınak arar. Sığınak varsa dinlenir.
* **R (Dinlen):** Yemek yiyerek sağlık ve enerjiyi yeniler.
* **E (Envanter):** Anlık sağlık, enerji, yemek ve puan durumunu gösterir.
* **F (Tehlike Simülasyonu):** Bölgedeki tehlikeli olayları (fırtına vb.) simüle eder.
* **P (Şifreli İlerleme):** Rastgele çıkan şifreyi çözerek bir engeli aşmaya çalışır.
* **X (Çıkış):** Simülasyonu sonlandırır.

## 🛠 Teknik Detaylar ve Kullanılan C Yapıları

Bu proje, C dilinin temel yapı taşlarını kullanarak oluşturulmuştur:

### 1. Döngüler (Loops)
* **DO-WHILE Döngüsü:** Oyunun ana döngüsünü oluşturur. Oyuncu 'X' tuşuna basana kadar veya karakter ölene kadar oyunun devam etmesini sağlar.
* **FOR Döngüsü:** `F` komutunda kullanılır. Belirli bir süre (tur sayısı) boyunca devam eden bir tehlike dalgasını simüle eder.
* **İç İçe DO-WHILE:** `P` (Şifre) komutunda, oyuncu doğru şifreyi girene kadar döngünün devam etmesi için kullanılmıştır.

### 2. Karar Yapıları (Decision Making)
* **SWITCH-CASE:** Kullanıcının girdiği komutları (A, S, R...) hızlı ve düzenli bir şekilde yönetmek için kullanılmıştır.
* **IF-ELSE:** Oyun içindeki koşulları kontrol eder. (Örn: `if (enerji >= 15)` avlanmak için yeterli enerji var mı?)

### 3. Operatörler
* **Aritmetik Operatörler:** Kaynak tüketimi ve kazanımı (`enerji -= 15`, `saglik += 10`) için kullanılmıştır.
* **Mantıksal Operatörler (&&, ||):** `A` komutunda yaralanma riskini hesaplarken veya `S` komutunda sığınak kurma şartlarını (yemek var VE sığınak yok) kontrol ederken kullanılmıştır.

### 4. Rastgelelik (Randomness)
* `rand()` ve `srand(time(NULL))` fonksiyonları ile oyunun her açılışta farklı senaryolar (farklı yemek sayısı, şifreler, riskler) üretmesi sağlanmıştır.

## 🚀 Kurulum ve Çalıştırma

1.  Bu projeyi bilgisayarınıza indirin veya kopyalayın.
2.  Bir C derleyicisi (Dev-C++, GCC, Code::Blocks) ile `main.c` dosyasını açın.
3.  Kodu derleyin ve çalıştırın (Compile & Run).

---
*Geliştirici: Mehmet Berke Ünlütürk*
*Yardım alınan yapay zeka: Gemini*
*Ders: Algoritma ve Programlama*
