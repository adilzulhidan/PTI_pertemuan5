# Program Data Mahasiswa
# I.S.: User memasukkan banyak data mahasiswa dan array mahasiswa
# F.S.: Menampilkan daftar Nilai mahasiswa

# Kamus global
MaksMhs = 50
Nim = [""] * MaksMhs
Nama = [""] * MaksMhs
Nilai = [0] * MaksMhs
Indeks = [""] * MaksMhs
BanyakData = 0
DataAkhir = 0
SisaData = MaksMhs

def isi_data_mhs():
    global BanyakData, DataAkhir, SisaData
    if SisaData != 0:
        BanyakData = int(input("Banyaknya Data Mahasiswa: "))
        while BanyakData < 1 or BanyakData > MaksMhs:
            print(f"Banyaknya Data Harus dari 1 sampai {MaksMhs}, Ulangi!")
            BanyakData = int(input("Banyaknya Data Mahasiswa: "))

        if BanyakData <= SisaData:
            for i in range(BanyakData):
                print(f"Data Mahasiswa Ke-{i + DataAkhir + 1}")
                Nim[i + DataAkhir] = input("Nim: ")
                Nama[i + DataAkhir] = input("Nama Mahasiswa: ")
                Nilai[i + DataAkhir] = int(input("Nilai: "))
                while Nilai[i + DataAkhir] < 0 or Nilai[i + DataAkhir] > 100:
                    print("Nilai Harus dari 0-100, Ulangi!")
                    Nilai[i + DataAkhir] = int(input("Nilai: "))

            DataAkhir += BanyakData
            SisaData = MaksMhs - DataAkhir
        else:
            print(f"Kuota data tersisa: {SisaData} slot, ulangi.")
    else:
        print("Sisa data habis.")

def indeks_nilai(nilai):
    if 80 <= nilai <= 100:
        return 'A'
    elif 70 <= nilai <= 79:
        return 'B'
    elif 60 <= nilai <= 69:
        return 'C'
    elif 50 <= nilai <= 59:
        return 'D'
    else:
        return 'E'

def nilai_tertinggi():
    return max(Nilai[:DataAkhir])

def nilai_terendah():
    return min(Nilai[:DataAkhir])

def rata_rata():
    return sum(Nilai[:DataAkhir]) / DataAkhir

def daftar_nilai():
    maks_nilai = nilai_tertinggi()
    min_nilai = nilai_terendah()
    rata = rata_rata()

    print("               DAFTAR Nilai MAHASISWA              ")
    print("---------------------------------------------------")
    print("| No |   Nim   |  Nama Mahasiswa | Indeks | Nilai |")
    print("---------------------------------------------------")
    
    for i in range(DataAkhir):
        Indeks[i] = indeks_nilai(Nilai[i])
        print(f"| {i+1:2} | {Nim[i]:7} | {Nama[i]:15} | {Indeks[i]}     | {Nilai[i]:5} |")
    
    print("---------------------------------------------------")
    print(f"Nilai Tertinggi                 : {maks_nilai}")
    print(f"Nilai Terendah                  : {min_nilai}")
    print(f"Nilai Rata-rata                 : {rata:.1f}")
    print(f"Sisa Data yang Dapat Dimasukkan : {SisaData}")

def menu_pilihan():
    print("MENU PILIHAN")
    print("************")
    print("1. Tambah Data Nilai Mahasiswa")
    print("2. Tampil Daftar Nilai Mahasiswa")
    print("0. Keluar")
    pilihan = int(input("Pilihan menu? : "))
    
    while pilihan < 0 or pilihan > 2:
        print("Pilih Menu harus antara 0 - 2, ulangi!")
        pilihan = int(input("Pilihan menu? : "))
    return pilihan

# Badan program utama
Nilai = []  # Inisialisasi list kosong untuk menyimpan nilai mahasiswa
BanyakData = 0  # Inisialisasi jumlah data awal

def menu_pilihan():
    print("\nMenu:")
    print("1. Isi Data Mahasiswa Baru")
    print("2. Tambah Nilai Mahasiswa")
    print("3. Daftar Nilai")
    print("0. Keluar")
    return int(input("Pilih menu: "))

def isi_data_mhs():
    global BanyakData  # Agar bisa mengubah nilai BanyakData
    jumlah_mahasiswa = int(input("Masukkan jumlah mahasiswa: "))
    for i in range(jumlah_mahasiswa):
        while True:
            try:
                nilai = int(input(f"Masukkan nilai untuk mahasiswa {BanyakData + i + 1}: "))
                Nilai.append(nilai)  # Menambahkan nilai ke list
                break
            except ValueError:
                print("Nilai harus berupa angka. Coba lagi.")
    BanyakData += jumlah_mahasiswa  # Perbarui jumlah total mahasiswa

def tambah_nilai_mhs():
    global BanyakData
    if BanyakData == 0:
        print("Data masih kosong. Isi data terlebih dahulu.")
    else:
        jumlah_tambah = int(input("Masukkan jumlah mahasiswa yang ingin ditambahkan nilainya: "))
        for i in range(jumlah_tambah):
            while True:
                try:
                    nilai = int(input(f"Masukkan nilai untuk mahasiswa {BanyakData + i + 1}: "))
                    Nilai.append(nilai)  # Menambahkan nilai baru ke list
                    break
                except ValueError:
                    print("Nilai harus berupa angka. Coba lagi.")
        BanyakData += jumlah_tambah  # Perbarui jumlah total mahasiswa

def daftar_nilai():
    if BanyakData == 0:
        print("Belum ada data mahasiswa.")
    else:
        print("Daftar Nilai Mahasiswa:")
        for i, nilai in enumerate(Nilai, start=1):
            print(f"Mahasiswa {i}: {nilai}")

while True:
    pilihan = menu_pilihan()
    
    if pilihan == 1:
        isi_data_mhs()  # Mengisi data mahasiswa baru
    elif pilihan == 2:
        tambah_nilai_mhs()  # Menambahkan nilai mahasiswa baru
    elif pilihan == 3:
        daftar_nilai()  # Menampilkan daftar nilai
    elif pilihan == 0:
        print("Keluar dari program.")
        break
    else:
        print("Pilihan tidak valid. Silakan pilih kembali.")

   
