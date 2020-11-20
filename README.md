# Projek-10-Komputer-1
from os import system
from datetime import datetime

def view_menu():
	system("cls")
	menu = """
VENDING MACHINE KANTIN SEKOLAH
[A] - PERLIHATKAN MENU
[B] - CARI NAMA PRODUK
[C] - PERBARUI INFO PRODUK LAMA
[D] - TAMBAH INFO PRODUK BARU
[E] - HAPUS INFO PRODUK LAMA
[F] - LAPORKAN MASALAH TEKNIS
[G] - KELUAR
	"""
	print(menu)

def verify_ans(char):
	char = char.upper()
	if char == "Y":
		return True
	else:
		return False

def print_header(msg):
	system("cls")
	print(msg)

def create_id_product():
	today = datetime.now()
	year = today.year
	month = today.month
	hari = today.day
	counter = len(data_menu)+1
	id_product = str("%4d%02d%02d-C%03d" % (year, month, hari, counter))
	return id_product

def print_data_menu(id_product = None, all_fields = False, kadaluwarsa = True):
	if id_product != None and all_fields == False:
		print(f"""
		-DATA DITEMUKAN-
	ID \t: {id_product}
	Merek \t: {data_menu[id_product]["merek"]}
	Rasa \t: {data_menu[id_product]["rasa"]}
	Kadaluwarsa : {data_menu[id_product]["kadaluwarsa"]}
			""")
	elif id_product != None and kadaluwarsa == False:
		print(f"""
		-DATA DITEMUKAN-
	ID \t: {id_product}
	Merek \t: {data_menu[id_product]["merek"]}
	Rasa \t: {data_menu[id_product]["rasa"]}
			""")
	elif all_fields == True:
		for id_product in data_menu:
			merek = data_menu[id_product]["merek"]
			rasa = data_menu[id_product]["rasa"]
			kadaluwarsa = data_menu[id_product]["kadaluwarsa"]
			print(f"ID: {id_product}\tMerek: {merek}\tRasa: {rasa}\tKadaluwarsa: {kadaluwarsa}")

def add_to_menu():
	print_header("-MEMASUKKAN DAFTAR MENU BARU-")
	merek = input("MEREK\t: ")
	rasa = input("RASA\t: ") 
	kadaluwarsa = input("KADALUWARSA\t: ") 

	user_ans = input("Tekan Y untuk menyimpan(Y/N) : ")

	if verify_ans(user_ans):
		id_product = create_id_product()
		print("Menyimpan Data ...")
		data_menu[id_product] = {
			"merek" : merek,
			"rasa" : rasa,
			"kadaluwarsa" : kadaluwarsa
		}
		print("Data Tersimpan")
	else:
		print("Data batal Disimpan")
	input("Tekan ENTER untuk kembali ke MENU")

def print_menu():
	print_header("-SEMUA PRODUK-")
	if len(data_menu) == 0:
		print("<BELUM ADA DATA PRODUK YANG DISIMPAN>")
	else:
		print_data_menu(all_fields=True)
	input("Tekan ENTER untuk kembali ke MENU")

def searching_by_name(menu):
	for id_product in data_menu:
		if data_menu[id_product]["merek"] == menu:
			print_data_menu(id_product=id_product)
			return True
	else:
		print("-DATA TIDAK DITEMUKAN-")
		return False

def get_id_product_from_name(menu):
	for id_product in data_menu:
		if data_menu[id_product]["merek"] == menu:
			return id_product

def find_product():
	print_header("-CARI PRODUK-\n")
	merek = input("Nama Produk Yang Dicari : ")
	result = searching_by_name(merek)
	input("Tekan ENTER untuk kembali ke MENU")

def delete_product_info():
	pass
	#sir nggak tau ngapa error terus kode utk deletenya jadi saya nyerah

def update_brand(menu):
	print(f"Merek Lama \t: {menu}")
	new_brand = input("Merek Baru\t: ")
	respon = input("Apa yakin ingin mengganti datanya (Y/N) : ")
	if verify_ans(respon):
		id_product = get_id_product_from_name(menu)
		data_menu[id_product]["merek"] = new_brand
		print("Data telah di-update")
	else:
		print("Data batal diperbarui")

def update_flavor(menu):
	id_product = get_id_product_from_name(menu)
	print(f"Merek \t: {data_menu[id_product]['merek']}")
	print(f"Rasa Lama\t: {data_menu[id_product]['rasa']}")
	new_flavor = input("Rasa Baru\t: ")
	respon = input("Apa yakin ingin mengganti datanya (Y/N) : ")
	if verify_ans(respon):
		data_menu[id_product]['rasa'] = new_flavor
		print("Data telah di-update")
	else:
		print("Data batal diperbarui")

def update_expiration_date(menu):
	id_product = get_id_product_from_name(menu)
	print(f"Merek \t: {data_menu[id_product]['merek']}")
	print(f"Kadaluwarsa Lama\t: {data_menu[id_product]['kadaluwarsa']}")
	new_expiration_date = input("Kadaluwarsa Baru\t: ")
	respon = input("Apa yakin ingin mengganti datanya (Y/N) : ")
	if verify_ans(respon):
		data_menu[id_product]['kadaluwarsa'] = new_expiration_date
		print("Data telah di-update")
	else:
		print("Data batal diperbarui")

def update_product_info():
	print_header("PERBARUI DATA PRODUK\n")
	merek = input("Nama produk yang ingin diperbarui : ")
	result = searching_by_name(merek)
	if result:
		print("Data yang ingin diperbarui : ")
		print("[1]. Merek , [2]. Rasa , [3]. Kadaluwarsa")
		respon = input("Pilihan : ")
		if respon == "1":
			update_brand(merek)
		elif respon == "2":
			update_flavor(merek)
		elif respon == "3":
			update_expiration_date(merek)
	input("Tekan ENTER untuk kembali ke menu utama")

def technical_problem():
	print_header("Please wait.")
	print("We have contacted the nearest employee.")
	print("Sorry for the inconveniences.")
	input("Tekan ENTER untuk kembali ke menu utama")
			
def check_input(char):
	char = char.upper()
	if char == "G":
		return True
	elif char == "A":
		print_menu()
	elif char == "B":
		find_product()
	elif char == "C":
		update_product_info()
	elif char == "D":
		add_to_menu()
	elif char == "E":
		delete_product_info()
	elif char == "F":
		technical_problem()

data_menu = {
	"20201007-C001" : {
		"merek" : "Fanta",
		"rasa" : "Grape",
		"kadaluwarsa" : "20-12-2020"
	},
	"20201007-C002" : {
		"merek" : "Indomilk",
		"rasa" : "Melon",
		"kadaluwarsa" : "13-11-2020"
	}
}
stop = False

while not stop:
	view_menu()
	user_input = input("Pilihan : ")
	stop = check_input(user_input)
