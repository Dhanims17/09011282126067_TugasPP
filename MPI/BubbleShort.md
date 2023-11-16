# MPI-Bubblesort menggunakan Python
Tugas Pemrosesan Paralel MPI Numerik

# Menyiapkan Ubuntu Server dan Linux Ubuntu
## 1. Pada setiap PC/LAPTOP menggunakan jaringan yang sama agar ip yang digunakan sama 
## 2. Menentukan master, slave1, slave2, slave3
## 3.	Melakukan penginstalan berikut: net-tools untuk ngecek IP, vim untuk teks editor.

$ sudo apt install net-tools vim

![image](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/c2520e70-5e9b-4532-ac8f-3b22e68e13b3)


## 4.	Melakukan pengecekan IP dengan perintah berikut:

$ Ifconfig
| NAMA    | Master           | Slave1           | Slave2          | Slave3           |
|---------|------------------|------------------|-----------------|------------------|
| IP      | 192.168.102.170  | 192.168.102.215  | 192.168.102.95  | 192.168.102.236  |

# Membuat MPI Cluster
## 1.	Konfigurasi hosts file /etc/hosts
- Pada Master
  
 ![WhatsApp Image 2023-11-16 at 19 14 04_0ee9b605](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/7b8e917c-68f1-4ae8-bba8-6facb00ecb2f)

- Pada Slave1

  ![WhatsApp Image 2023-11-16 at 08 58 02_dd7fa2f2](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/ce62c6da-2d6c-4da6-86d5-5d9fab9a28af)

- Pada Slave2
  
  ![WhatsApp Image 2023-11-16 at 08 49 35_762e3b49](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/2445b4e2-0070-44fb-acbb-2bb6766eca2a)


- Pada Slave3 

  ![WhatsApp Image 2023-11-16 at 08 54 14_0da3f0fe](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/e8f1151d-dc2a-45cd-b6ae-e0665790fa39)


## 2. Membuat User Baru
Buat user baru di SERVER dan CLIENT. Nama user harus samo semua di seluruh komputer.

$ sudo adduser <nama user>

$ sudo usermod -aG sudo <nama user>

$ su - <nama user>

Server
-	Master
  
  ![WhatsApp Image 2023-11-16 at 08 53 53_e3ddd541](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/bc0ce36b-07df-4933-9cf5-c7c7bb04272d)

Client
-	Slave1
  
 ![WhatsApp Image 2023-11-16 at 08 57 29_05e8c12c](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/bc6d8d07-a415-4077-816a-0cc90fa7f269)


-	Slave2
  
  ![WhatsApp Image 2023-11-16 at 08 57 14_d14e7c7f](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/766dc1f7-4527-48c6-9ed9-62c61c16bef4)


-	Slave3
  
  ![image](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/60ea96df-13a7-44c8-8ce5-0502eac0bad8)


## 3. Konfigurasi SSH
Setelah membuat dan masuk ke user, lakukan konfigurasi SSH.

1. Install SSH
   
$ sudo apt install openssh-server

-	Pada master

  ![WhatsApp Image 2023-11-16 at 09 00 19_35306ee4](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/b89a6d78-4623-4e6c-9def-bb20f7e4461b)


-	Pada Slave1
  
  ![WhatsApp Image 2023-11-16 at 09 01 48_fa1a5a58](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/a5c4d99d-2a23-4300-bfdb-d4b105680085)


-	Pada Slave2

  ![WhatsApp Image 2023-11-16 at 09 01 51_3fbaea84](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/e54985ca-1c90-4540-94c4-717fa5e36d80)


-	Pada Slave3

  ![image](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/469ceeee-b2dd-4eb2-99e2-e5a3b1b3893e)


2. Melakukan pengecekan SSH
   
$ ssh nama user@host

-	SSH dari Master ke Worker

  ![WhatsApp Image 2023-11-16 at 09 05 53_03418604](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/8f5a2488-4490-457b-8de8-c7475b372fe7)


-	SSH dari Worker ke Master

  ![WhatsApp Image 2023-11-16 at 09 05 04_ca498b5c](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/d0b7bedb-89bb-4975-8ecc-3dc8b6809256)


3. Generate Keygen
Lakukan di SERVER

$ ssh-keygen -t rsa

![WhatsApp Image 2023-11-16 at 09 07 41_179a221e](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/1d2031a4-e6e8-48ef-8900-e194f5636980)


4. Copy key publik ke client
   
$ cd .ssh

$ cat id_rsa.pub | ssh <nama user>@<host> "mkdir .ssh; cat >> .ssh/authorized_keys"

![WhatsApp Image 2023-11-16 at 09 11 22_3e9ad4db](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/e33a2088-27ea-4178-a12f-23244ccb2dc9)



## 5. Konfigurasi NFS

1. Buat shared folder

$ mkdir banyu

-	Pada Master
  
![WhatsApp Image 2023-11-16 at 09 12 38_cf73ecae](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/0754d763-bd3d-41f9-8fb3-daaebe7408c3)


-	Pada Slave1

  ![WhatsApp Image 2023-11-16 at 09 12 57_e8cba145](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/82f9a35f-82f1-47b0-9d9a-a2f559dd0f21)


-	Pada Slave2
  
  ![WhatsApp Image 2023-11-16 at 09 13 05_a5a212ea](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/fda3db4d-725c-4bd2-9ab6-0ed78b803080)


-	Pada Slave3
  
![image](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/f46cc17f-f3a6-40c5-8424-2deeb68f7b33)


2. Install NFS Server

$ sudo apt install nfs-kernel-server

![WhatsApp Image 2023-11-16 at 09 13 40_9e329462](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/083e6759-3406-4e42-a4d9-7f9085ecb393)


3. Konfigurasi file /etc/exports

<lokasi shared folder> *(rw,sync,no_root_squash,no_subtree_check)

![WhatsApp Image 2023-11-16 at 09 14 19_50541347](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/e848f6c5-5484-455a-a21c-1a661b1255a0)


$ sudo exportfs -a

$ sudo systemctl restart nfs-kernel-server

![WhatsApp Image 2023-11-16 at 09 15 21_78a04ae3](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/26251b12-3600-4d82-a63c-2fcb9bc361f3)


4. Install NFS Client
      
$ sudo apt install nfs-common

-	Slave1

  ![WhatsApp Image 2023-11-16 at 09 16 12_b6933a6a](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/d2727cd4-2700-4576-a561-79c36fd3685b)


-	Slave2

  ![WhatsApp Image 2023-11-16 at 09 16 31_de0c5f59](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/4dfb7ad0-c7da-4e53-9dba-d5de27771635)


-	Slave3
  
  ![image](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/5d6771ba-5448-45de-b53f-7cc72d5ee9da)


5. Mounting

$ sudo mount <server host>:<lokasi shared folder di server> <lokasi shared folder di client>

![WhatsApp Image 2023-11-16 at 09 17 39_7b9c23fc](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/aba3364f-0e06-463b-b27a-958c0cbcbab0)


## 6. Instalasi MPI
1.	Install MPI

$ sudo apt install openmpi-bin libopenmpi-dev

-	Pada Master

 	![WhatsApp Image 2023-11-16 at 09 18 20_3d99ae94](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/276e7a6a-ec71-4c80-916c-cac030d21dd6)

-	Pada Slave1

  ![WhatsApp Image 2023-11-16 at 09 18 51_26627774](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/c7317a9f-10e6-4af8-bda1-c8a0e144fb54)


-	Pada Slave2

  ![WhatsApp Image 2023-11-16 at 09 18 42_4e1d2aae](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/cc1c7083-7125-4466-a454-511cecb32f74)


-	Pada Slave3

  ![image](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/7b1a787b-cabb-4c5f-a763-5e8265e3c342)


# Menjalankan Program Bubblesort.py
## 1.	Membuat Program

$ touch bubblesort.py

$ sudo nano bubblesort.py

- bublleshort.py
  ![WhatsApp Image 2023-11-16 at 09 21 53_c8d91ce8](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/8a488562-b80f-4116-83f7-05168601867c)

- nmeric.py
  ![WhatsApp Image 2023-11-16 at 10 50 02_710fce7e](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/1040ee95-f5e4-49bd-9360-0878b3e740bc)


## 2.	Instalasi Python

$ sudo apt install python3-pip

![WhatsApp Image 2023-11-16 at 09 21 32_71230188](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/e16f7a52-a60f-4018-9467-bd6784a341d0)


## 3.	Eksekusi Numerik menggunakan Python

$python3 numeric.py

![WhatsApp Image 2023-11-16 at 10 49 27_8f805807](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/534afb1e-d6bd-4dc2-a823-1fb5c81f9a84)


$ mpirun -np 2 -host master,slave3 phyton3 numeric.py

![WhatsApp Image 2023-11-16 at 10 49 47_a5acb996](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/21763521-2298-425a-b648-b45eae2e202e)


## 4. Eksekusi Bubblesort menggunakan MPI

$ python3 bubblesort.py

![WhatsApp Image 2023-11-16 at 10 44 01_a935f5b0](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/01813654-f4f1-4ba2-a145-aefb3e826f80)

$ mpirun -np 2 -host master,slave3 python3 bubblesort.py

![WhatsApp Image 2023-11-16 at 10 44 16_be9eb67e](https://github.com/Dhanims17/TugasPP_09011282126067/assets/150988829/a8f5cebf-edc4-4f90-bc64-b670c8221bbf)
