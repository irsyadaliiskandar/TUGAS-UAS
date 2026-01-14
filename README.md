# TUGAS-UAS

# code

# Sistem Manajemen Penjualan Tiket Event

event = {
    "Konser Musik": {"harga": 150000, "stok": 100},
    "Seminar IT": {"harga": 50000, "stok": 50},
    "Workshop Coding": {"harga": 75000, "stok": 30}
}

penjualan = []

def tampilkan_event():
    print("\nDaftar Event:")
    for nama, data in event.items():
        print(f"- {nama} | Harga: Rp{data['harga']} | Stok: {data['stok']}")

def beli_tiket():
    nama_pembeli = input("Nama Pembeli: ")
    nama_event = input("Nama Event: ")

    if nama_event not in event:
        print("Event tidak ditemukan.")
    elif event[nama_event]["stok"] <= 0:
        print("Tiket habis.")
    else:
        jumlah = int(input("Jumlah tiket: "))
        if jumlah > event[nama_event]["stok"]:
            print("Jumlah melebihi stok.")
        else:
            total = jumlah * event[nama_event]["harga"]
            event[nama_event]["stok"] -= jumlah
            penjualan.append({
                "pembeli": nama_pembeli,
                "event": nama_event,
                "jumlah": jumlah,
                "total": total
            })
            print("Pembelian berhasil.")
            print("Total bayar: Rp", total)

def tampilkan_penjualan():
    if not penjualan:
        print("Belum ada penjualan.")
    else:
        print("\nData Penjualan Tiket:")
        for data in penjualan:
            print(f"- {data['pembeli']} membeli {data['jumlah']} tiket {data['event']} | Rp{data['total']}")

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
