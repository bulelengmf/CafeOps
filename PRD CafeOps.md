# **PRD: CafeOps — Web App Mobile-First untuk Inventory & Purchasing Cafe**

**Versi:** 1.0 (Draft) · **Tanggal:** 26 Oktober 2026 · **Sumber:** dokumen analisis sistem Excel Inventory & Purchasing (hasil.docx) · **Platform:** Website responsif dengan tampilan mobile (Progressive Web App)

## **1\. Ringkasan Eksekutif**

CafeOps adalah aplikasi web yang dirancang dengan tampilan mobile-first, dibuka lewat browser di HP tanpa perlu instal dari app store, dan dapat dipasang ke layar utama (PWA). Aplikasi ini memindahkan seluruh sistem Excel 13 sheet yang sudah dirancang (master data, purchasing, receiving, stok, aset, laporan) menjadi alur kerja digital yang bisa dipakai barista, admin purchasing, manager, dan finance langsung dari lantai cafe.

Nilai utama: (1) data tercatat saat kejadian, bukan direkap belakangan; (2) kontrol internal (approval, audit trail, 3-way matching) berjalan otomatis walau satu staf merangkap beberapa peran; (3) siap diperluas ke multi-outlet pada tahun ke-2.

## **2\. Latar Belakang dan Masalah**

Cafe saat ini memiliki 1 outlet, POS buatan sendiri tanpa Auto-BOM, pembelian hybrid (supplier formal dan belanja tunai di pasar), serta staf yang merangkap peran. Dari analisis, empat masalah utama yang harus diselesaikan aplikasi:

| \# | Masalah | Dampak | Respons produk |
| :---- | :---- | :---- | :---- |
| 1 | Perangkapan tugas tanpa check and balance | Risiko ghost receiving, kolusi, manipulasi opname | Approval wajib oleh Manager, audit trail tak bisa dihapus, spot check terjadwal |
| 2 | Pembelian pasar tanpa nota standar | Markup, nota fiktif, selisih kas kecil | Formulir Belanja Pasar dengan foto nota, perbandingan ke price benchmark |
| 3 | Stok sistem selisih dengan fisik | Food/beverage cost tidak diketahui | Log pemakaian harian cepat, opname terjadwal, laporan variance |
| 4 | Valuasi bingung (WACC vs FIFO) | HPP tidak konsisten | Valuasi WAC otomatis, FEFO per batch untuk fisik |

## **3\. Tujuan, Non-Tujuan, dan Metrik Sukses**

### **3.1 Tujuan**

* Mengganti pencatatan Excel dengan input mobile yang selesai kurang dari 30 detik per transaksi rutin.  
* Menegakkan kontrol wajib: bukti fisik, pemeriksaan barang sebelum masuk stok, dan approval berjenjang.  
* Memberi manager dan owner dashboard stok, waste, dan variance secara real-time.  
* Menyiapkan arsitektur multi-lokasi sejak awal.

### **3.2 Non-Tujuan (di luar rilis awal)**

* Pengganti POS atau integrasi penuh Auto-BOM (masuk Fase 3).  
* Modul akuntansi lengkap (jurnal, buku besar umum). Aplikasi hanya menyediakan data persediaan dan ekspor untuk finance.  
* Aplikasi native iOS/Android.

### **3.3 Metrik Sukses**

| Metrik | Target |
| :---- | :---- |
| Inventory Accuracy (opname vs sistem) | di atas 95% dalam 3 bulan setelah go-live |
| Waste Rate | di bawah 3–5% dari total pembelian |
| Stockout Frequency bahan utama | 0 kali per bulan |
| Receiving Discrepancy Rate | di bawah 5% PO |
| Purchase Price Variance | mendekati 0% |
| Adopsi: transaksi dicatat di aplikasi (bukan Excel/kertas) | di atas 90% pada bulan ke-2 |
| Waktu input barang masuk | kurang dari 1 menit per penerimaan |

## **4\. Pengguna dan Peran**

| Peran | Tugas utama di aplikasi | Perangkat utama |
| :---- | :---- | :---- |
| Barista / Staff | Buat permintaan beli (PR), catat pemakaian dan waste, terima barang, hitung opname | HP di cafe |
| Admin Purchasing / Cost Controller | Kelola master data, buat PO, pantau pengiriman, cek harga vs benchmark | HP dan laptop |
| Cafe Manager | Approval PR/PO, approval penyesuaian stok, spot check, audit harian | HP |
| Finance / Owner | 3-way matching, pelunasan, audit bulanan, laporan valuasi | HP dan laptop |

Catatan penting: satu akun memiliki satu peran utama, tetapi sistem mengizinkan satu orang diberi lebih dari satu peran. Saat itu terjadi, aturan kontrol kompensasi di Bagian 8 otomatis aktif.

## **5\. Ruang Lingkup dan Fase Rilis**

### **Fase 1 — MVP (target 8–10 minggu)**

* Login dan manajemen peran, audit trail.  
* Master Data: Item, Supplier, Konversi Satuan, Kategori (CAT-A sampai CAT-G).  
* PR, PO dengan approval, Receiving dan QC, Karantina.  
* Ledger stok, Log Pemakaian Harian dan Waste, Stock Opname.  
* Belanja Pasar (petty cash) dengan foto nota.  
* Dashboard dasar: nilai stok, stok di bawah minimum, mendekati kedaluwarsa.  
* Impor data awal dari Excel.

### **Fase 2**

* Invoice dan 3-way matching, status pembayaran.  
* CAPEX Register dan penyusutan sederhana.  
* Price Benchmark mingguan, penilaian kinerja supplier.  
* KPI lengkap (5 KPI), ekspor Excel/PDF, notifikasi push dan WhatsApp.

### **Fase 3**

* Multi-outlet penuh dan transfer stok antar outlet.  
* Resep (BOM) dan integrasi POS buatan sendiri untuk pemotongan stok otomatis.  
* Saran pembelian otomatis berdasarkan pemakaian dan lead time.

## **6\. Prinsip UX Mobile-First**

* **Desain utama 360–430 px.** Desktop hanya memperluas layout (maksimal lebar konten sekitar 480 px untuk alur input, tabel lebar untuk laporan).  
* **Navigasi bawah (bottom navigation)** dengan 5 tab: Beranda, Beli, Terima, Stok, Laporan. Aksi utama lewat tombol mengambang (+).  
* **Satu layar, satu tugas.** Formulir pendek, bertahap (stepper), tombol besar minimal 44 px, jangkauan jempol.  
* **Input cepat:** pencarian barang dengan autocomplete, pemindai barcode/QR via kamera (opsional), satuan default, angka dengan keypad numerik.  
* **Kamera langsung** untuk foto nota, foto barang rusak, dan bukti penerimaan, dikompres otomatis.  
* **Offline-tolerant:** pencatatan pemakaian, waste, dan opname tetap bisa dilakukan saat sinyal lemah, lalu disinkronkan. Transaksi yang butuh approval hanya dikirim saat online.  
* **Kode warna status** konsisten (Draft, Menunggu approval, Disetujui, Ditolak, Selesai) dan bahasa Indonesia yang sederhana.  
* **Aksesibilitas:** kontras cukup, ukuran font minimal 16 px, mode gelap mengikuti perangkat.  
* **PWA:** dapat dipasang di layar utama, ikon dan splash screen, memuat cepat.

## **7\. Alur Pengguna Utama**

### **7.1 Alur Pembelian End-to-End**

1. Barista membuat PR (atau sistem menyarankan karena stok di bawah minimum).  
2. Cost Controller memeriksa stok dan anggaran, memilih supplier, dan membuat PO.  
3. Cafe Manager menyetujui atau menolak PO (wajib, tidak bisa dilewati).  
4. PO dikirim ke supplier (bagikan PDF/WhatsApp).  
5. Barang datang: penerima memeriksa jumlah dan kualitas di layar Receiving, memotret surat jalan, memisahkan barang rusak ke Karantina.  
6. Stok masuk ke ledger hanya setelah QC disimpan.  
7. Finance mencocokkan PO, surat jalan, dan invoice (3-way matching), lalu menandai lunas.  
8. Barista mencatat pemakaian dan waste harian.  
9. Opname periodik, variance diinvestigasi, penyesuaian disetujui Manager.  
10. Finance merekonsiliasi pembayaran dan mengevaluasi supplier.

Untuk bahan rutin harian (susu, es batu), tersedia PO Mingguan yang menggabungkan PR dan PO dalam satu approval Manager agar tidak birokratis.

### **7.2 Alur Belanja Pasar (Kas Kecil)**

1. Admin/Barista membuka Belanja Pasar, memilih barang, mengisi jumlah dan harga estimasi.  
2. Setelah belanja, isi harga aktual dan unggah foto nota (wajib).  
3. Sistem membandingkan dengan Price Benchmark dan menandai harga yang menyimpang di atas ambang yang ditentukan.  
4. Manager/Owner memverifikasi dan menyetujui. Barang masuk stok setelah QC penerimaan.

## **8\. Kebutuhan Fungsional**

Prioritas: **P0** wajib MVP, **P1** Fase 2, **P2** Fase 3\.

### **8.1 Autentikasi dan Peran**

| ID | Kebutuhan | Prioritas |
| :---- | :---- | :---- |
| FR-001 | Login dengan email/nomor HP dan kata sandi atau PIN 6 digit. | P0 |
| FR-002 | Role-based access: Barista, Admin Purchasing, Manager, Finance/Owner. | P0 |
| FR-003 | Satu pengguna boleh memiliki beberapa peran; sistem mencatat peran yang dipakai di setiap transaksi. | P0 |
| FR-004 | Pengguna terhubung ke satu atau banyak outlet (outlet\_id). | P0 |

### **8.2 Master Data**

| ID | Kebutuhan | Prioritas |
| :---- | :---- | :---- |
| FR-010 | CRUD Item: ID unik (RM-001, PKG-001, CAPEX-001), nama, kategori, satuan beli, satuan pakai, faktor konversi, min stock, metode valuasi, status. | P0 |
| FR-011 | Kategori tetap CAT-A sampai CAT-G sesuai klasifikasi. | P0 |
| FR-012 | CRUD Supplier (formal dan pasar): kontak, kategori barang, termin pembayaran. | P0 |
| FR-013 | Tabel konversi satuan (1 dus \= 12 botol, 1 botol \= 1000 ml). | P0 |
| FR-014 | Barang tidak dihapus, hanya dinonaktifkan (Discontinued). | P0 |
| FR-015 | Penandaan otomatis CAPEX bila nilai satuan sama dengan atau di atas Rp 2.000.000, di bawah itu OPEX. | P0 |

### **8.3 Purchase Requisition dan Purchase Order**

| ID | Kebutuhan | Prioritas |
| :---- | :---- | :---- |
| FR-020 | Buat PR: pilih item, jumlah, alasan, tanggal dibutuhkan. | P0 |
| FR-021 | Peringatan saat stok di bawah minimum dengan tombol Buat PR. | P0 |
| FR-022 | Konversi PR menjadi PO, pilih supplier, harga acuan terisi dari terakhir beli. | P0 |
| FR-023 | Status PO: Draft, Menunggu Approval, Disetujui, Dikirim, Diterima Sebagian, Selesai, Dibatalkan. | P0 |
| FR-024 | Approval/penolakan PO oleh Manager dengan catatan. | P0 |
| FR-025 | Ekspor PO sebagai PDF dan bagikan lewat WhatsApp. | P1 |
| FR-026 | PO Mingguan gabungan untuk bahan rutin. | P1 |

### **8.4 Receiving dan QC**

| ID | Kebutuhan | Prioritas |
| :---- | :---- | :---- |
| FR-030 | Buka PO yang akan diterima, isi jumlah diterima, jumlah ditolak/rusak, kualitas, tanggal kedaluwarsa per batch. | P0 |
| FR-031 | Foto surat jalan dan barang rusak. | P0 |
| FR-032 | Barang tidak masuk stok aktif sebelum QC disimpan; barang rusak otomatis masuk CAT-G Karantina. | P0 |
| FR-033 | Dukungan penerimaan parsial dan penerimaan tanpa PO (ditandai dan butuh approval). | P0 |
| FR-034 | Keputusan akhir barang karantina: retur ke supplier atau write-off (butuh approval Manager). | P0 |

### **8.5 Stok, Pemakaian, Waste, dan Opname**

| ID | Kebutuhan | Prioritas |
| :---- | :---- | :---- |
| FR-040 | Stock Movement Ledger otomatis dari semua transaksi (IN-Purchase, OUT-Usage, OUT-Waste, ADJ-Opname); tidak bisa diedit, koreksi lewat entri pembalik. | P0 |
| FR-041 | Log pemakaian harian: pilih item, jumlah, kategori (pemakaian, spill, staff meal, rusak/kedaluwarsa), foto opsional untuk waste. | P0 |
| FR-042 | Stock opname: daftar item per kategori/rak, input hitung fisik, selisih otomatis, alasan wajib bila di atas ambang. | P0 |
| FR-043 | Opname buta (blind count): stok sistem disembunyikan dari penghitung. | P0 |
| FR-044 | Penyesuaian stok hasil opname hanya efektif setelah disetujui Manager. | P0 |
| FR-045 | Daftar FEFO: barang mendekati kedaluwarsa diurutkan, peringatan 7 hari dan 3 hari. | P0 |
| FR-046 | Jadwal opname otomatis: mingguan untuk bahan bernilai tinggi/perishable, bulanan penuh. | P1 |

### **8.6 Belanja Pasar dan Kas Kecil**

| ID | Kebutuhan | Prioritas |
| :---- | :---- | :---- |
| FR-050 | Formulir Belanja Pasar dengan foto nota wajib, tanggal, nama toko, pembeli, dan saksi/penyetuju. | P0 |
| FR-051 | Price Benchmark per item; harga di luar toleransi ditandai merah. | P1 |
| FR-052 | Rekap kas kecil harian: saldo awal, belanja, sisa; cocokkan dengan nota. | P0 |

### **8.7 Invoice, Pembayaran, dan Aset**

| ID | Kebutuhan | Prioritas |
| :---- | :---- | :---- |
| FR-060 | Input invoice dan 3-way matching PO, penerimaan, invoice; selisih ditandai. | P1 |
| FR-061 | Status pembayaran: Belum Dibayar, Sebagian, Lunas; jatuh tempo dan pengingat. | P1 |
| FR-062 | CAPEX Register: nilai, tanggal beli, lokasi, penanggung jawab, umur manfaat, penyusutan garis lurus. | P1 |
| FR-063 | Daftar inventaris alat CAT-E (di bawah Rp 2 juta) tanpa penyusutan. | P1 |

### **8.8 Valuasi, Dashboard, dan Laporan**

| ID | Kebutuhan | Prioritas |
| :---- | :---- | :---- |
| FR-070 | Valuasi Weighted Average Cost otomatis: Harga rata-rata baru \= (Stok lama × Harga lama \+ Pembelian baru × Harga baru) / (Stok lama \+ Pembelian baru). | P0 |
| FR-071 | Dashboard: total nilai stok, stok di bawah minimum, mendekati kedaluwarsa, PO menunggu approval, variance opname terakhir. | P0 |
| FR-072 | Laporan 5 KPI (Bagian 11\) dengan filter periode dan outlet. | P1 |
| FR-073 | Ekspor laporan ke Excel dan PDF. | P1 |
| FR-074 | Estimasi food/beverage cost berdasarkan pemakaian (sebelum Auto-BOM). | P1 |

### **8.9 Notifikasi dan Audit**

| ID | Kebutuhan | Prioritas |
| :---- | :---- | :---- |
| FR-080 | Audit trail untuk setiap perubahan: siapa, kapan, nilai lama dan baru, perangkat. | P0 |
| FR-081 | Notifikasi dalam aplikasi untuk approval, stok minimum, dan kedaluwarsa. | P0 |
| FR-082 | Push notification dan WhatsApp. | P1 |
| FR-083 | Checklist audit harian, mingguan, bulanan untuk Manager dan Finance dengan status selesai. | P1 |

## **9\. Aturan Bisnis dan Kontrol Internal**

1. Setiap pembelian wajib punya bukti: invoice untuk supplier formal, foto nota bertanggal untuk pasar.  
2. Barang tidak masuk stok sebelum pemeriksaan fisik (jumlah dan kualitas).  
3. Pembuat PO tidak boleh menyetujui PO yang sama. Bila pembuat dan penerima barang adalah orang yang sama, sistem menandai transaksi dan mewajibkan spot check Manager.  
4. Pembuat dan pemegang pembayaran utama tidak boleh sama dalam satu transaksi; pelunasan perlu verifikasi Finance atau Manager.  
5. Penyesuaian stok, write-off, dan pembatalan transaksi selalu butuh approval Manager.  
6. Ledger bersifat append-only; tidak ada hapus, hanya pembalikan.  
7. Valuasi keuangan memakai Weighted Average Cost; fisik gudang memakai FEFO/FIFO berbasis batch dan tanggal kedaluwarsa.  
8. Barang bernilai satuan di bawah Rp 2.000.000 adalah OPEX, dan sama dengan atau di atas itu adalah CAPEX dan masuk Asset Register, bukan food/beverage cost.  
9. Barang karantina (CAT-G) dipisahkan secara data dan fisik dari stok aktif.  
10. Ambang yang bisa diatur oleh Owner: toleransi harga pasar, ambang variance opname, batas nilai PO yang butuh approval ganda.

## **10\. Model Data (Entitas Utama)**

Setiap tabel memiliki id unik, outlet\_id, created\_by, created\_at, updated\_at agar siap multi-outlet dan teraudit.

| Entitas | Atribut kunci | Relasi |
| :---- | :---- | :---- |
| Outlet | outlet\_id, nama, alamat | induk semua data |
| User | user\_id, nama, peran (boleh banyak), outlet | membuat/menyetujui transaksi |
| Item | item\_id, nama, kategori, satuan beli, satuan pakai, konversi, min stock, valuasi, status | dipakai di PR, PO, ledger |
| Supplier | supplier\_id, tipe (formal/pasar), kontak, termin | PO, invoice |
| UnitConversion | dari, ke, faktor | Item |
| PurchaseRequisition | pr\_id, requester, status, tanggal butuh | PR\_Line → Item |
| PurchaseOrder | po\_id, supplier, status, approver, total | PO\_Line → Item |
| Receiving | recv\_id, po\_id, penerima, foto, status QC | Receiving\_Line (diterima, ditolak, batch, expired) |
| MarketPurchase | mp\_id, toko, pembeli, foto nota, approver | Line → Item |
| StockLedger | log\_id, tanggal, item\_id, tipe transaksi, reference\_id, qty\_in, qty\_out, unit\_cost, total\_value, recorded\_by | sumber kebenaran stok |
| UsageWasteLog | log\_id, item, qty, jenis, foto | Ledger |
| StockOpname | opname\_id, periode, penghitung, status | Opname\_Line (qty fisik, qty sistem, selisih, alasan) |
| Invoice | invoice\_id, po\_id, nilai, status match, status bayar | Payment |
| Asset | asset\_id, item, nilai, lokasi, PIC, umur manfaat | CAPEX Register |
| PriceBenchmark | item\_id, harga acuan, periode | PPV, peringatan pasar |
| AuditLog | siapa, apa, kapan, sebelum, sesudah | semua entitas |

Stok saat ini tidak disimpan sebagai angka bebas, melainkan dihitung dari StockLedger (dengan cache untuk performa).

## **11\. KPI dan Pelaporan**

| KPI | Formula | Target | Sumber |
| :---- | :---- | :---- | :---- |
| Inventory Accuracy | item sesuai / total item dicek × 100% | di atas 95% | Stock Opname |
| Waste Rate | nilai waste / total pembelian × 100% | di bawah 3–5% | Usage/Waste Log |
| Stockout Frequency | jumlah kejadian bahan utama habis | 0 per bulan | Catatan stockout |
| Receiving Discrepancy Rate | PO bermasalah / total PO × 100% | di bawah 5% | Receiving |
| Purchase Price Variance | (harga aktual − harga acuan) / harga acuan | mendekati 0% | PO dan Invoice |

Setiap KPI menampilkan tren, daftar penyebab (drill-down ke transaksi), dan tindak lanjut yang disarankan sesuai dokumen analisis.

## **12\. Arsitektur Informasi dan Layar**

**Navigasi bawah:**

* **Beranda:** ringkasan hari ini, tugas menunggu (approval, opname), peringatan stok dan kedaluwarsa.  
* **Beli:** PR, PO, Belanja Pasar, Supplier.  
* **Terima:** daftar PO datang hari ini, form Receiving/QC, Karantina.  
* **Stok:** daftar item dan stok, Log Pemakaian/Waste, Opname, Ledger.  
* **Laporan:** Dashboard, KPI, Valuasi, CAPEX Register, ekspor.

**Menu Lainnya (profil):** Master Data, pengguna dan peran, pengaturan ambang, audit trail.

**Layar kunci MVP:** Login, Beranda, Daftar dan Detail Item, Form PR, Form PO, Antrean Approval, Form Receiving/QC, Form Belanja Pasar, Log Pemakaian Cepat, Hitung Opname, Detail Variance, Dashboard.

## **13\. Kebutuhan Non-Fungsional**

| Aspek | Persyaratan |
| :---- | :---- |
| Performa | Halaman utama dimuat di bawah 3 detik pada jaringan 4G; interaksi di bawah 200 ms. |
| Kompatibilitas | Chrome dan Safari mobile (2 versi terakhir), Android 9+, iOS 15+; desktop modern. |
| Offline | Pencatatan pemakaian, waste, dan opname dapat dilakukan offline dengan antrean sinkronisasi dan penanganan konflik (last-write dengan peringatan). |
| Keamanan | HTTPS, hash kata sandi, sesi dengan kedaluwarsa, pembatasan percobaan login, kontrol akses di sisi server, enkripsi data saat transit dan tersimpan. |
| Privasi dan data | Foto nota disimpan terenkripsi; retensi data minimal 5 tahun untuk kebutuhan audit. |
| Keandalan | Cadangan otomatis harian, uptime target 99,5%. |
| Skalabilitas | Dirancang multi-outlet (outlet\_id di semua tabel) dan dukung ribuan transaksi per bulan tanpa perubahan arsitektur. |
| Bahasa | Bahasa Indonesia sebagai default; format Rupiah dan tanggal lokal; struktur siap multi-bahasa. |
| Auditabilitas | Semua aksi sensitif tercatat dan tidak dapat diubah oleh pengguna biasa. |

## **14\. Rekomendasi Teknis**

* **Frontend:** Next.js atau React (Vite) dengan Tailwind, komponen mobile-first, PWA (service worker, manifest), penyimpanan offline IndexedDB.  
* **Backend dan database:** PostgreSQL dengan Row Level Security per outlet; opsi cepat memakai Supabase atau Firebase, atau API sendiri (Node.js/NestJS).  
* **File:** object storage untuk foto nota dengan kompresi sisi klien.  
* **Autentikasi:** email/OTP atau PIN, role dan permission di server.  
* **Pelaporan:** query SQL view untuk KPI dan valuasi; ekspor Excel/PDF di server.  
* **Integrasi berikutnya:** API untuk POS buatan sendiri (Fase 3\) dan WhatsApp Business API untuk notifikasi.  
* **Hosting:** layanan cloud dengan cadangan otomatis (misal Vercel atau Cloud Run dan database terkelola).

## **15\. Migrasi dari Excel**

1. Bersihkan dan standarkan Item\_Master, Supplier\_Master, dan konversi satuan; beri ID unik.  
2. Impor master data lewat template CSV/Excel dengan validasi dan laporan kesalahan.  
3. Lakukan opname penuh sebagai saldo awal (opening balance) pada tanggal cut-over, lengkap dengan harga rata-rata awal.  
4. Jalankan paralel Excel dan aplikasi selama 2–4 minggu, bandingkan stok mingguan.  
5. Go-live penuh, Excel dibekukan menjadi arsip baca saja.  
6. Pelatihan singkat per peran (30–45 menit) dan panduan satu halaman di aplikasi.

## **16\. Roadmap dan Tonggak**

| Tonggak | Estimasi | Keluaran |
| :---- | :---- | :---- |
| Discovery dan desain UX (wireframe, prototipe) | Minggu 1–2 | Prototipe mobile tervalidasi dengan staf cafe |
| Pengembangan MVP sprint 1–3 | Minggu 3–8 | Master data, PR/PO, Receiving, Ledger, Pemakaian, Opname |
| UAT dan migrasi data | Minggu 9–10 | Data awal, uji paralel, perbaikan |
| Go-live MVP | Minggu 10–11 | Operasional memakai aplikasi |
| Fase 2 | Bulan 3–5 | Invoice, 3-way matching, CAPEX, KPI penuh, notifikasi |
| Fase 3 | Bulan 6–12 (sebelum buka cabang) | Multi-outlet, BOM, integrasi POS |

## **17\. Risiko dan Mitigasi**

| Risiko | Dampak | Mitigasi |
| :---- | :---- | :---- |
| Staf enggan pindah dari Excel/kertas | Data tidak lengkap | Input super cepat, pelatihan, paralel run, Manager menolak laporan di luar sistem |
| Sinyal buruk di cafe/pasar | Data hilang | Mode offline untuk pencatatan inti, antrean sinkronisasi |
| Perangkapan peran disalahgunakan | Kecurangan | Flag otomatis, spot check wajib, laporan transaksi berisiko |
| Konversi satuan salah | Stok tidak akurat | Validasi konversi, peringatan lonjakan tidak wajar |
| Scope membengkak | Rilis molor | Disiplin fase, prioritas P0 saja untuk MVP |
| Ketergantungan satu pengembang | Keberlanjutan | Dokumentasi, stack umum, kode di repositori bersama |

## **18\. Asumsi dan Pertanyaan Terbuka**

**Asumsi:** 1 outlet pada tahap awal; staf memiliki smartphone dengan kamera; internet cafe tersedia; valuasi memakai WAC dengan FEFO fisik; ambang CAPEX Rp 2.000.000.

**Perlu diputuskan bersama:**

1. Siapa yang menjadi pemilik akhir (Owner) dan siapa saja akun Finance?  
2. Apakah PO perlu approval ganda di atas nilai tertentu? Berapa batasnya?  
3. Berapa toleransi harga pasar terhadap benchmark (misal 10%)?  
4. Apakah pelaporan perlu terhubung langsung ke software akuntansi tertentu?  
5. Apakah POS buatan sendiri sudah memiliki API atau akses basis data untuk integrasi Fase 3?  
6. Apakah barcode/QR pada item diperlukan, atau cukup pencarian nama?  
7. Apakah dibutuhkan peran Supplier (portal terbatas) di masa depan?

## **19\. Lampiran: Pemetaan dari Excel ke Aplikasi**

| Sheet Excel | Modul di aplikasi |
| :---- | :---- |
| Item\_Master, Supplier\_Master, Unit\_Conversion | Master Data |
| Purchase\_Requisition, Purchase\_Order | Beli (PR, PO) |
| Receiving\_QC | Terima (Receiving, Karantina) |
| Invoice\_Payment | Laporan/Finance (Invoice, 3-way matching) |
| Stock\_Movement\_Ledger | Stok (Ledger) |
| Daily\_Usage\_Waste | Stok (Pemakaian dan Waste) |
| Stock\_Opname | Stok (Opname) |
| CAPEX\_Register | Laporan (Aset) |
| Inventory\_Valuation, Dashboard\_Summary | Laporan (Valuasi, Dashboard, KPI) |

