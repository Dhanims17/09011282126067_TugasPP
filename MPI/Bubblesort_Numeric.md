# MPI-Bubblesort menggunakan Python
Tugas Pemrosesan Paralel MPI Numerik

# Menyiapkan Ubuntu Server dan Linux Ubuntu
 1. Pada setiap PC/LAPTOP menggunakan jaringan yang sama agar ip yang digunakan sama 
 2. Menentukan master, slave1, slave2, slave3
 3.	Melakukan penginstalan net-tools.
 4.	Melakukan pengecekan IP dengan perintah berikut:


$ Ifconfig

| NAMA    | Master           | Slave1           | Slave2          | Slave3           |
|---------|------------------|------------------|-----------------|------------------|
| IP      | 192.168.102.170  | 192.168.102.215  | 192.168.102.95  | 192.168.102.236  |

# Membuat MPI Cluster
## 1.	Konfigurasi hosts file /etc/hosts
- Pada Master
  
  ![image](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/5d49b47d-8f20-4985-abc7-737415886bdf)

- Pada Slave1

  ![WhatsApp Image 2023-11-16 at 08 58 02_f2679545](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/3a0e7736-9479-4deb-9793-b66eed0e3352)


- Pada Slave2
  
  ![image](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/20f347fc-a353-4ff3-8401-cca8d8adc614)



- Pada Slave3 

  ![WhatsApp Image 2023-11-16 at 08 54 14_931758a3](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/6dff01e5-2a78-4bf1-bfd9-be444cd58f02)



## 2. Membuat User Baru
Buat user baru di SERVER dan CLIENT. Nama user harus samo semua di seluruh komputer.

$ sudo adduser <nama user>

$ sudo usermod -aG sudo <nama user>

$ su - <nama user>

## Server
-	Master
  
  ![image](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/c9ec4657-f974-47b6-af9c-c89828c20948)


## Client
-	Slave1

   ![WhatsApp Image 2023-11-16 at 08 57 29_3afc7f15](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/b9e47471-1fd5-4e76-9523-c16d33915f01)

-	Slave2
  
   ![WhatsApp Image 2023-11-16 at 08 57 14_0a10ae23](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/1d1a9566-e547-4723-b421-856e7d460980)

-	Slave3
  
   ![image](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/efa7ae48-6967-4212-8651-08178d22a5aa)



## 3. Konfigurasi SSH
Setelah membuat dan masuk ke user, lakukan konfigurasi SSH.

1. Install SSH
   
$ sudo apt install openssh-server

-	Pada master

  ![WhatsApp Image 2023-11-16 at 09 00 19_535c2ed5](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/7a5155aa-57da-4c2d-88b5-d4977112310f)

-	Pada Slave1
  
  ![WhatsApp Image 2023-11-16 at 09 01 48_26c97d80](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/ea600a7f-ff54-4163-9583-4f8be8437b71)

-	Pada Slave2

  ![WhatsApp Image 2023-11-16 at 09 01 51_a1af6f7b](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/ebd038fa-c1a8-4d62-af31-dc37e41f235c)

-	Pada Slave3

  ![image](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/6cdf6aee-4826-4f4b-9e4d-45c0313ae559)



2. Melakukan pengecekan SSH
   
$ ssh nama user@host

-	SSH dari Master ke Worker

  ![WhatsApp Image 2023-11-16 at 09 05 53_046e9c4c](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/1832aeec-e358-4389-b123-22dc50728b36)


-	SSH dari Worker ke Master

  ![WhatsApp Image 2023-11-16 at 09 05 04_f5ca2868](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/eedac203-d67a-4821-a521-b9af2462f2dc)



3. Generate Keygen
Lakukan di SERVER

$ ssh-keygen -t rsa

  ![WhatsApp Image 2023-11-16 at 09 07 41_f92a5ebc](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/65ff94c3-3f48-482f-b924-4bd07422d350)


4. Copy key publik ke client
   
$ cd .ssh

$ cat id_rsa.pub | ssh <nama user>@<host> "mkdir .ssh; cat >> .ssh/authorized_keys"

![WhatsApp Image 2023-11-16 at 09 11 22_667e2f51](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/ec08cb9d-2907-4cbd-a997-6819422e9388)



## 5. Konfigurasi NFS

1. Buat shared folder

$ mkdir banyu

-	Pada Master
  
  ![WhatsApp Image 2023-11-16 at 09 12 38_db6224be](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/9bc9d6d8-3951-42bd-8130-c47f02ee57d3)

-	Pada Slave1

  ![WhatsApp Image 2023-11-16 at 09 12 57_75604aa4](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/c037e724-3686-4117-bc45-ed628f57996e)

-	Pada Slave2
  
  ![WhatsApp Image 2023-11-16 at 09 13 05_b274514a](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/67eb8cad-7f9b-4bb0-bc8d-18d98a94d6c8)

-	Pada Slave3
  ![image](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/3fad8099-cf46-45f4-bcae-39a5690a8d99)



2. Install NFS Server

$ sudo apt install nfs-kernel-server

![WhatsApp Image 2023-11-16 at 09 13 40_4f1ec2f6](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/da6ab4a2-50d7-4de9-af5e-1352d2abf9c9)



3. Konfigurasi file /etc/exports

<lokasi shared folder> *(rw,sync,no_root_squash,no_subtree_check)

![WhatsApp Image 2023-11-16 at 09 14 19_13ca38c1](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/002e24a5-9568-4e86-a897-05e6c1dce35f)



$ sudo exportfs -a

$ sudo systemctl restart nfs-kernel-server

![WhatsApp Image 2023-11-16 at 09 15 21_3cdcd1ec](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/4b83de68-838a-4448-96cb-9fe4679c6f5d)



4. Install NFS Client
      
$ sudo apt install nfs-common

-	Slave1

  ![WhatsApp Image 2023-11-16 at 09 16 12_f28d7014](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/646a25d0-d6fb-4260-a603-630fd561bad6)


-	Slave2

  ![WhatsApp Image 2023-11-16 at 09 16 31_008aa2d8](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/53700d30-d617-43d4-bf84-03a20fcd21c7)


-	Slave3
  
   ![image](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/e72550e2-b0ed-4975-a98a-9072de141780)


5. Mounting

$ sudo mount <server host>:<lokasi shared folder di server> <lokasi shared folder di client>

![WhatsApp Image 2023-11-16 at 09 17 39_1d2007ec](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/3fe7af25-ae43-4c5b-ad02-8c5958b34803)



## 6. Instalasi MPI
1.	Install MPI

$ sudo apt install openmpi-bin libopenmpi-dev

-	Pada Master

 	![WhatsApp Image 2023-11-16 at 09 18 20_ce5dec11](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/b8711c84-a2b2-4dda-a175-ba5a7e428cac)


-	Pada Slave1

  ![WhatsApp Image 2023-11-16 at 09 18 51_d59be5ad](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/d545f3f5-1bbe-43d0-b753-4a20c9894e3f)


-	Pada Slave2

  ![WhatsApp Image 2023-11-16 at 09 18 42_1253f3e4](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/4b6ce657-adcb-4f00-902f-9c009d7b6432)


-	Pada Slave3

   ![image](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/e1bde2d5-6970-47a6-82bb-79c58a44d8c0)



# Menjalankan Program Bubblesort.py dan numeric.py
## 1.	Membuat Program

- bublleshort.py
  ![WhatsApp Image 2023-11-16 at 09 21 53_bd6f8c12](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/219a38a8-fa9e-4084-86db-d84490e6ceb4)

- numeric.py
  ![WhatsApp Image 2023-11-16 at 10 50 02_92063d89](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/ae1f64d9-37a6-432e-a0b9-dd16c881ae1d)



## 2.	Instalasi Python

$ sudo apt install python3-pip

  ![WhatsApp Image 2023-11-16 at 09 21 32_22db0afa](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/e1eef407-dd14-4b23-98b0-c6d7cda27c5a)



## 3.	Eksekusi Bubblesort dan Numerik menggunakan Python

$ python3 numeric.py

![WhatsApp Image 2023-11-16 at 10 49 27_ea3eedca](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/cc1f1123-a407-488a-9dda-85b3ff25f342)

$ python3 bubblesort.py

![WhatsApp Image 2023-11-16 at 10 44 01_3af90d40](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/2a7ef719-85cf-4c0a-866b-2f56c3b718dc)


## 4. Eksekusi Bubblesort dan Numerik menggunakan MPI


$ mpirun -np 2 -host master,slave3 phyton3 numeric.py

![WhatsApp Image 2023-11-16 at 10 49 47_af8541bf](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/0aeaa105-4622-4b06-be6e-a96041547670)

$ mpirun -np 2 -host master,slave3 python3 bubblesort.py

![WhatsApp Image 2023-11-16 at 10 44 16_22d2313a](https://github.com/Dhanims17/09011282126067_TugasPP/assets/150988829/f175756a-3b33-4143-87dc-7523762cc4a1)

