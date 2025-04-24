# Data pengguna dan resep
users = {}
recipes = {}

# Fungsi untuk mendaftar pengguna
def register():
    username = input("Masukkan username: ")
    password = input("Masukkan password: ")
    
    if username in users:
        print("Username sudah terdaftar!")
    else:
        users[username] = password
        recipes[username] = []  # Inisialisasi daftar resep untuk pengguna
        print("Pendaftaran berhasil!")

# Fungsi untuk login pengguna
def login():
    username = input("Masukkan username: ")
    password = input("Masukkan password: ")
    
    if username in users and users[username] == password:
        print("Login berhasil!")
        return username
    else:
        print("Username atau password salah!")
        return None

# Fungsi untuk menambah resep
def add_recipe(username):
    recipe_name = input("Masukkan nama obat: ")
    dosage = input("Masukkan dosis: ")
    frequency = input("Masukkan frekuensi: ")
    
    recipes[username].append({
        'name': recipe_name,
        'dosage': dosage,
        'frequency': frequency
    })
    
    print("Resep berhasil ditambahkan!")

# Fungsi untuk melihat resep
def view_recipes(username):
    if username in recipes and recipes[username]:
        print("Resep untuk", username)
        for i, recipe in enumerate(recipes[username]):
            print(f"{i + 1}. Nama: {recipe['name']}, Dosis: {recipe['dosage']}, Frekuensi: {recipe['frequency']}")
    else:
        print("Tidak ada resep untuk pengguna ini.")

# Fungsi untuk menghapus resep
def delete_recipe(username):
    if username in recipes and recipes[username]:
        view_recipes(username)
        recipe_index = int(input("Masukkan nomor resep yang ingin dihapus: ")) - 1
        
        if 0 <= recipe_index < len(recipes[username]):
            recipes[username].pop(recipe_index)
            print("Resep berhasil dihapus!")
        else:
            print("Nomor resep tidak valid.")
    else:
        print("Tidak ada resep untuk pengguna ini.")

# Fungsi utama
def main():
    while True:
        print("\nMenu:")
        print("1. Daftar")
        print("2. Login")
        print("3. Keluar")
        
        choice = input("Pilih opsi: ")
        
        if choice == '1':
            register()
        elif choice == '2':
            username = login()
            if username:
                while True:
                    print("\nMenu Pengguna:")
                    print("1. Tambah Resep")
                    print("2. Lihat Resep")
                    print("3. Hapus Resep")
                    print("4. Logout")
                    
                    user_choice = input("Pilih opsi: ")
                    
                    if user_choice == '1':
                        add_recipe(username)
                    elif user_choice == '2':
                        view_recipes(username)
                    elif user_choice == '3':
                        delete_recipe(username)
                    elif user_choice == '4':
                        print("Logout berhasil!")
                        break
                    else:
                        print("Opsi tidak valid.")
        elif choice == '3':
            print("Terima kasih! Sampai jumpa.")
            break
        else:
            print("Opsi tidak valid.")

if __name__ == "__main__":
    main()
