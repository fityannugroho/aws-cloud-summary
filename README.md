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
- EC2 berjalan di host (mesin fisik) \d teknologi virtualisasi. 1 host \u banyak instance (virtual machines-VM).
- Tugas hypervisor:
  - membagi sumber daya host \u semua VM.
  - mengisolasi antar VM saat berbagi sumber daya.
- Konfigurasi instance fleksibel: sistem operasi, instalasi software, ukuran (\d vertical scalling--menambah memori/CPU--), jaringan (jenis request, publik/privat).
- Cara kerja EC2:
  - luncurkan, pilih template \d konfigurasi dasar, lalu atur jaringan & keamanan
  - hubungkan, instance \dpt diakses dari desktop, dll.
  - gunakan, install software, tambah storage, menyalin file, dll.

## Tipe Instance EC2

- Setiap tipe instance dikelompokkan dalam satu instance family \u tugas tertentu.
- Instance family:
  - General purpose instances, seimbang antara sumber daya komputasi, memori, & jaringan. Bisa \sbg server apk web / code repo.
  - Compute optimized instances, ideal \u komputasi tinggi \dgn performa prosesor tinggi, \sprt: server game, HPC (high performance computing), / pemodelan ilmiah. Bisa \u beban kerja batch processing.
  - Memory optimized instances, \u beban kerja memproses kumpulan data besar di memori, \sprt relasional & non-relasional / HPC.
  - Accelerated computing instances, \u menjalankan beberapa fungsi \lbh efisien \drpd software \yg berjalan di CPU, \cth kalkulasi floating-point, pemrosesan grafik, & data pattern matching.
  - Storage optimized instance, \u beban kerja membaca (read) & menulis (write) tinggi & berurutan \dr database besar di local storage. Bisa \u sistem file terdistribusi, data warehouse (gudang data), online transaction processing system. Cocok jika butuh input/output operation per second (IOPS) tinggi.

## Harga EC2

- On-demand (sesuai permintaan), membayar selama instance berjalan--bisa per jam atau per detik--.
- Savings Plans (Rencana Tabungan), mengurangi biaya komputasi \d berkomitmen \thdp \jmlh dolar/jam \yg keluar & penggunaan komputasi \yg konsisten \u jangka waktu 1 / 3 tahun.
- Reserved Instances (Instance Terpesan), menawarkan diskon penagihan \yg diterapkan \u instance On-Demand \d berkomitmen \thdp tingkat penggunaan \u jangka waktu 1 / 3 tahun.
- Spot Instances, menggunakan kapasitas komputasi Amazon EC2 \yg tak terpakai & menawarkan penghematan biaya \hg 90% \dr harga On-Demand. Opsi ini sangat ideal \u beban kerja \d waktu mulai & akhir \yg fleksibel & tak masalah \d interupsi.
- Dedicated Hosts (Host Khusus), server fisik \dr kapasitas EC2 instance \yg didedikasikan sepenuhnya \u Anda gunakan.

## Penyesuaian Kapasitas EC2

- Skalabilitas & elastisitas
- Amazon EC2 Auto Scaling, menambah / menghapus Amazon EC2 instances secara otomatis sesuai kebutuhan.
- Dynamic scaling: merespons \thdp perubahan permintaan.
- Predictive scaling: secara otomatis menjadwalkan \jmlh Amazon EC2 instances \yg tepat berdasarkan prediksi permintaan.
- Scaling up: menambahkan lebih banyak daya \pd mesin \yg sedang berjalan.
- Scaling out: menambahkan lebih banyak instance agar \dpt menangani permintaan.

## Elastic Load Balancing (ELB)

- Load balancing: memastikan bahwa distribusi beban kerja merata di seluruh EC2 instance \shg tak ada satu instance pun \yg menganggur.
- Load balancer: bertindak \sbg satu titik kontak untuk semua traffic web \yg masuk ke Auto Scaling group Anda.
- ELB: regional construct (berjalan di tingkat Region), bukan \pd individu EC2 instance \shg membuatnya highly available secara otomatis.
- ELB \dpt bekerja sama \dgn EC2 Auto Scaling \u membantu memastikan aplikasi \yg berjalan di EC2 \dpt memberikan kinerja & ketersediaan tinggi.
- Decoupled architecture (arsitektur \yg terpisah)

## Messaging & Queueing

- Ide \dr menempatkan pesan ke \dlm buffer disebut messaging & queueing.
- Tightly coupled architecture: ketika aplikasi berkomunikasi secara \lsng. Jika ada 1 komponen gagal / berubah, maka akan memicu kegagalan di komponen lain / bahkan seluruh sistem.
- Aplikasi monolitik: desain aplikasi \yg menggabungkan berbagai komponen menjadi satu kesatuan.
- Loosely coupled architecture: jika 1 komponen gagal, maka komponen \tsb akan diisolasi \shg tak akan menyebabkan kegagalan beruntun ke seluruh sistem.
- Aplikasi microservice: komponen dibuat menjadi loosely coupled \shg \dpt dikembangkan, di-deploy (diterapkan), & dikelola secara independen.
- Amazon Simple Queue Service (Amazon SQS) & Amazon Simple Notification Service (Amazon SNS) \u arsitektur \yg loosely coupled.
- SQS: mengirim, menyimpan, & menerima pesan antar komponen software \d volume berapapun tanpa khawatir kehilangan pesan \tsb.
- Data \yg terkandung di \dlm pesan disebut payload & itu dilindungi \hg terkirim.
- SNS: juga digunakan \u mengirimkan pesan ke layanan. Bedanya, ia juga \dpt mengirimkan pemberitahuan ke pelanggan.
- SNS menggunakan model publish/subscribe alias pub/sub.
- SNS topic: membuat suatu saluran \u menyampaikan pesan. Jika ingin mempublikasikan pesan (publish), Anda bisa mengatur pelanggan (subscribers).
- Di SNS, subscribers \dpt berupa server web, alamat email, AWS Lambda function, \ beberapa opsi lainnya.

## Layanan Komputasi Tambahan

- Pengguna EC2 bertanggung jawab \u:
  - patching (memperbaiki masalah \d memperbarui program komputer).
  - menyiapkan scaling.
  - merancang aplikasi \u dijalankan agar high available.
- Serverless: pengguna \tdk \dpt melihat & mengakses infrastruktur dasar \yg menjalankan aplikasi. Semua pengelolaan lingkungan \yg mendasari penyediaan, scaling, high availability, & pemeliharaan sudah ditangani \shg pengguna bisa fokus \pd aplikasi \yg akan dijalankan.
- AWS lambda: layanan serverless AWS.
- AWS Lambda dirancang \u menjalankan kode di bawah 15 menit \shg tdk cocok \u proses \yg berjalan lama \sprt deep learning.
- Container: \u efisiensi & portabilitas.
-  Amazon Elastic Container Service (Amazon ECS) & Amazon Elastic Kubernetes Service (Amazon EKS). Keduanya adalah container orchestration.
- Container menyediakan cara \u mengemas kode, konfigurasi, & dependensi aplikasi ke dalam satu objek.
- Container bekerja di atas EC2 instance & berjalan secara terpisah satu sama lain. Cara kerja container serupa \dgn mesin virtual, namun \dlm kasus ini, host-nya (server) adalah EC2 instance.
- ECS & EKS berjalan di atas EC- Jika tak ingin sibuk mengurusi EC2, gunakan AWS Fargate.
- AWS Fargate: platform komputasi serverless \u ECS & EKS.

# 3. Infrastruktur Global & Keandalan

## Pengantar

- High availability: kemampuan \u memastikan bahwa sistem selalu bekerja & \dpt diakses \d waktu henti \yg minimal tanpa memerlukan intervensi manusia.
- Fault tolerance: sistem masih mampu beroperasi meskipun beberapa komponen mengalami kegagalan.

## Infrastruktur Global AWS

- AWS Regions memiliki beberapa data center \yg berisi semua sumber daya \yg dibutuhkan \sprt komputasi, penyimpanan, jaringan, dll.
- Setiap Region terkoneksi \dgn region lain melalui high speed fiber network, & juga terisolasi \dr region lain kecuali Anda memberinya izin.
- 4 faktor bisnis \yg menentukan pemilihan suatu Region:
  - Compliance (kepatuhan): mengikuti standar \yg ditetapkan pemerintah.
  - Proximity (Kedekatan): latensi (waktu \u mengirim & menerima data) bisa semakin kecil & pengiriman konten ke pelanggan jadi lebih cepat.
  - Feature Availability (Ketersediaan Fitur): Region terdekat mungkin \tdk memiliki semua fitur AWS dibutuhkan.
  - Pricing (Harga): beberapa lokasi bisa lebih mahal pengoperasiannya.
- Availability Zone (AZ): 1 atau sekelompok data center \dlm 1 region.
- Setiap Regions terdiri dari beberapa AZ \yg terisolasi & secara fisik terpisah di dalam Region geografis.
- EC2 menjalankan VM \pd hardware \yg ada di AZ. Best practice-nya, jalankan setidaknya 2 AZ \dlm 1 Region.

## Edge Locations

- Content Delivery Network (CDN): teknik menyimpan salinandata di cache \dgn lokasi \yg \lbh dekat \d pelanggan.
- Amazon CloudFront: layanan CDN \u mengirim data ke seluruh dunia \d latensi rendah & kecepatan transfer \yg tinggi.
- Edge locations: lokasi \yg digunakan CloudFront \u menyimpan salinan cache. Edge locations terpisah dari Regions.
- Amazon Route 53: layanan domain name system (DNS) menggunakan edge locations.
-  AWS Outposts: menginstal Region mini \yg beroperasi penuh, tepat di \dlm data center Anda sendiri.

## Menyediakan Sumber Daya AWS

- Di AWS semua aktivitas adalah panggilan API.
- AWS Management Console: antarmuka berbasis browser \yg \dpt digunakan \u mengakses & mengelola layanan AWS. Fungsi:
  - mencari layanan AWS \dr nama, kata kunci, / akronim.
  - membangun lingkungan pengujian.
  - melihat tagihan AWS.
  - melakukan pemantauan.
  - bekerja \d sumber daya non-teknis lainnya.
- AWS Command Line Interface (CLI): mengendalikan layanan AWS \d baris perintah melalui satu alat, juga \dpt menjalankan skrip \tsb secara otomatis.
- AWS Software Development Kit (SDK): \u berinteraksi \d sumber daya AWS melalui berbagai bahasa pemrograman, & memudahkan developer \u membuat program di AWS tanpa menggunakan low-level API.
- Low-level API: memungkinkan Anda \u memanipulasi fungsi di \dlm API secara terperinci sesuai \d kebutuhan.
- high-level API: memberikan lebih banyak fungsi \dlm 1 perintah & lebih mudah digunakan.
- AWS Elastic Beanstalk: membantu menyediakan lingkungan berbasis Amazon EC- Cukup unggah kode & tentukan konfigurasi \yg diinginkan, maka pembangunan lingkungan \sprt penyesuaian kapasitas, load balancing, auto-scaling, & pemantauan kesehatan aplikasi akan otomatis dikerjakan.
- AWS CloudFormation: layanan infrastructure as code (IaaS, infrastruktur sebagai kode) \u menentukan berbagai sumber daya AWS \d cara deklaratif menggunakan CloudFormation template (dokumen berbasis JSON / YAML).
- CloudFormation template\dpt dijalankan di beberapa akun / region.

# 4. Jaringan

## Pengantar

- Amazon Virtual Private Cloud (VPC): \u menyediakan bagian logis \dr AWS Cloud \yg terisolasi & meluncurkan sumber daya \sprt EC2 instance & ELB di dalamnya.
- Sumber daya \tsb \dpt menjadi public-facing \yg berarti memiliki akses ke internet \ pun private alias tanpa akses internet.

## Konektivitas ke AWS

- Subnet: bagian \dr VPC \yg \dpt mengelompokkan sumber daya. Subnet bersama dgn aturan jaringan \dpt mengontrol apakah sumber daya tersedia \u publik / privat.
- Internet Gateway (IGW): \u mengizinkan traffic \dr internet publik mengalir masuk & keluar dr VPC.
- Virtual Private Gateway (VPG): komponen \yg memungkinkan traffic internet \yg terlindungi masuk ke dalam VPC, hanya mengizinkan masuk suatu permintaan jika berasal \dr jaringan \yg disetujui, bukan internet publik.
- VPN bersifat pribadi & dienkripsi, tetapi ia masih menggunakan koneksi internet reguler \d bandwidth (\jmlh maksimum data \yg \dpt dikirim) \yg terbagi ke banyak pengguna internet lainnya.
- AWS Direct Connect: menyediakan koneksi privat, koneksi terdedikasi, \jmlh latensi \yg rendah, & tingkat keamanan \yg tinggi.

## Subnet & Network Access Control List (ACL)

- Subnet: bagian \dr VPC \u mengelompokkan sumber daya berdasarkan keamanan / kebutuhan operasional, bisa publik / privat.
- Subnet \dpt berkomunikasi satu sama lain.
- Network ACL: firewall virtual \yg mengontrol traffic masuk & keluar (memeriksa izin paket data) di tingkat **subnet**. Anggap \sbg petugas pengawas paspor.
- Setiap akun AWS menyertakan network ACL secara default (mengizinkan semua traffic masuk & keluar). Bisa diatur agar menolak semua traffic masuk & keluar \hg Anda secara eksplisit mengizinkannya.
- Security group: firewall virtual \yg mengontrol traffic masuk & keluar \u **EC2 instance**.
- Secara default, security group menolak semua traffic masuk namun mengizinkan semua traffic keluar \dr instance.
-  Anggap seperti penjaga pintu di gedung apartemen.
-  Security group bersifat stateful (\dpt mengingat siapa \yg diizinkan masuk / keluar), network ACL bersifat stateless (\tdk mengingat apa pun).

## Jaringan Global

- DNS: menerjemahkan nama domain ke alamat IP (Internet Protocol) \yg \dpt dibaca komputer.
- Amazon Route 53: layanan DNS \yg highly available (sangat tersedia) & scalable (\dpt diskalakan).
- Route 53 juga \dpt mengarahkan traffic ke endpoints (titik akhir) \yg berbeda menggunakan beberapa routing policies, \sprt Geolocation DNS.
- Geolocation DNS: mengarahkan traffic berdasarkan lokasi pelanggan.

# 5. Penyimpanan & Database

## Instance Store & Amazon Elastic Block Store (EBS)

- Block-level storage (penyimpanan tingkat blok) \u menyimpan data dalam bentuk blok. Anggap \sbg tempat menyimpan file.
- File: serangkaian byte \yg disimpan di \dlm blok \pd disk.
- Instance store: penyimpanan block-level storage sementara \u EC2 instance.
- Jika EC2 instance berhenti, maka semua data di dalamnya akan terhapus.
- EC2 instance adalah mesin virtual. Oleh \krn itu, host \yg mendasarinya \dpt berubah \pd saat instance berhenti & memulai.
- Instance store digunakan \u penyimpanan data \yg sering berubah, \sprt cache, temp file, dll.
- Amazon Elastic Block Store (EBS): menyediakan block-level storage \yg \dpt digunakan bersama \d EC2 instance.
- EBS memungkinkan Anda \u membuat hard drive virtual (EBS volume) lalu memasangnya ke EC2 instance. Ia pun \tdk terikat \lngsng ke host.
- Amazon EBS snapshot: mem-backup data secara incremental dari EBS  volume.
- Incremental backup: hanya mencadangkan data \yg berubah (delta) dari pencadangan sebelumnya.


## Amazon Simple Storage Service (S3)

- S3: layanan \u menyimpan & mengambil data \dlm bentuk onjek \d \jmlh tak terbatas. Objek \tsb disimpan \dlm bucket. Bucket \dpt diatur hak aksesnya.
- Setiap objek terdiri dari data, metadata, & kunci. Setiap objek maks. berukuran 5 TB.
- Metadata: informasi mengenai data, cara penggunaan, ukurannya, dll.
- Kunci (key): identifier/pengenal \yg unik.
- S3 juga ada fitur versioning.
- Saat mengubah file di object-level storage, maka seluruh objek akan diperbarui.
- S3 storage class:
  - S3 standard: objek \yg disimpan akan memiliki 99,999999999% probabilitas tetap utuh \stlh jangka waktu 1 tahun. Data disimpan minimal di 3 AZ.
  - S3 Standard-Infrequent Access (S3 Standard-IA): digunakan \u data \yg jarang diakses tapi membutuhkan proses cepat saat dibutuhkan. \cth \u menyimpan backup.
  - S3 One Zone-Infrequent Access (S3 One Zone-IA): Data disimpan hanya di 1 AZ.
  - S3 Intelligent-Tiering: S3 memantau pola akses objek. Jika objek \tdk diakses selama 30 hari berturut-turut, S3 akan otomatis memindahkannya dari S3 Standard ke S3 Standard-IA. Jika objek kembali diakses, maka S3 akan otomatis mengembalikannya ke S3 standard.
  - S3 Glacier: ideal \u data audit. Mengaksesnya perlu waktu beberapa menit hingga jam.
  - S3 Glacier Deep Archive: memiliki biaya terendah & ideal untuk pengarsipan. Mengaksesnya perlu waktu 12 hingga 48 jam.
- S3 Lifecycle policies: kebijakan \u memindahkan data secara otomatis antar storage class (kelas penyimpanan).
- Jika Anda memiliki objek / file \yg lengkap & hanya membutuhkan sesekali perubahan, maka pilihlah S- Namun, jika Anda membutuhkan proses read (baca) data \yg kompleks, maka pilihlah EBS.

## Amazon Elastic File System (Amazon EFS)

- File server menggunakan block storage \d local file system \u mengatur file. Client \dpt mengakses data di dalamnya melalui file path.
- File storage sangat ideal \u kasus penggunaan di mana data perlu diakses pada waktu \yg sama oleh banyak layanan / sumber daya.
- Amazon EFS: sistem file terkelola \yg bisa diskalakan & \dpt digunakan oleh layanan AWS Cloud & sumber daya di data center on-premise.
- EBS volume dilampirkan ke EC2 instance & merupakan AZ-level resource, sedangkan EFS adalah sistem file \u Linux & merupakan Regional resource \shg setiap EC2 instance di region \yg sama \dpt menggunakannya.

## Amazon Relational Database Service (Amazon RDS)

- Relational database management system (RDBMS): data memiliki relasi \d bagian data lainnya.
- RDS: layanan \u menjalankan database relasional di AWS Cloud. Mendukung: Amazon Aurora, PostgreSQL, MySQL, MariaDB, Oracle DB, & Microsoft SQL Server.
- Lift-and-Shift: proses memigrasikan beban kerja \dr on-premise ke AWS \d sedikit / bahkan tanpa modifikasi.
- Layanan Amazon RDS hadir \d berbagai fitur, termasuk:
  - Automated patching (memperbaiki masalah \d memperbarui program).
  - Backup (pencadangan).
  - Redundancy (memiliki lebih \dr 1 instance \u berjaga-jaga jika instance utama gagal beroperasi).
  - Failover (instance lain akan mengambil alih saat instance utama mengalami kegagalan).
  - Disaster recovery (memulihkan pascabencana).
  - Encryption at rest (enkripsi data saat disimpan).
  - Encryption in-transit (enkripsi data saat sedang dikirim & diterima).

## Amazon DynamoDB

- Amazon DynamoDB: database non-relasional (NoSQL) & menggunakan key-value storage & juga database serverless.
- Setiap item \tdk hrs memiliki atribut \yg sama.

## Amazon Redshift

- Data warehouse: dirancang secara spesifik \u jenis big data, yaitu analitik historis, bukan analisis operasional.
- Amazon Redshift: layanan data warehousing \u analitik big data,  mengumpulkan data \dr banyak sumber & membantu memahami hubungan & tren di seluruh data. Juga \dpt diskalakan secara masif.

## AWS Database Migration Service (AWS DMS)

- AWS DMS: \dpt memigrasikan database baik relasional, nonrelasional, / tipe penyimpanan data lain ke AWS \d mudah & aman.
- \d AWS DMS :
  - Database sumber tetap beroperasi penuh selama proses migrasi.
  - Downtime (waktu henti) diminimalkan \u aplikasi \yg bergantung \pd database \tsb.
  - Database sumber & target \tdk harus bertipe sama (heterogeneous database migration).
- AWS Schema Conversion Tool: \u heterogeneous database migration.
- Amazon DocumentDB: layanan \u menangani manajemen konten, katalog, / pun profil pengguna, layanan database dokumen \yg mendukung beban kerja MongoDB.
- Amazon Neptune: layanan graph database \u membuat & menjalankan aplikasi \dgn kumpulan data \yg sangat terhubung, \sprt social networking, recommendation engines, fraud detection (sistem pendeteksi penipuan), & knowledge graph.
- Amazon Managed Blockchain: membuat & mengelola jaringan blockchain \d framework (kerangka kerja) \yg open-source.
- Amazon Managed Blockchain menggunakan desain decentralized ownership.
- Blockchain: sistem ledger (kumpulan catatan riwayat aktivitas) terdistribusi \yg memungkinkan banyak pihak menjalankan transaksi & berbagi data tanpa otoritas pusat.
- Amazon Quantum Ledger Database (Amazon QLDB): sistem pencatatan \yg immutable di mana entri apa pun \tdk akan pernah bisa dihapus \dr audit, menyediakan log transaksi terpusat, \tdk \dpt diubah, & \dpt diverifikasi secara kriptografi.
- QLDB menggunakan desain centralized ownership. Otoritas pusat nan tepercaya memiliki, mengelola, & membagikan ledger \d sejumlah pihak tertentu.
- Amazon ElastiCache: menambahkan lapisan cache \pd database \yg \dpt meningkatkan read time (waktu baca) \u permintaan umum, mendukung Redis & Memcached.
- Amazon DynamoDB Accelerator (DAX): native caching layer \yg akan meningkatkan waktu read (baca) \u data nonrelasional.

# 6. Keamanan

## Shared Responsibility Model

- Shared responsibility model:
  - AWS mengontrol security **of** the cloud (keamanan dari cloud).
  - Pelanggan mengontrol security **in** the cloud (keamanan di cloud).
- Tanggung jawab AWS:
  - Physical: berbagai komponen keamanan fisik, \sprt gedung, sumber daya listrik, instalasi jaringan, sistem pendingin, penjagaan keamanan, dll.
  - Network & Hypervisor: AWS memiliki banyak auditor pihak ketiga \yg memperhatikan & mengawasi bagaimana infrastruktur AWS dibangun.
- Tanggung jawab pengguna:
  - Operating System: memilih sistem operasi, melakukan patching, dll.
  - Application
  - Data: Anda bisa membuat data \dpt diakses oleh semua orang, beberapa orang, 1 orang \d kondisi tertentu, / bahkan benar-benar menguncinya.

## Perizinan & Hak Akses Pengguna

- Root user: pemilik akun AWS, memiliki permission \u mengakses & mengontrol seluruh sumber daya apa pun \dlm akun \tsb, \sprt menjalankan database, membuat EC2 instance, layanan blockchain, dll.
- Multi-factor authentication (MFA) \u root user.
- AWS Identity and Access Management (AWS IAM): mengatur hak akses pengguna.
- Fitur-fitur IAM, \sprt: IAM users, IAM policies, IAM groups, & IAM roles.
- IAM users: mewakili orang (personal) \yg berinteraksi \d layanan & sumber daya AWS, secara default \blm memiliki permission sama sekali & \hrs memberikan permission secara eksplisit.
- IAM policies: dokumen JSON \yg mengizinkan / menolak aktivitas tertentu \thdp layanan & sumber daya AWS.
- Berikanlah akses sesuai \d kebutuhan saat itu saja (principle of least privilege).
- IAM groups: grup/kelompok \yg berisi kumpulan \dr user. Anda bisa melampirkan policy ke group \shg semua user \yg berada di group \tsb akan memiliki permission \yg sama.
- IAM roles: memiliki permission \yg \dpt mengizinkan tindakan tertentu \yg dibutuhkan secara temporer / sementara.

## AWS Organizations

- AWS Organizations: lokasi sentral \yg \dpt mengelola beberapa akun AWS, \sprt mengelola biaya, kontrol akses, compliance (kepatuhan), keamanan, & berbagi sumber daya \d seluruh akun-akun AWS.
- Fitur AWS Organizations:
  - Manajemen terpusat
  - Consolidated billing (Tagihan terkonsolidasi)
  - Pengelompokan hierarki akun
  - Kontrol atas layanan AWS & tindakan API
