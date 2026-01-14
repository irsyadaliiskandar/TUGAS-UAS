START

Buat data EVENT
    "Konser Musik" → harga 150000, stok 100
    "Seminar IT" → harga 50000, stok 50
    "Workshop Coding" → harga 75000, stok 30

Buat list PENJUALAN kosong

PROCEDURE Tampilkan_Event
    Tampilkan "Daftar Event"
    FOR setiap EVENT
        Tampilkan nama event, harga, dan stok
    END FOR
END PROCEDURE

PROCEDURE Beli_Tiket
    Input nama_pembeli
    Input nama_event

    IF nama_event tidak ada di EVENT THEN
        Tampilkan "Event tidak ditemukan"
    ELSE IF stok event = 0 THEN
        Tampilkan "Tiket habis"
    ELSE
        Input jumlah_tiket
        IF jumlah_tiket > stok event THEN
            Tampilkan "Jumlah melebihi stok"
        ELSE
            total ← jumlah_tiket × harga event
            stok event ← stok event − jumlah_tiket
            Simpan data (nama_pembeli, nama_event, jumlah_tiket, total) ke PENJUALAN
            Tampilkan "Pembelian berhasil"
            Tampilkan total bayar
        END IF
    END IF
END PROCEDURE

PROCEDURE Tampilkan_Penjualan
    IF PENJUALAN kosong THEN
        Tampilkan "Belum ada penjualan"
    ELSE
        FOR setiap data di PENJUALAN
            Tampilkan nama pembeli, event, jumlah tiket, total bayar
        END FOR
    END IF
END PROCEDURE

REPEAT
    Tampilkan MENU
        1. Tampilkan Event
        2. Beli Tiket
        3. Tampilkan Penjualan
        4. Keluar
    Input pilihan

    IF pilihan = 1 THEN
        Panggil Tampilkan_Event
    ELSE IF pilihan = 2 THEN
        Panggil Beli_Tiket
    ELSE IF pilihan = 3 THEN
        Panggil Tampilkan_Penjualan
    ELSE IF pilihan = 4 THEN
        Tampilkan "Program selesai"
        STOP
    ELSE
        Tampilkan "Pilihan tidak valid"
    END IF
UNTIL pilihan = 4

END
