[README.md](https://github.com/user-attachments/files/28596325/README.md)
# 💰 Kişisel Finans ve Harcama Takip Sistemi

## Öğrenci Bilgileri

| Alan | Bilgi |
|------|-------|
| **Ad Soyad** | Mustafa Şükrü Egrıbaş |
| **Öğrenci No** | 24903003 |
| **Ders Kodu** | BGY210 – Python Programlama II |
| **Öğretim Üyesi** | Dr. Öğr. Üyesi Tohid YOUSEFİ |
| **Dönem** | Bahar 2026 |
| **GitHub Repo** | `https://github.com/<kullanici>/24903003-MustafaSukruEgribas-PythonProje` |

---

## 📌 Proje Amacı

Bu uygulama kullanıcıların **gelir ve giderlerini** takip etmesini,  
finansal analizler yapmasını ve verileri **CSV / Excel** formatında  
saklamasını sağlayan modüler, nesne tabanlı bir konsol uygulamasıdır.

---

## 📁 Proje Dosya Yapısı

```
MustafaSukruEgribas_24903003_BGY210/
│
├── main.py                 ← Uygulamanın giriş noktası; ana menü döngüsü
├── finans_modeli.py        ← OOP: Islem ve FinansYoneticisi sınıfları
├── islem_yonetimi.py       ← Gelir/gider ekleme, listeleme, silme
├── dosya_islemleri.py      ← CSV okuma/yazma + Excel dışa aktarma
├── analiz.py               ← Pandas & NumPy analizleri, aylık tablo
├── gorsellestirme.py       ← Matplotlib / Seaborn grafikleri
├── utils.py                ← Yardımcı fonksiyonlar, doğrulama, menü
│
├── finans_verileri.csv     ← Otomatik oluşturulan veri dosyası
├── finans_raporu.xlsx      ← Excel çıktısı (3 sayfa)
├── aylik_ozet.txt          ← Aylık tablo metin çıktısı
└── grafikler/              ← PNG grafik çıktıları
    ├── aylik_cizgi_grafik.png
    ├── gelir_gider_bar.png
    ├── pasta_grafik.png
    └── kategori_bar.png
```

---

## 🏗️ Modüller ve Görevleri

### `finans_modeli.py` – Nesne Tabanlı Model
İki sınıf içerir:

**`Islem`** – Tek bir finansal kaydı temsil eder:
- `id`, `tutar`, `tarih`, `aciklama`, `tip` (`gelir`/`gider`), `kategori`
- `to_dict()` → CSV ve DataFrame dönüşümü için sözlük üretir
- `__str__`, `__repr__` → Okunabilir çıktı
- `ay`, `yil` property'leri → Aylık gruplama için

**`FinansYoneticisi`** – Merkezi veri yöneticisi:
- `gelirler: list[Islem]` ve `giderler: list[Islem]` listelerini tutar
- `gelir_ekle()`, `gider_ekle()`, `islem_sil()`, `id_ile_bul()`
- `toplam_gelir()`, `toplam_gider()`, `bakiye()`

---

### `utils.py` – Yardımcı Fonksiyonlar

| Fonksiyon | Açıklama |
|-----------|----------|
| `yeni_id_olustur(liste)` | Listede en büyük ID'yi bulup +1 döndürür |
| `tum_listelerden_yeni_id(gelirler, giderler)` | Her iki listeden benzersiz ID üretir |
| `tarih_kontrol(tarih)` | YYYY-MM-DD formatı doğrulama |
| `sayi_kontrol(deger)` | Pozitif sayı doğrulama |
| `kategori_sec(tip)` | Numaralı menüden kategori seçimi |
| `kullanici_tarih_al()` | Geçerli tarih girişi; boşsa bugün |
| `kullanici_tutar_al()` | Geçerli pozitif tutar girişi |
| `menu_goster()` | Ana menüyü ekrana yazdırır |
| `baslik_yazdir(baslik)` | Bölüm başlığı çizgili çıktı |
| `onay_al()` | Evet/Hayır onayı |

---

### `islem_yonetimi.py` – İşlem Yönetimi

| Fonksiyon | Açıklama |
|-----------|----------|
| `gelir_ekle(yonetici)` | Kullanıcıdan bilgi alarak gelir kaydı oluşturur |
| `gider_ekle(yonetici)` | Kullanıcıdan bilgi alarak gider kaydı oluşturur |
| `islemleri_listele(yonetici)` | Tarih sıralamalı tüm işlemler + bakiye özeti |
| `islem_sil(yonetici)` | ID ile işlem bulup siler |

---

### `dosya_islemleri.py` – Dosya İşlemleri

| Fonksiyon | Açıklama |
|-----------|----------|
| `csv_kaydet(yonetici, dosya_adi)` | Tüm verileri UTF-8 CSV'ye yazar |
| `csv_oku(yonetici, dosya_adi)` | CSV'den veri okuyarak yöneticiye yükler |
| `csv_menu(yonetici)` | Kaydet/Yükle alt menüsü |
| `excel_aktar(yonetici, dosya_adi)` | 3 sayfalı xlsx dosyası oluşturur |
| `excel_menu(yonetici)` | Dosya adı alarak Excel aktarımı başlatır |

**Excel Sayfaları:**
1. **Tüm İşlemler** – Renkli ham veri tablosu (gelir: yeşil, gider: turuncu)
2. **Aylık Özet** – Ay bazında gelir/gider/net bakiye
3. **İstatistikler** – Ortalama, min, max, toplam özeti

---

### `analiz.py` – Veri Analizi

| Fonksiyon | Açıklama |
|-----------|----------|
| `verileri_dataframe_yap(yonetici)` | Islem listelerini Pandas DataFrame'e çevirir |
| `toplam_gelir_gider(df)` | Toplam gelir, gider, bakiye dict döndürür |
| `aylik_analiz(df)` | Aya göre gruplandırılmış özet DataFrame |
| `numpy_istatistik(df)` | NumPy ile ortalama, min, max, std, medyan |
| `kategori_analizi(df)` | Kategoriye göre toplam/adet/ortalama |
| `analiz_goster(yonetici)` | Tüm analizleri biçimli ekrana yazdırır |
| `aylik_tablo_guncelle(yonetici)` | Aylık tabloyu ekranda göster + txt'ye yaz |

---

### `gorsellestirme.py` – Grafikler

| Fonksiyon | Açıklama |
|-----------|----------|
| `aylik_grafik(yonetici)` | Aylık gelir/gider/bakiye çizgi grafiği |
| `gelir_gider_bar(yonetici)` | Toplam gelir–gider sütun grafiği |
| `pasta_grafik(yonetici)` | Gider/gelir kategori pasta grafiği |
| `kategori_bar(yonetici)` | Kategoriye göre yatay sütun grafiği |
| `grafik_menu(yonetici)` | Grafik seçim alt menüsü |

---

## 🗂️ Kullanılan Veri Yapıları

```python
# FinansYoneticisi içinde:
gelirler: list[Islem] = []   # Tüm gelir nesneleri
giderler: list[Islem] = []   # Tüm gider nesneleri

# Her eleman bir Islem nesnesidir:
islem = Islem(id=1, tutar=5000.0, tarih="2026-06-01",
              aciklama="Maaş", tip="gelir", kategori="Maaş")
```

---

## 🛠️ Kurulum ve Çalıştırma

### Gereksinimler
```bash
pip install pandas numpy matplotlib seaborn openpyxl
```

### Çalıştırma
```bash
cd MustafaSukruEgribas_24903003_BGY210
python main.py
```

### Ana Menü
```
═══════════════════════════════════════════════════════
  💰  KİŞİSEL FİNANS TAKİP SİSTEMİ
      Mustafa Şükrü Egrıbaş – 24903003
═══════════════════════════════════════════════════════
  1  ➜  Gelir Ekle
  2  ➜  Gider Ekle
  3  ➜  İşlemleri Listele
  4  ➜  Analiz Yap
  5  ➜  Grafik Göster
  6  ➜  CSV Kaydet / Yükle
  7  ➜  Excel'e Aktar
  8  ➜  İşlem Sil
  9  ➜  Aylık Tabloyu Güncelle (Manuel)
  0  ➜  Çıkış
═══════════════════════════════════════════════════════
```

---

## 🧠 Öğrenme Çıktıları ile Örtüşme

| Ö.Ç | Konu | Karşılandığı Modül |
|-----|------|--------------------|
| 1 | İleri düzey veri yapıları, OOP | `finans_modeli.py`, `islem_yonetimi.py` |
| 2 | NumPy, Pandas, Matplotlib | `analiz.py`, `gorsellestirme.py` |
| 3 | Dosya I/O (CSV, Excel) | `dosya_islemleri.py` |
| 4 | Konsol uygulaması | `main.py`, `utils.py` |

---

## 📊 Özellikler

- ✅ Tam modüler yapı (7 ayrı dosya)
- ✅ OOP: `Islem` + `FinansYoneticisi` sınıfları
- ✅ CSV otomatik kayıt ve yükleme
- ✅ Excel export (3 sayfa, renkli, biçimli)
- ✅ Aylık tablo manuel güncelleme (`aylik_ozet.txt`)
- ✅ Pandas & NumPy analizleri
- ✅ 4 farklı grafik türü (PNG kayıt)
- ✅ Kategori sistemi
- ✅ Try-except hata yönetimi
- ✅ Docstring ve clean code prensipleri

---

*BGY210 – Python Programlama II | Bahar 2026 | Kayseri Üniversitesi*
