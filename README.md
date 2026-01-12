# ERD Sistem

```mermaid
erDiagram
    UNIT_ORGANISASI ||--o{ LOG_TRANSAKSI_LINGKUNGAN : menghasilkan
    UNIT_ORGANISASI ||--o{ INSIDEN_KESELAMATAN : lokasi_kejadian
    UNIT_ORGANISASI ||--o{ FASILITAS_TAILING : memiliki

    TOPIK_MATERIAL ||--o{ DEFINISI_METRIK : mendefinisikan
    DEFINISI_METRIK ||--o{ LOG_KELUHAN : kategori_isu
    DEFINISI_METRIK ||--o{ LOG_TRANSAKSI_LINGKUNGAN : klasifikasi

    PEMANGKU_KEPENTINGAN ||--o{ LOG_KELUHAN : melaporkan
    FAKTOR_EMISI ||--o{ LOG_TRANSAKSI_LINGKUNGAN : konversi

    LOG_TRANSAKSI_LINGKUNGAN {
        bigint ID_Transaksi PK
        date Tanggal
        decimal Nilai
        enum Tipe_Data "Terukur/Estimasi"
        enum Scope "1/2/3"
    }

    INSIDEN_KESELAMATAN {
        int ID_Insiden PK
        datetime Waktu
        enum Klasifikasi "LTI/MTI/NearMiss"
        int Potensi_Konsekuensi
        enum Tipe_Pekerja "Karyawan/Kontraktor"
    }

    LOG_KELUHAN {
        int ID_Keluhan PK
        date Tanggal_Lapor
        enum Status "Open/Closed"
        string Remediasi
    }
