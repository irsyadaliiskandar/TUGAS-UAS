# Sistem Manajemen Penjualan Tiket Event

```
# Sistem Manajemen Penjualan Tiket Event
event = {
    "E01": {"nama": "Konser Musik", "harga": 150000, "stok": 100},
    "E02": {"nama": "Seminar IT", "harga": 50000, "stok": 50},
    "E03": {"nama": "Workshop Coding", "harga": 75000, "stok": 30},
    "E04": {"nama": "Festival Musik", "harga": 200000, "stok": 20},
    "E05": {"nama": "Seminar Bisnis", "harga": 60000, "stok": 40},
    "E06": {"nama": "Workshop Desain Grafis", "harga": 80000, "stok": 25},
    "E07": {"nama": "Festival Kuliner", "harga": 180000, "stok": 15},
    "E08": {"nama": "Seminar Manajemen Proyek", "harga": 70000, "stok": 35},
    "E09": {"nama": "Workshop Fotografi", "harga": 90000, "stok": 20},
}

penjualan = []

def format_rp(harga):
    return f"{harga:,}".replace(",", ".")

def tampilkan_event():
    print("\nDaftar Event:")
    print("="*60)
    print(f"| {'Kode':^5} | {'Nama Event':^25} | {'Harga':^10} | {'Stok':^5} |")
    print("="*60)
    for kode, data in event.items():
        print(f"| {kode:^5} | {data['nama']:<25} | Rp{format_rp(data['harga']):<8} | {data['stok']:^5} |")
    print("="*60)

def cetak_struk(data_pembelian):
    print("\n=== STRUK PEMBELIAN TIKET ===")
    print(f"Nama Pembeli   : {data_pembelian['pembeli']}")
    print(f"Event          : {data_pembelian['event_nama']}")
    print(f"Jumlah Tiket   : {data_pembelian['jumlah']}")
    print(f"Harga per Tiket: Rp{format_rp(data_pembelian['harga_per_tiket'])}")
    print(f"Total Bayar    : Rp{format_rp(data_pembelian['total'])}")
    print("=============================\n")

def beli_tiket():
    nama_pembeli = input("Nama Pembeli: ")
    kode_event = input("Kode Event: ").upper()

    if kode_event not in event:
        print("Kode event tidak ditemukan.")
        return
    elif event[kode_event]["stok"] <= 0:
        print("Tiket habis.")
        return

    # Masukkan jumlah awal
    while True:
        try:
            jumlah = int(input("Jumlah tiket: "))
            if jumlah < 1:
                print("Harap membeli minimal 1 tiket.")
            elif jumlah > event[kode_event]["stok"]:
                print(f"Jumlah melebihi stok ({event[kode_event]['stok']} tiket tersisa).")
            else:
                break
        except ValueError:
            print("Masukkan angka valid.")

    # Menu tambah/kurang sebelum struk
    while True:
        print(f"\nJumlah tiket saat ini: {jumlah}")
        print("1. Tambah tiket")
        print("2. Kurangi tiket")
        print("3. Lanjut ke struk")
        opsi = input("Pilih opsi: ")

        if opsi == "1":
            tambah = int(input("Masukkan jumlah tiket tambahan: "))
            if tambah < 1:
                print("Minimal tambah 1 tiket.")
            elif jumlah + tambah > event[kode_event]["stok"]:
                print(f"Tidak cukup stok. Maksimal sisa {event[kode_event]['stok'] - jumlah} tiket.")
            else:
                jumlah += tambah
                print(f"Jumlah tiket sekarang: {jumlah}")
        elif opsi == "2":
            kurang = int(input("Masukkan jumlah tiket dikurangi: "))
            if kurang < 1:
                print("Minimal kurangi 1 tiket.")
            elif jumlah - kurang < 1:
                print("Jumlah tiket minimal 1.")
            else:
                jumlah -= kurang
                print(f"Jumlah tiket sekarang: {jumlah}")
        elif opsi == "3":
            break
        else:
            print("Opsi tidak valid.")

    total = jumlah * event[kode_event]["harga"]
    event[kode_event]["stok"] -= jumlah

    data_pembelian = {
        "pembeli": nama_pembeli,
        "event_nama": event[kode_event]["nama"],
        "jumlah": jumlah,
        "harga_per_tiket": event[kode_event]["harga"],
        "total": total
    }

    penjualan.append(data_pembelian)
    print("Pembelian berhasil.")
    cetak_struk(data_pembelian)

def tampilkan_penjualan():
    if not penjualan:
        print("Belum ada penjualan.")
    else:
        print("\nData Penjualan Tiket:")
        print("="*70)
        print(f"| {'Nama Pembeli':^20} | {'Event':^25} | {'Jumlah':^6} | {'Total':^10} |")
        print("="*70)
        for data in penjualan:
            print(f"| {data['pembeli']:<20} | {data['event_nama']:<25} | {data['jumlah']:^6} | Rp{format_rp(data['total']):<8} |")
        print("="*70)

# Menu utama
while True:
    print("\n=== SISTEM PENJUALAN TIKET EVENT ===")
    print("1. Tampilkan Event")
    print("2. Beli Tiket")
    print("3. Tampilkan Penjualan")
    print("4. Keluar")

    pilihan = input("Pilih menu: ")

    if pilihan == "1":
        tampilkan_event()
    elif pilihan == "2":
        beli_tiket()
    elif pilihan == "3":
        tampilkan_penjualan()
    elif pilihan == "4":
        print("Program selesai.")
        break
    else:
        print("Pilihan tidak valid.")
        print("Pilihan tidak valid.")
```
