import time
import os

# -------------------------------------
#  DATA LOGIN SEDERHANA
# -------------------------------------
akun = {
    "siswa1": "12345",
    "ratna": "abcde"
}

# -------------------------------------
#  DATA MATERI & SOAL
# -------------------------------------
materi = {
    "1": "Bilangan Bulat\nBilangan bulat terdiri dari bilangan positif, nol, dan negatif.",
    "2": "Penjumlahan\nContoh: 5 + 3 = 8",
    "3": "Pengurangan\nContoh: 10 - 4 = 6"
}

soal = [
    {"pertanyaan": "1. Hasil dari 8 + 4 adalah ...", 
     "jawaban": "12"},

    {"pertanyaan": "2. Hasil dari 15 - 5 adalah ...", 
     "jawaban": "10"},

    {"pertanyaan": "3. Bilangan -2 termasuk bilangan ... (bulat/pecahan)", 
     "jawaban": "bulat"}
]

# -------------------------------------
#  CLEAR CONSOLE
# -------------------------------------
def clear():
    os.system('cls' if os.name == 'nt' else 'clear')


# -------------------------------------
#  LOGIN
# -------------------------------------
def login():
    attempts = 3
    while attempts > 0:
        clear()
        print("=" * 38)
        print("            LOGIN SISWA            ")
        print("=" * 38)

        username = input("Username : ")
        password = input("Password : ")

        if username in akun and akun[username] == password:
            print("\nLogin berhasil! Selamat datang,", username)
            time.sleep(1.5)
            return True
        else:
            attempts -= 1
            print(f"\nLogin gagal! Coba lagi ({attempts} percobaan tersisa)")
            time.sleep(1.5)

    print("\nKesempatan habis. Program berhenti.")
    return False


# -------------------------------------
#  MENU UTAMA
# -------------------------------------
def menu():
    while True:
        clear()
        print("=" * 42)
        print("     Aplikasi Pembelajaran Interaktif")
        print("=" * 42)
        print("1. Lihat Materi")
        print("2. Latihan Soal")
        print("3. Tentang Aplikasi")
        print("4. Keluar")
        print("=" * 42)

        pilihan = input("Pilih menu (1-4): ")

        if pilihan in ["1", "2", "3", "4"]:
            return pilihan

        print("\nInput tidak valid! Harus 1-4.")
        time.sleep(1)


# -------------------------------------
#  FITUR MATERI
# -------------------------------------
def tampilkan_materi():
    while True:
        clear()
        print("------ MATERI PEMBELAJARAN ------")
        for key, value in materi.items():
            print(f"{key}. {value.splitlines()[0]}")

        pilih = input("\nPilih materi (1/2/3) atau 0 untuk kembali: ")

        if pilih == "0":
            return

        if pilih in materi:
            clear()
            print(materi[pilih])
            input("\nTekan ENTER untuk kembali...")
        else:
            print("Pilihan tidak ada!")
            time.sleep(1)


# -------------------------------------
#  FITUR LATIHAN SOAL
# -------------------------------------
def latihan_soal():
    clear()
    print("------ LATIHAN SOAL ------")
    skor = 0

    for item in soal:
        print(item["pertanyaan"])
        jawaban = input("Jawab: ")

        if jawaban.strip().lower() == item["jawaban"].lower():
            print("✓ Benar!\n")
            skor += 1
        else:
            print(f"✗ Salah! Jawaban benar: {item['jawaban']}\n")

        time.sleep(1)

    print(f"Skor akhir: {skor} dari {len(soal)} soal.")
    input("\nTekan ENTER untuk kembali...")


# -------------------------------------
#  TENTANG APLIKASI
# -------------------------------------
def tentang():
    clear()
    print("------ TENTANG APLIKASI ------")
    print("Aplikasi ini dibuat untuk membantu siswa belajar\n"
          "melalui materi singkat dan latihan soal interaktif.\n"
          "Dikembangkan menggunakan Python.")
    input("\nTekan ENTER untuk kembali...")


# =====================================
#  PROGRAM UTAMA
# =====================================
if login():  # Berhasil login baru masuk menu
    while True:
        pilihan = menu()

        if pilihan == "1":
            tampilkan_materi()
        elif pilihan == "2":
            latihan_soal()
        elif pilihan == "3":
            tentang()
        elif pilihan == "4":
            print("Terima kasih telah menggunakan aplikasi ini.")
            time.sleep(1)
            break
