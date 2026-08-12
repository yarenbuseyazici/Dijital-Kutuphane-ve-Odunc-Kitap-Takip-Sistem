<img width="903" height="401" alt="Yönetici Girişi" src="https://github.com/user-attachments/assets/b382c014-f2c1-4a24-bdb4-f41cceaddc94" />
<img width="889" height="555" alt="Yeni Kitap Ekle" src="https://github.com/user-attachments/assets/25d0482c-7e4a-46ca-a459-71f9b05e1c0b" />
<img width="896" height="489" alt="Kullanıcı Yönetim Paneli" src="https://github.com/user-attachments/assets/125ed681-5fc5-40b0-a2be-5db407f3cdd2" />
<img width="891" height="909" alt="Kullanıcı Paneli" src="https://github.com/user-attachments/assets/791e331b-aa27-4498-9ebd-6dc38e31d7b1" />
<img width="904" height="443" alt="Kullanıcı Girişi" src="https://github.com/user-attachments/assets/d5c9f92a-d7f1-442f-9c2d-d03ec42ff5c8" />
<img width="892" height="632" alt="Kitap Yönetim Paneli" src="https://github.com/user-attachments/assets/4e578bd1-1a66-46cb-a5fa-da1b360fd1ea" />
<img width="1059" height="477" alt="Kayıt Ol" src="https://github.com/user-attachments/assets/05a53968-bdf3-4e30-a68e-31c443404973" />
<img width="1962" height="1276" alt="Anasayfa" src="https://github.com/user-attachments/assets/ad9a511a-451a-45c4-9981-062a94eb6cf4" />
 📚 Dijital Kütüphane & Ödünç Kitap Takip Sistemi
ASP.NET Core MVC ve Entity Framework Core mimarisi kullanılarak geliştirilmiş; kitap envanteri yönetimi, rol tabanlı kullanıcı yetkilendirmesi ve kütüphane ödünç/iade süreçlerini uçtan uca yöneten web uygulamasıdır.

 ⚡ Adım Adım Sistem Çalışma Algoritması (İş Akışı)
Proje, kullanıcı ve yönetici olmak üzere iki ana rol üzerinden aşağıdaki algoritma ve iş kurallarıyla çalışır:




   ├──► 1. Oturum ve Kayıt Algoritması
   │      ├── Kullanıcı Kayıt Olur ──► Varsayılan olarak "User" rolü atanır.
   │      └── Giriş İşlemi ─────────► Kullanıcı Girişi / Yönetici Girişi seçilir.
   │                                   └─► Çerez (Cookie Authentication) oluşturulur.
   │
   ├──► 2. Kitap İnceleme ve Filtreleme Algoritması (Anasayfa)
   │      ├── DB'deki 'IsPopular = true' olan kitaplar Popüler Listesine çekilir.
   │      └── Seçilen Kategori ID'ye göre kitaplar LINQ (.Where) ile filtrelenir.
   │
   ├──► 3. Ödünç Alma Algoritması (User)
   │      ├── Kullanıcının aktif ödünç aldığı kitap sayısı sayılır (Count).
   │      ├── EĞER (Count >= 4) ──► İŞLEM ENGELLE (Maksimum 4 kitap limiti uyarısı).
   │      └── EĞER (Count < 4)  ──► Book.IsBorrowed = true, Book.UserId = ActiveUserId 
   │                               └─► DB Güncellenir.
   │
   ├──► 4. İade Etme Algoritması (User)
   │      └── Kitap İade Et ──────► Book.IsBorrowed = false, Book.UserId = null 
   │                               └─► DB Güncellenir.
   │
   └──► 5. Yönetim (Admin) Algoritması
          ├── Kitap İşlemleri ────► CRUD + Sunucuya Kapak Resmi Yükleme (/uploads)
          └── Kullanıcı İşlemleri ─► Üye Ekleme/Silme/Düzenleme + Rol Atama (Admin/User
