# 1. Pengantar ke AWS

- pay-as-you-go: bayar sesuai penggunaan
- upfront expense: bayar dimuka
- on-demand: sesuai permintaan
- on-premise: server lokal / cloud-private

# 2. Komputasi di Cloud

## Pengenalan ke EC2

- Amazon EC2 (Elastic Compute Cloud): layanan \u mengakses server virtual AWS.
- EC2 vs data center on-premise:
  - kapasitas fleksibel
  - hemat biaya
  - cepat
- Instance: sebutan \u server virtual di AWS.
- EC2 berjalan di host (mesin fisik) \dg teknologi virtualisasi. 1 host \u \byk instance (virtual machines-VM).
- Tugas hypervisor:
  - membagi sumber daya host \u semua VM.
  - mengisolasi antar VM saat berbagi sumber daya.
- Konfigurasi instance fleksibel: sistem operasi, instalasi software, ukuran (\dg vertical scalling--menambah memori/CPU--), jaringan (jenis request, publik/privat).
- Cara kerja EC2:
  - luncurkan, pilih template \dg konfigurasi dasar, lalu atur jaringan & keamanan.
  - hubungkan, instance \dp diakses \dr desktop, \dll.
  - gunakan, install software, tambah storage, menyalin file, \dll.

## Tipe Instance EC2

- Setiap tipe instance dikelompokkan \dl 1 instance family \u tugas tertentu.
- Instance family:
  - General purpose instances, seimbang antara sumber daya komputasi, memori, & jaringan. Bisa \sbg server apk web / code repo.
  - Compute optimized instances, ideal \u komputasi tinggi \dg performa prosesor tinggi, \spt: server game, HPC (high performance computing), / pemodelan ilmiah. Bisa \u beban kerja batch processing.
  - Memory optimized instances, \u beban kerja memproses kumpulan data besar di memori, \spt relasional & non-relasional / HPC.
  - Accelerated computing instances, \u menjalankan beberapa fungsi \lb efisien \drpd software \y berjalan di CPU, \ct kalkulasi floating-point, pemrosesan grafik, & data pattern matching.
  - Storage optimized instance, \u beban kerja membaca (read) & menulis (write) tinggi & berurutan \dr database besar di local storage. Bisa \u sistem file terdistribusi, data warehouse (gudang data), online transaction processing system. Cocok jika butuh input /output operation per second (IOPS) tinggi.

## Harga EC2

- On-demand (sesuai permintaan), membayar selama instance berjalan--\dp per jam / per detik--.
- Savings Plans (Rencana Tabungan), mengurangi biaya komputasi \dg berkomitmen \thd \jml dolar/jam \y keluar & penggunaan komputasi \y konsisten \u jangka waktu 1 / 3 tahun.
- Reserved Instances (Instance Terpesan), menawarkan diskon penagihan \y diterapkan \u instance On-Demand \dg berkomitmen \thd tingkat penggunaan \u jangka waktu 1 / 3 tahun.
- Spot Instances, menggunakan kapasitas komputasi Amazon EC2 \y \t terpakai & menawarkan penghematan biaya hingga 90% \dr harga On-Demand. Opsi ini sangat ideal \u beban kerja \dg waktu mulai & akhir \y fleksibel & \t masalah \dg interupsi.
- Dedicated Hosts (Host Khusus), server fisik \dr kapasitas EC2 instance \y didedikasikan sepenuhnya \u Anda gunakan.

## Penyesuaian Kapasitas EC2

- Skalabilitas & elastisitas
- Amazon EC2 Auto Scaling, menambah / menghapus Amazon EC2 instances \scr otomatis sesuai kebutuhan.
- Dynamic scaling: merespons \thd perubahan permintaan.
- Predictive scaling: \scr otomatis menjadwalkan \jml Amazon EC2 instances \y tepat berdasarkan prediksi permintaan.
- Scaling up: menambahkan \lb \byk daya \p mesin \y sedang berjalan.
- Scaling out: menambahkan \lb \byk instance agar \dp menangani permintaan.

## Elastic Load Balancing (ELB)

- Load balancing: memastikan bahwa distribusi beban kerja merata di seluruh EC2 instance \shg \t ada 1 instance pun \y menganggur.
- Load balancer: bertindak \sbg 1 titik kontak \u semua traffic web \y masuk ke Auto Scaling group Anda.
- ELB: regional construct (berjalan di tingkat Region), bukan \p individu EC2 instance \shg membuatnya highly available \scr otomatis.
- ELB \dp bekerja sama \dg EC2 Auto Scaling \u membantu memastikan aplikasi \y berjalan di EC2 \dp memberikan kinerja & ketersediaan tinggi.
- Decoupled architecture (arsitektur \y terpisah)

## Messaging & Queueing

- Ide \dr menempatkan pesan ke \dl buffer disebut messaging & queueing.
- Tightly coupled architecture: ketika aplikasi berkomunikasi \scr \lsg. Jika ada 1 komponen gagal / berubah, maka akan memicu kegagalan di komponen lain / bahkan seluruh sistem.
- Aplikasi monolitik: desain aplikasi \y menggabungkan berbagai komponen menjadi 1 kesatuan.
- Loosely coupled architecture: jika 1 komponen gagal, maka komponen \tsb akan diisolasi \shg \t akan menyebabkan kegagalan beruntun ke seluruh sistem.
- Aplikasi microservice: komponen dibuat menjadi loosely coupled \shg \dp dikembangkan, di-deploy (diterapkan), & dikelola \scr independen.
- Amazon Simple Queue Service (Amazon SQS) & Amazon Simple Notification Service (Amazon SNS) \u arsitektur \y loosely coupled.
- SQS: mengirim, menyimpan, & menerima pesan antar komponen software \dg volume berapapun tanpa khawatir kehilangan pesan \tsb.
- Data \y terkandung di \dl pesan disebut payload & itu dilindungi hingga terkirim.
- SNS: juga digunakan \u mengirimkan pesan ke layanan. Bedanya, ia juga \dp mengirimkan pemberitahuan ke pelanggan.
- SNS menggunakan model publish/subscribe alias pub/sub.
- SNS topic: membuat suatu saluran \u menyampaikan pesan. Jika ingin mempublikasikan pesan (publish), Anda \dp mengatur pelanggan (subscribers).
- Di SNS, subscribers \dp berupa server web, alamat email, AWS Lambda function, \ beberapa opsi lainnya.

## Layanan Komputasi Tambahan

- Pengguna EC2 bertanggung jawab \u:
  - patching (memperbaiki masalah \dg memperbarui program komputer).
  - menyiapkan scaling.
  - merancang aplikasi \u dijalankan agar high available.
- Serverless: pengguna \t \dp melihat & mengakses infrastruktur dasar \y menjalankan aplikasi. Semua pengelolaan lingkungan \y mendasari penyediaan, scaling, high availability, & pemeliharaan sudah ditangani \shg pengguna \dp fokus \p aplikasi \y akan dijalankan.
- AWS Lambda: layanan serverless AWS.
- AWS Lambda dirancang \u menjalankan kode di bawah 15 menit \shg tdk cocok \u proses \y berjalan lama \spt deep learning.
- Container: \u efisiensi & portabilitas.
-  Amazon Elastic Container Service (Amazon ECS) & Amazon Elastic Kubernetes Service (Amazon EKS). Keduanya \a container orchestration.
- Container menyediakan cara \u mengemas kode, konfigurasi, & dependensi aplikasi ke \dl 1 objek.
- Container bekerja di atas EC2 instance & berjalan \scr terpisah 1 sama lain. Cara kerja container serupa \dg mesin virtual, namun \dl kasus ini, host-nya (server) \a EC2 instance.
- ECS & EKS berjalan di atas EC2. Jika \t ingin sibuk mengurusi EC2, gunakan AWS Fargate.
- AWS Fargate: platform komputasi serverless \u ECS & EKS.

# 3. Infrastruktur Global & Keandalan

## Pengantar

- High availability: kemampuan \u memastikan bahwa sistem selalu bekerja & \dp diakses \dg waktu henti \y minimal tanpa memerlukan intervensi manusia.
- Fault tolerance: sistem masih mampu beroperasi meskipun beberapa komponen mengalami kegagalan.

## Infrastruktur Global AWS

- AWS Regions memiliki beberapa data center \y berisi semua sumber daya \y dibutuhkan \spt komputasi, penyimpanan, jaringan, \dll.
- Setiap Region terkoneksi \dg region lain melalui high speed fiber network, & juga terisolasi \dr region lain kecuali Anda memberinya izin.
- 4 faktor bisnis \y menentukan pemilihan suatu Region:
  - Compliance (kepatuhan): mengikuti standar \y ditetapkan pemerintah.
  - Proximity (Kedekatan): latensi (waktu \u mengirim & menerima data) \dp semakin kecil & pengiriman konten ke pelanggan jadi \lb cepat.
  - Feature Availability (Ketersediaan Fitur): Region terdekat mungkin \t memiliki semua fitur AWS dibutuhkan.
  - Pricing (Harga): beberapa lokasi \dp \lb mahal pengoperasiannya.
- Availability Zone (AZ): 1 / sekelompok data center \dl 1 region.
- Setiap Regions terdiri \dr beberapa AZ \y terisolasi & \scr fisik terpisah di \dl Region geografis.
- EC2 menjalankan VM \p hardware \y ada di AZ. Best practice-nya, jalankan setidaknya 2 AZ \dl 1 Region.

## Edge Locations

- Content Delivery Network (CDN): teknik menyimpan salinandata di cache \dg lokasi \y \lb dekat \dg pelanggan.
- Amazon CloudFront: layanan CDN \u mengirim data ke seluruh dunia \dg latensi rendah & kecepatan transfer \y tinggi.
- Edge locations: lokasi \y digunakan CloudFront \u menyimpan salinan cache. Edge locations terpisah \dr Regions.
- Amazon Route 53: layanan domain name system (DNS) menggunakan edge locations.
-  AWS Outposts: menginstal Region mini \y beroperasi penuh, tepat di \dl data center Anda sendiri.

## Menyediakan Sumber Daya AWS

- Di AWS semua aktivitas \a panggilan API.
- AWS Management Console: antarmuka berbasis browser \y \dp digunakan \u mengakses & mengelola layanan AWS. Fungsi:
  - mencari layanan AWS \dr nama, kata kunci, / akronim.
  - membangun lingkungan pengujian.
  - melihat tagihan AWS.
  - melakukan pemantauan.
  - bekerja \dg sumber daya non-teknis lainnya.
- AWS Command Line Interface (CLI): mengendalikan layanan AWS \dg baris perintah melalui 1 alat, juga \dp menjalankan skrip \tsb \scr otomatis.
- AWS Software Development Kit (SDK): \u berinteraksi \dg sumber daya AWS melalui berbagai bahasa pemrograman, & memudahkan developer \u membuat program di AWS tanpa menggunakan low-level API.
- Low-level API: memungkinkan Anda \u memanipulasi fungsi di \dl API \scr terperinci sesuai \dg kebutuhan.
- high-level API: memberikan \lb \byk fungsi \dl 1 perintah & \lb mudah digunakan.
- AWS Elastic Beanstalk: membantu menyediakan lingkungan berbasis Amazon EC2. Cukup unggah kode & tentukan konfigurasi \y diinginkan, maka pembangunan lingkungan \spt penyesuaian kapasitas, load balancing, auto-scaling, & pemantauan kesehatan aplikasi akan otomatis dikerjakan.
- AWS CloudFormation: layanan infrastructure as code (IaaS, infrastruktur sebagai kode) \u menentukan berbagai sumber daya AWS \dg cara deklaratif menggunakan CloudFormation template (dokumen berbasis JSON / YAML).
- CloudFormation template \dp dijalankan di beberapa akun / region.

# 4. Jaringan

## Pengantar

- Amazon Virtual Private Cloud (VPC): \u menyediakan bagian logis \dr AWS Cloud \y terisolasi & meluncurkan sumber daya \spt EC2 instance & ELB di dalamnya.
- Sumber daya \tsb \dp menjadi public-facing \y berarti memiliki akses ke internet \ pun private alias tanpa akses internet.

## Konektivitas ke AWS

- Subnet: bagian \dr VPC \y \dp mengelompokkan sumber daya. Subnet bersama dgn aturan jaringan \dp mengontrol apakah sumber daya tersedia \u publik / privat.
- Internet Gateway (IGW): \u mengizinkan traffic \dr internet publik mengalir masuk & keluar dr VPC.
- Virtual Private Gateway (VPG): komponen \y memungkinkan traffic internet \y terlindungi masuk ke \dl VPC, hanya mengizinkan masuk suatu permintaan jika berasal \dr jaringan \y disetujui, bukan internet publik.
- VPN bersifat pribadi & dienkripsi, tetapi ia masih menggunakan koneksi internet reguler \dg bandwidth (\jml maksimum data \y \dp dikirim) \y terbagi ke \byk pengguna internet lainnya.
- AWS Direct Connect: menyediakan koneksi privat, koneksi terdedikasi, \jml latensi \y rendah, & tingkat keamanan \y tinggi.

## Subnet & Network Access Control List (ACL)

- Subnet: bagian \dr VPC \u mengelompokkan sumber daya berdasarkan keamanan / kebutuhan operasional, \dp publik / privat.
- Subnet \dp berkomunikasi 1 sama lain.
- Network ACL: firewall virtual \y mengontrol traffic masuk & keluar (memeriksa izin paket data) di tingkat **subnet**. Anggap \sbg petugas pengawas paspor.
- Setiap akun AWS menyertakan network ACL \scr default (mengizinkan semua traffic masuk & keluar). Bisa diatur agar menolak semua traffic masuk & keluar hingga Anda \scr eksplisit mengizinkannya.
- Security group: firewall virtual \y mengontrol traffic masuk & keluar \u **EC2 instance**.
- Secara default, security group menolak semua traffic masuk namun mengizinkan semua traffic keluar \dr instance.
-  Anggap \spt penjaga pintu di gedung apartemen.
-  Security group bersifat stateful (\dp mengingat siapa \y diizinkan masuk / keluar), network ACL bersifat stateless (\t mengingat apa pun).

## Jaringan Global

- DNS: menerjemahkan nama domain ke alamat IP (Internet Protocol) \y \dp dibaca komputer.
- Amazon Route 53: layanan DNS \y highly available (sangat tersedia) & scalable (\dp diskalakan).
- Route 53 juga \dp mengarahkan traffic ke endpoints (titik akhir) \y berbeda menggunakan beberapa routing policies, \spt Geolocation DNS.
- Geolocation DNS: mengarahkan traffic berdasarkan lokasi pelanggan.

# 5. Penyimpanan & Database

## Instance Store & Amazon Elastic Block Store (EBS)

- Block-level storage (penyimpanan tingkat blok) \u menyimpan data \dl bentuk blok. Anggap \sbg tempat menyimpan file.
- File: serangkaian byte \y disimpan di \dl blok \p disk.
- Instance store: penyimpanan block-level storage sementara \u EC2 instance.
- Jika EC2 instance berhenti, maka semua data di dalamnya akan terhapus.
- EC2 instance \a mesin virtual. Oleh \krn itu, host \y mendasarinya \dp berubah \p saat instance berhenti & memulai.
- Instance store digunakan \u penyimpanan data \y sering berubah, \spt cache, temp file, \dll.
- Amazon Elastic Block Store (EBS): menyediakan block-level storage \y \dp digunakan bersama \dg EC2 instance.
- EBS memungkinkan Anda \u membuat hard drive virtual (EBS volume) lalu memasangnya ke EC2 instance. Ia pun \t terikat \lsg ke host.
- Amazon EBS snapshot: mem-backup data \scr incremental \dr EBS  volume.
- Incremental backup: hanya mencadangkan data \y berubah (delta) \dr pencadangan sebelumnya.


## Amazon Simple Storage Service (S3)

- S3: layanan \u menyimpan & mengambil data \dl bentuk objek \dg \jml \t terbatas. Objek \tsb disimpan \dl bucket. Bucket \dp diatur hak aksesnya.
- Setiap objek terdiri \dr data, metadata, & kunci. Setiap objek maks. berukuran 5 TB.
- Metadata: informasi mengenai data, cara penggunaan, ukurannya, \dll.
- Kunci (key): identifier/pengenal \y unik.
- S3 juga ada fitur versioning.
- Saat mengubah file di object-level storage, maka seluruh objek akan diperbarui.
- S3 storage class:
  - S3 standard: objek \y disimpan akan memiliki 99,999999999% probabilitas tetap utuh \stlh jangka waktu 1 tahun. Data disimpan minimal di 3 AZ.
  - S3 Standard-Infrequent Access (S3 Standard-IA): digunakan \u data \y jarang diakses tapi membutuhkan proses cepat saat dibutuhkan. \ct \u menyimpan backup.
  - S3 One Zone-Infrequent Access (S3 One Zone-IA): Data disimpan hanya di 1 AZ.
  - S3 Intelligent-Tiering: S3 memantau pola akses objek. Jika objek \t diakses selama 30 hari berturut-turut, S3 akan otomatis memindahkannya \dr S3 Standard ke S3 Standard-IA. Jika objek kembali diakses, maka S3 akan otomatis mengembalikannya ke S3 standard.
  - S3 Glacier: ideal \u data audit. Mengaksesnya perlu waktu beberapa menit hingga jam.
  - S3 Glacier Deep Archive: memiliki biaya terendah & ideal \u pengarsipan. Mengaksesnya perlu waktu 12 hingga 48 jam.
- S3 Lifecycle policies: kebijakan \u memindahkan data \scr otomatis antar storage class (kelas penyimpanan).
- Jika Anda memiliki objek / file \y lengkap & hanya membutuhkan sesekali perubahan, maka pilihlah S3. Namun, jika Anda membutuhkan proses read (baca) data \y kompleks, maka pilihlah EBS.

## Amazon Elastic File System (Amazon EFS)

- File server menggunakan block storage \dg local file system \u mengatur file. Client \dp mengakses data di dalamnya melalui file path.
- File storage sangat ideal \u kasus penggunaan di mana data perlu diakses \p waktu \y sama oleh \byk layanan / sumber daya.
- Amazon EFS: sistem file terkelola \y \dp diskalakan & \dp digunakan oleh layanan AWS Cloud & sumber daya di data center on-premise.
- EBS volume dilampirkan ke EC2 instance & merupakan AZ-level resource, sedangkan EFS \a sistem file \u Linux & merupakan Regional resource \shg setiap EC2 instance di region \y sama \dp menggunakannya.

## Amazon Relational Database Service (Amazon RDS)

- Relational database management system (RDBMS): data memiliki relasi \dg bagian data lainnya.
- RDS: layanan \u menjalankan database relasional di AWS Cloud. Mendukung: Amazon Aurora, PostgreSQL, MySQL, MariaDB, Oracle DB, & Microsoft SQL Server.
- Lift-and-Shift: proses memigrasikan beban kerja \dr on-premise ke AWS \dg sedikit / bahkan tanpa modifikasi.
- Layanan Amazon RDS hadir \dg berbagai fitur, termasuk:
  - Automated patching (memperbaiki masalah \dg memperbarui program).
  - Backup (pencadangan).
  - Redundancy (memiliki \lb \dr 1 instance \u berjaga-jaga jika instance utama gagal beroperasi).
  - Failover (instance lain akan mengambil alih saat instance utama mengalami kegagalan).
  - Disaster recovery (memulihkan pascabencana).
  - Encryption at rest (enkripsi data saat disimpan).
  - Encryption in-transit (enkripsi data saat sedang dikirim & diterima).

## Amazon DynamoDB

- Amazon DynamoDB: database non-relasional (NoSQL) & menggunakan key-value storage & juga database serverless.
- Setiap item \t \hr memiliki atribut \y sama.

## Amazon Redshift

- Data warehouse: dirancang \scr spesifik \u jenis big data, yaitu analitik historis, bukan analisis operasional.
- Amazon Redshift: layanan data warehousing \u analitik big data,  mengumpulkan data \dr \byk sumber & membantu memahami hubungan & tren di seluruh data. Juga \dp diskalakan \scr masif.

## AWS Database Migration Service (AWS DMS)

- AWS DMS: \dp memigrasikan database baik relasional, nonrelasional, / tipe penyimpanan data lain ke AWS \dg mudah & aman.
- \dg AWS DMS :
  - Database sumber tetap beroperasi penuh selama proses migrasi.
  - Downtime (waktu henti) diminimalkan \u aplikasi \y bergantung \p database \tsb.
  - Database sumber & target \t \hr bertipe sama (heterogeneous database migration).
- AWS Schema Conversion Tool: \u heterogeneous database migration.
- Amazon DocumentDB: layanan \u menangani manajemen konten, katalog, / pun profil pengguna, layanan database dokumen \y mendukung beban kerja MongoDB.
- Amazon Neptune: layanan graph database \u membuat & menjalankan aplikasi \dg kumpulan data \y sangat terhubung, \spt social networking, recommendation engines, fraud detection (sistem pendeteksi penipuan), & knowledge graph.
- Amazon Managed Blockchain: membuat & mengelola jaringan blockchain \dg framework (kerangka kerja) \y open-source.
- Amazon Managed Blockchain menggunakan desain decentralized ownership.
- Blockchain: sistem ledger (kumpulan catatan riwayat aktivitas) terdistribusi \y memungkinkan \ pihak menjalankan transaksi & berbagi data tanpa otoritas pusat.
- Amazon Quantum Ledger Database (Amazon QLDB): sistem pencatatan \y immutable di mana entri apa pun \t akan pernah \dp dihapus \dr audit, menyediakan log transaksi terpusat, \t \dp diubah, & \dp diverifikasi \scr kriptografi.
- QLDB menggunakan desain centralized ownership. Otoritas pusat nan tepercaya memiliki, mengelola, & membagikan ledger \dg sejumlah pihak tertentu.
- Amazon ElastiCache: menambahkan lapisan cache \p database \y \dp meningkatkan read time (waktu baca) \u permintaan umum, mendukung Redis & Memcached.
- Amazon DynamoDB Accelerator (DAX): native caching layer \y akan meningkatkan waktu read (baca) \u data nonrelasional.

# 6. Keamanan

## Shared Responsibility Model

- Shared responsibility model:
  - AWS mengontrol security **of** the cloud (keamanan \dr cloud).
  - Pelanggan mengontrol security **in** the cloud (keamanan di cloud).
- Tanggung jawab AWS:
  - Physical: berbagai komponen keamanan fisik, \spt gedung, sumber daya listrik, instalasi jaringan, sistem pendingin, penjagaan keamanan, \dll.
  - Network & Hypervisor: AWS memiliki \byk auditor pihak ketiga \y memperhatikan & mengawasi bagaimana infrastruktur AWS dibangun.
- Tanggung jawab pengguna:
  - Operating System: memilih sistem operasi, melakukan patching, \dll.
  - Application
  - Data: \dp diatur agar \dp diakses oleh semua orang, beberapa orang, 1 orang \dg kondisi tertentu, / bahkan benar-benar menguncinya.

## Perizinan & Hak Akses Pengguna

- Root user: pemilik akun AWS, memiliki permission \u mengakses & mengontrol seluruh sumber daya apa pun \dl akun \tsb, \spt menjalankan database, membuat EC2 instance, layanan blockchain, \dll.
- Multi-factor authentication (MFA) \u root user.
- AWS Identity and Access Management (AWS IAM): mengatur hak akses pengguna.
- Fitur-fitur IAM, \spt: IAM users, IAM policies, IAM groups, & IAM roles.
- IAM users: mewakili orang (personal) \y berinteraksi \dg layanan & sumber daya AWS, \scr default belum memiliki permission sama sekali & \hr memberikan permission \scr eksplisit.
- IAM policies: dokumen JSON \y mengizinkan / menolak aktivitas tertentu \thd layanan & sumber daya AWS.
- Berikanlah akses sesuai \dg kebutuhan saat itu saja (principle of least privilege).
- IAM groups: grup/kelompok \y berisi kumpulan \dr user. Anda \dp melampirkan policy ke group \shg semua user \y berada di group \tsb akan memiliki permission \y sama.
- IAM roles: memiliki permission \y \dp mengizinkan tindakan tertentu \y dibutuhkan \scr temporer / sementara.

## AWS Organizations

- AWS Organizations: lokasi sentral \y \dp mengelola beberapa akun AWS, \spt mengelola biaya, kontrol akses, compliance (kepatuhan), keamanan, & berbagi sumber daya \dg seluruh akun-akun AWS.
- Fitur AWS Organizations:
  - Manajemen terpusat.
  - Consolidated billing (Tagihan terkonsolidasi).
  - Pengelompokan hierarki akun: kelompokkan ke \dlm organiztional unit (OU) \y memiliki tujuan serupa. Terapkan policy (kebijakan) ke OU, maka semua akun akan mewarisi permission \dr policy \tsb.
  - Kontrol atas layanan AWS & tindakan API.

## Compliance (Kepatuhan)

- AWS telah memenuhi daftar panjang \dr [program compliance](https://aws.amazon.com/compliance/programs).
- Region \y Anda pilih \dp juga membantu memenuhi regulasi compliance.
- [AWS Artifact](https://aws.amazon.com/id/artifact): layanan akses on-demand ke laporan keamanan & compliance AWS serta online agreements (perjanjian online) tertentu.
- AWS Artifact Agreements: \u menandatangani perjanjian \dg AWS terkait penggunaan jenis informasi tertentu di seluruh layanan.
- AWS Artifact Reports: menyediakan laporan compliance dari auditor pihak ketiga \y menguji & memverifikasi bahwa AWS mematuhi berbagai standar & regulasi keamanan global, regional, & industri.
- Customer Compliance Center: menyediakan informasi \u mempelajari lebih lanjut tentang compliance. Anda \dp membaca beberapa \ct kasus \y berhubungan \dg compliance \dr para pelanggan AWS \u memberikan gambaran bagaimana perusahaan \dl regulated industry (industri teregulasi) menyelesaikan berbagai tantangan compliance, governance/tata kelola, & audit.

## Serangan Denial-of-Service (DoS)

- Serangan DoS: sengaja \u membuat website / aplikasi menjadi \t bekerja \dg optimal bagi pengguna, \spt mengirimkan traffic jaringan \y masif ke aplikasi.
- Distributed denial-of-service (DDoS): serangan DoS \y berasal \dr \byk sumber.
- Tipe-tipe DDoS:
  - UDP flood: Penyerang mengirim permintaan ke penyedia lain \dg alamat penerima yaitu alamat infrastruktur Anda \shg server akan dibanjiri data \dr penyedia \tsb.
  - HTTP level attack: Penyerang terlihat \spt pengguna normal, namun mengirim permintaan secara berulang kali & terus-menerus.
  - Slowloris attack: Penyerang berpura-pura memiliki koneksi \y sangat lambat \shg server \shg \t \dp memproses permintaan pengguna \y lain.
- Solusi UDP flood: menggunakan security group \y akan menolak permintaan jika memang \t ada di \dl daftar \y diizinkan.
- Solusi slowloris attack: menggunakan ELB \u mengarahkan traffic lalu lintas ke EC2 instance. \u bisa membanjiri ELB, Anda harus membanjiri keseluruhan AWS Regions \y secara teoritis akan terlalu mahal bagi siapa pun \y melakukannya.
- AWS Shield: layanan proteksi \dr serangan DDoS.
- AWS Shield Standard: otomatis melindungi sumber daya AWS \dr jenis serangan DDoS \y paling umum tanpa biaya.
- AWS Shield Advanced: layanan berbayar \y menyediakan kemampuan \u mendiagnostik, mendeteksi, & memitigasi serangan DDoS \y canggih.

## Layanan Keamanan Tambahan

- Di AWS, enkripsi hadir \dl 2 varian: at rest (saat diam) & in-transit (\dlm perjalanan).
- Encryption at rest: proses enkripsi saat data \t bergerak. \ct: server-side encryption at rest \u semua data di tabel DynamoDB. Data \y tersimpan akan berubah menjadi serangkaian kata \y \t terbaca.
- Encryption in-transit: proses enkripsi saat data berpindah antar layanan AWS / pun klien. \ct: menggunakan koneksi (secure sockets layer) SSL.
- AWS Key Management Service (AWS KMS): layanan \ u melakukan enkripsi menggunakan cryptographic key (kunci kriptografi).
- Kunci kriptografi: rangkaian angka acak \u mengunci (mengenkripsi) & membuka kunci (mendekripsi) data.
- AWS WAF (web application firewall): melindungi aplikasi web / API \dr eksploitasi web umum menggunakan web access control list (web ACL), \spt gangguan keamanan, pemakaian sumber daya berlebih, atau gangguan ketersediaan.
- Web ACL: daftar alamat IP \y diizinkan / diblokir request-nya.
- Amazon Inspector: meningkatkan keamanan & compliance/kepatuhan aplikasi \dg menjalankan penilaian keamanan secara otomatis.
- Amazon GuardDuty: layanan \y menyediakan deteksi ancaman cerdas \u infrastruktur & sumber daya AWS. Detail ancaman \y ditemukan \dp ditinjau \dr AWS Management Console.

# Pemantauan & Analitik

## Pengantar

- Monitoring / pemantauan: proses mengamati sistem; mengumpulkan metrik; & mengevaluasinya \dr waktu ke waktu \u membuat keputusan / mengambil tindakan.
- Fungsi pemantauan: mengukur performa sistem; memberi peringatan jika ada \y \t beres, bahkan \dp membantu proses debugging.

## Amazon CloudWatch

- CloudWatch: memantau infrastruktur & aplikasi secara real time. Cara kerja: melacak & memantau metrik.
- Metrik: variabel \y terikat \d sumber daya Anda, \spt penggunaan CPU \dr EC2 instance.
- CloudWatch alarm: memberi peringatan jika suatu metrik mencapai batas yang ditentukan, & juga terintegrasi \dg [Amazon SNS](#messaging--queueing).
- CloudWatch dashboard: panel \y mencantumkan metrik hampir \scr real time.
- Keuntungan memakai CloudWatch:
  - Akses ke semua metrik \dr satu lokasi.
  - Visibilitas ke seluruh aplikasi, infrastruktur, & layanan.
  - Mengurangi waktu MTTR & mengurangi TCO.
  - Mengoptimalkan aplikasi & sumber daya operasional.
- MTTR (mean time to resolution): rata-rata waktu \u menyelesaikan suatu masalah.
- TCO (total cost of ownership): biaya kepemilikan.

## AWS CloudTrail

- CloudTrail: layanan audit API \y komprehensif; \dp melihat riwayat lengkap \dr aktivitas pengguna & panggilan API \u aplikasi maupun sumber daya.
- Mesin akan mencatat \dg tepat tentang identitas pemanggil API, waktu panggilan, alamat IP pemanggil, dll.
- CloudTrail Insights: fitur opsional \y memungkinkan CloudTrail \scr otomatis mendeteksi aktivitas API \y mencurigakan di akun AWS Anda.

## AWS Trusted Advisor

- Trusted Advisor: layanan web \y memeriksa lingkungan AWS Anda & memberikan rekomendasi \scr real time sesuai \dg praktik terbaik AWS.
- 3 kategori status:
  - Centang hijau : menunjukkan jumlah item \y terdeteksi tanpa masalah.
  - Segitiga oranye : mewakili jumlah saran \y mungkin perlu Anda investigasi.
  - Lingkaran merah : mengindikasikan jumlah rekomendasi \y perlu Anda tindak lanjuti.
- Trusted Advisor mengevaluasi sumber daya berdasarkan 5 pilar:
  - Cost optimization (pengoptimalan biaya)
    - \ct: RDS instances \y \t dipakai; Beberapa EC2 instance \y jarang digunakan; EBS volume \y \t dimanfaatkan.
    - Solusi: scaling-down instance; menghapus sumber daya yang tidak digunakan.
  - Performance (kinerja).
    - \ct: pengiriman konten \u Amazon CloudFront \y \t teroptimasi.
  - Security (keamanan).
    - \ct: IAM password policy \y lemah \u user; MFA \t diaktifkan \u root user; security group \y mengizinkan akses publik ke EC2 instance.
  - Fault tolerance (toleransi terhadap kesalahan)
    - \ct: EBS volume \y \t memiliki snapshot (backup); EC2 \y \t terdistribusi ke seluruh AZ.
  - Service limits (batas layanan): memberi peringatan saat Anda mendekati / mencapai batas layanan AWS.
    - \ct: limit \dr kepemilikan VPC per Region = 5.

# Harga & Dukungan

## AWS Free Tier

- AWS Free Tier menyediakan 3 jenis penawaran:
  - Always free, \ct: AWS Lambda (1 juta request & 3,2 juta detik waktu komputasi per bulan); Amazon DynamoDB (25 GB penyimpanan per bulan).
  - 12 months free, \ct: Amazon S3 (S3 standard hingga 5 GB); Amazon EC2 (720 jam komputasi per bulan); Amazon CloudFront (50 GB \u transfer data keluar).
  - Trials: lamanya waktu uji coba mungkin berbeda menurut jumlah hari / jumlah penggunaan \dl layanan, \ct: Amazon Inspector (90 hari uji coba); Amazon SNS; Amazon Cognito; dll.

## Konsep Harga AWS

- Pay for what you use: membayar sesuai \dg jumlah sumber daya \y digunakan, \t perlu komitmen jangka panjang.
- Pay less when you reserve: Beberapa layanan menawarkan opsi reservasi \y memberikan diskon signifikan daripada harga instance \dg opsi penagihan On-Demand.
- Pay less with volume-based discounts when you use more: biaya per unit akan semakin rendah jika semakin sering digunakan.
- AWS pricing calculator: membuat estimasi biaya \u kasus penggunaan di AWS.
- Manfaat:
  - Memodelkan arsitektur \y diinginkan sebelum membangunnya.
  - Menelusuri setiap harga sekaligus membuat perhitungan.
  - Menemukan tipe instance \y tersedia beserta persyaratan kontrak \y \dp memenuhi kebutuhan Anda.

## Billing Dashboard

- AWS Billing & Cost Management dashboard: layanan \u melihat informasi penagihan, membayar tagihan AWS, memantau penggunaan, menganalisis, & mengontrol biaya.

## Consolidated Billing

- Consolidated billing: fitur gratis \u mendapatkan 1 tagihan \u semua akun AWS \y ada di organis asi.
- Manfaat lain: \dp mendistribusikan bulk discount pricing (harga diskon massal), Savings Plans, & Reserved Instances di seluruh akun \p organisasi Anda.

## AWS Budget

- AWS Budgets: \u menetapkan anggaran \p berbagai skenario, \spt biaya / penggunaan layanan. Bahkan bisa mengirimkan notifikasi saat penggunaan Anda sudah melebihi \jml batas anggaran.

## AWS Cost Explorer

- Cost Explorer: layanan berbasis konsol \y \dp meninjau & menganalisis \scr visual pengeluaran Anda di AWS.
- Pengeluaran \dp divisualisasikan & dikelompokkan berdasarkan beberapa atribut: layanan, AWS Regions, tipe instance, tag, dll.

## AWS Support Plans

- 4 support plan: basic, developer, bussiness, enterprise.
- AWS Basic Support: setiap pelanggan otomatis mendapatkan paket AWS Basic Support gratis. Fungsi dukungan:
  - Akses 24/7 ke customer service.
  - Dokumentasi.
  - Whitepaper.
  - Forum dukungan.
  - AWS Trusted Advisor.
  - AWS Personal Health Dashboard
- AWS Developer Support. Fitur:
  - Semua fitur \y ada di Basic.
  - Layanan diagnostik \p sisi klien.
  - Panduan praktik terbaik.
  - Dukungan arsitektur dasar \y terdiri \dr panduan penggunaan penawaran, fitur, & layanan AWS.
  - Akses email ke customer support \dg waktu respons 24 jam \u segala pertanyaan.
- AWS Business Support. Fitur:
  - Semua \y ada di Basic & Developer.
  - Seluruh rangkaian pemeriksaan AWS Trusted Advisor.
  - Akses telepon \lsg ke tim dukungan (cloud support engineer) \y memiliki SLA (service level agreement alias jaminan) respons 4 jam jika sistem produksi Anda mengalami gangguan & 1 jam jika sistem Anda down / \t bekerja.
  - Akses ke Infrastructure Event Management \d biaya tambahan. AWS \dp membantu Anda \u merencanakan acara besar, \spt peluncuran produk baru / periklanan global.
  - Panduan kasus penggunaan \u mengidentifikasi penawaran, fitur, & layanan AWS \y paling mendukung kebutuhan spesifik Anda.
  - Dukungan terbatas \u perangkat lunak pihak ketiga, \ct \dl proses instal, konfigurasi, & pemecahan masalah \p sistem operasi pihak ketiga.
- AWS Enterprise Support. Fitur:
  - Semua \y ada di Basic, Developer, & Bussiness.
  - SLA 15 menit.
  - Panduan arsitektur aplikasi: hubungan konsultatif \y \d mendukung kasus penggunaan & aplikasi spesifik Anda.
  - Infrastructure Event Management.
  - Technical Account Manager (TAM) \y akan mengoordinasikan akses ke program & pakar AWS lainnya sesuai kebutuhan. Juga menyediakan infrastructure event management, tinjauan Well-Architected, & reviu operasional.
- Tinjauan Well-Architected: TAM bekerja sama \dg pelanggan \u meninjau arsitektur menggunakan Well-Architected Framework berdasarkan 5 pilar: Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization.

## AWS Marketplace

- AWS Marketplace: katalog digital pilihan \y memiliki ribuan perangkat lunak \dr berbagai vendor.
- Kategori produk AWS marketplace: Infrastructure Software, Business Applications, Data & Analytics, DevOps, dll.

# Singkatan

- \a: adalah
- \byk: banyak
- \ct: contoh
- \dg: dengan
- \dl: dalam
- \dll: dan lain-lain
- \dp: dapat
- \dr: dari
- \hr: harus
- \jml: jumlah
- \lb: lebih
- \lsg: langsung
- \p: pada
- \scr: secara
- \shg: sehingga
- \spt: seperti
- \t: tidak
- \thd: terhadap
- \tsb: tersebut
- \u: untuk
- \y: yang
