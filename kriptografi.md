# KRIPTOGRAFI

Kriptografi adalah ilmu yang mempelajari teknik - teknik matematika yang berhubungan dengan aspek keamanan informasi seperti kerahasiaan, integritas data, serta otentikasi (Menes, 1996)

Kata *cryptography* berasal dari bahasa Yunani:

- ``cryptos`` yang berarti rahasia

- ``graphein`` yang berarti penulisan

maka, *cryptography* artinya adalah penulisan rahasia.

Salah satu contoh alat kriptografi klasik yang telah ada pada zaman Romawi adalah *``scytale``*. Cara kerja alat ini yaitu dengan menuliskan pesan diatas pita yang digulung pada batang silinder.

![gambar1](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSV4BaOUbFqstroIUbDXGcLUTm1a6xFxkDQcS9FFILbHSIJBDDK3XoPhBPOGqt94sFbKl4&usqp=CAU)

Contoh, jika kita ingin mengirim pesan:

```
TEMUI SAYA DI MARKAS SORE INI
```

Maka, kita dapat menulis di atas batang silinder dengan:
```
T E M U I S
A Y A D I M
A R K A S S
O R E I N I
```
Jika pita dilepaskan, maka tulisan yang muncul adalah:

```
TAAYOEYRRMAKEUDAIIISNSMSI
```

## Layanan Kriptografi

- Terjaga kerahasiaannya, yaitu hanya yang memiliki otoritas atau kunci rahasia yang dapat membuka informasi yang telah disandi.

- Integritas data (terjaga keasliannya), yaitu sistem harus memiliki kemampuan untuk mendeteksi manipulasi data oleh pihak-pihak yang tidak berhak, antara lain penyisipan, penghapusan, dan pensubsitusian data lain kedalam data yang sebenarnya.

- Autentikasi, adalah berhubungan dengan identifikasi/pengenalan, baik secara kesatuan sistem maupun informasi itu sendiri. Pengirim informasi adalah asli (*authentication*), bukan pihak ketiga.

- Non-repudiasi, atau nirpenyangkalan adalah usaha untuk mencegah terjadinya penyangkalan terhadap pengiriman/terciptanya suatu informasi oleh yang mengirimkan/membuat.

## Istilah dalam Kriptografi

- Pesan (*plaintext, plain-image, plain-video, plain-audio*), yaitu informasi yang dapat dibaca dan dimengerti maknanya.
- *Sender*, yaitu pihak pengirim pesan.
- *Receiver*, yaitu pihak penerima pesan.
- *Chipertext / Cryptogram*, yaitu pesan yang telah disandikan (di-enkripsi) dengan tujuan agar hanya bisa dibaca oleh pihak tertentu.

    Contoh :
    
    *Plaintext* : bertemu di markas jam 7 malam
        
    *Chipertext* : 5U5eEJ9YsBJjog88XhjRPm8pNqt1EqTu9uMNEKPJ

- *Encryption*, yaitu proses mengubah *plaintext* menjadi *chipertext*.
- *Decryption*, yaitu proses mengubah *chipertext* menjadi *plaintext*

    ![skema-enkripsi-deksripsi](https://cogierb201.files.wordpress.com/2012/04/kriptografi.png)

- *Chiper*, yaitu algoritma yang digunakan untuk enkripsi dan deskripsi pesan
    ```
    Contoh :
        Enkripsi : Geser 4 huruf ke kanan
        Deskripsi : Geser 4 huruf ke kiri

        E(p) = (p + 4) mod 26
        D(c) = (c - 4) mod 26
    
    Misalkan kita punya plainteks : SAYA
    
    E(S)    = (S + 4) mod 26
            = (19 + 4) mod 26
            = 23 mod 26
            = 23
            = W

    Maka, "SAYA" apabila diubah menjadi sebuah chiperteks akan menjadi "WECE"
    ```

- *Key*, yaitu parameter yang digunakan dalam enkripsi dan deskripsi, serta bersifat rahasia.
- *Eavesdropper* (penyadap), yaitu pihak yang menangkan pesan selama ditransmisikan.
- *Cryptanalysis*, yaitu ilmu untuk memecahkan *chipertext* menjadi *plaintext* tanpa mengetahui *key* yang digunakan.
- *Cryptology*, yaitu studi engenai *criptogafi* dan *cryptanalysis*.

## Teknik Dasar Kriptografi Klasik

### 1. *Substitution Chipers*
*Substitution Chiper*, yaitu mengganti *plaintext* dengan *chipertext*. Jenis-jenis *Substitution Chiper*:
1. Cipher abjad-tunggal (*Monoalphabetic cipher*)
2. Cipher substitusi homofonik (*Homophonic substitution cipher*)
3. Cipher abjad-majemuk (*Polyalpabetic substitution cipher*)
4. Cipher substitusi poligram (*Polygram substitution cipher*)

### 2. *Transposition Chipers*, 
*Transposition Chipers*, yaitu mengubah susunan/posisi huruf *plaintext* ke posisi lainnya. 

## Contoh Kriptografi Klasik

### 1. Caesar Chiper

![ilustrasi](https://media.geeksforgeeks.org/wp-content/uploads/ceaserCipher.png)

Teknik Caesar Chiper adalah salah satu metode teknik enkripsi dengan menggunakan *substitution chipper*. Teknik ini dilakukan dengan pergeseran huruf. Misalkan kita melakukan pergeseran sebanyak 5 kali ke kanan, maka A akan digantikan oleh F, B digantikan oleh G, dan seterusnya seperti contoh:

*plaintext* : A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

*chipertext* : F G H I J K L M N O P Q R S T U V W X Y Z A B C D E

Caesar Chiper dapat dirumuskan secara matematis dengan: 

- Jika pergeseran huruf sejauh n, maka:
> c = E(p) = (p + n) mod 26  
> p = D(c) = (c - n) mod 26

- Untuk 256 karakter ASCII, maka: 
> c = E(p) = (p + n) mod 256  
> p = D(c) = (c - n) mod 256

Keterangan:

p : karakter *plaintext*; c : karakter *chipertext*; n : shift (pergeseran) yang diinginkan.

Supaya lebih mudah dan efisien, berikut ini adalah source code untuk mengenkripsi sebuah kata atau kalimat dalam bentuk Caesar Chiper:

```py
#A python program to illustrate Caesar Cipher Technique
def encrypt(text,s):
    result = ""
 
    # traverse text
    for i in range(len(text)):
        char = text[i]
 
        # Encrypt uppercase characters
        if (char.isupper()):
            result += chr((ord(char) + s-65) % 26 + 65)
 
        # Encrypt lowercase characters
        else:
            result += chr((ord(char) + s - 97) % 26 + 97)
 
    return result
 
#check the above function
text = (input("Masukkan teks yang ingin di enkripsi: "))
s = 4
print ("Text  : " + text)
print ("Shift : " + str(s))
print ("Cipher: " + encrypt(text,s))
```
atau source code dapat di cek melalui [link ini](https://www.geeksforgeeks.org/caesar-cipher-in-cryptography/).

### 2. Vigenère Chiper

Vigenère Chiper termasuk ke dalam cipher abjad-majemuk (polyalpabetic substitution
cipher). Teknik ini dipublikasikan oleh diplomat Perancis, Blaise de Vigènere pada abad 16 (tahun 1586). Tetapi sebenarnya teknik ini telah digambarkan oleh Giovan Batista Belaso pada tahun 1553 dalam bukunya yang berjudul La Cifra del Sig. 

- **Encrypt**

    Contoh Vigenère square untuk melakukan enkripsi:
    ![ilustrasi](https://pages.mtu.edu/~shene/NSF-4/Tutorial/VIG/FIG-VIG-Table.jpg)

    ```
    Contoh cara enkripsi:

    plainteks : POROSORGANIZATION
    kata kunci : OPEN
    kunci : OPENOPENOPENOPENO
    chiperteks : DDVBGDVTOCMMOIMBB

    Keterangan :
    Huruf pertama dari plainteks, P dipasangkan dengan O, huruf pertama dari kunci. Jadi gunakan baris P dan kolom O dari Vigenère square yaitu D. Demikian pula untuk huruf kedua dari plaintext digunakan huruf kedua dari kunci, huruf pada baris O dan kolom P adalah D. Huruf selanjutnya juga dilakukan hal yang sama secara terus - menerus.
    ```

- **Decrypt**

    Dekripsi dilakukan dengan cara menuju baris pada tabel yang sesuai dengan kunci, mencari posisi huruf ciphertext pada baris ini, dan kemudian menggunakan label kolom sebagai plaintext. Misalkan pada baris O (dari OPEN, ciphertext D muncul di kolom P yang merupakan huruf plaintext pertama. Kemudian, pada baris kedua, yaitu P  (dari OPEN), cari ciphertext D yang terdapat pada kolom O yang merupakan huruf plaintext kedua. Implementasi lain adalah dengan memvisualisasikan Vigenère secara aljabar dengan mengubah [A-Z] menjadi angka [0–25]. 

Vigenère Chiper dapat digambarkan secara matematis dengan:
```
Enkripsi
E = (P + K) mod 26

Dekripsi 
D = (E - K + 26) mod 26 
```

#### **Kasiski Test**

Langkah-langkah metode Kasiski:
1. Temukan semua kriptogram yang berulang di dalam cipherteks (pesan yang panjang biasanya mengandung kriptogram yang berulang).
2. Hitung jarak antara kriptogram yang berulang
3. Hitung semua faktor (pembagi) dari jarak tersebut (faktor pembagi menyatakan panjang kunci yang mungkin ).
4. Tentukan irisan dari himpunan faktor pembagi tersebut. Nilai yang muncul di dalam irisan menyatakan angka yang muncul pada semua faktor pembagi dari jarak-jarak tersebut . Nilai tersebut mungkin adalah panjang kunci.

Berikut ini adalah implementasi Vigenère Chiper dalam source code python:
```py
# Python code to implement Vigenere Cipher
 
# This function generates the key in a cyclic manner until it's length isn't equal to the length of original text
def generateKey(string, key):
    key = list(key)
    if len(string) == len(key):
        return(key)
    else:
        for i in range(len(string) -
                       len(key)):
            key.append(key[i % len(key)])
    return("" . join(key))
     
# This function returns the encrypted text generated with the help of the key
def cipherText(string, key):
    cipher_text = []
    for i in range(len(string)):
        x = (ord(string[i]) +
             ord(key[i])) % 26
        x += ord('A')
        cipher_text.append(chr(x))
    return("" . join(cipher_text))
     
# This function decrypts the encrypted text and returns the original text
def originalText(cipher_text, key):
    orig_text = []
    for i in range(len(cipher_text)):
        x = (ord(cipher_text[i]) -
             ord(key[i]) + 26) % 26
        x += ord('A')
        orig_text.append(chr(x))
    return("" . join(orig_text))
     
# Driver code
if __name__ == "__main__":
    string = input("Masukkan teks yang akan di enkripsi:" )
    keyword = "OPEN"
    key = generateKey(string, keyword)
    cipher_text = cipherText(string,key)
    print("Ciphertext :", cipher_text)
    print("Original/Decrypted Text :", originalText(cipher_text, key))
 
# This code is contributed by Pratik Somwanshi
```
atau source code dapat di cek melalui [link ini](https://www.geeksforgeeks.org/vigenere-cipher/).

### 3. Playfair Chiper

![ilustrasi](https://scienceblogs.de/klausis-krypto-kolumne/files/2018/04/Playfair-bar-590x360.png)

Playfair Chiper ditemukan oleh Sir Charles Wheatstone namun dipromosikan oleh
Baron Lyon Playfair pada tahun 1854. Teknik ini termasuk ke dalam *polygram chiper*.

Kunci kriptografi Playfair Chiper berupa 25 buah huruf yang disusun di dalam tabel berukuran 5x5 dengan menghilangkan huruf J dari tabel. Jika *plaintext* berisi J, maka akan diganti dengan I. Cipher ini mengenkripsi pasangan huruf (bigram), bukan huruf tunggal seperti pada cipher klasik lainnya. Jika jumlah huruf ganjil, maka dapat ditambah huruf z di akhir.

```
Contoh  

kunci : POROS
plainteks : KRIPTOGRAFI
split : 'KR' 'IP' 'TO' 'GR' 'AF' 'IZ'
chiperteks : ISGRNSIPFLQR
```

Maka, bentuk tabel untuk contoh di atas adalah:
|   |   |   |   |   |
|---|---|---|---|---|
| P	| O	| R	| S	| A |
| B	| C	| D	| E	| F |
| G	| H	| I	| K | L |
| M	| N	| Q	| T	| U |
| V	| W	| X	| Y	| Z |

Untuk deskripsi, memiliki aturan yang berbeda dengan enkripsi:
1. Jika dua huruf terdapat pada baris yang sama maka tiap huruf diganti dengan huruf di kirinya.
2. Jika dua huruf terdapat pada kolom yang sama maka tiap huruf diganti dengan huruf di atasnya.

    Sebagai contoh:
    
    chiperteks : FL
    
    plainteks : AF

    |   |   |   |   |   |
    |---|---|---|---|---|
    | P	| O	| R	| S	| A |
    | B	| C	| D	| E	| F |
    | G	| H	| I	| K | L |
    | M	| N	| Q	| T	| U |
    | V	| W	| X	| Y	| Z |

3. Jika dua huruf tidak pada baris yang sama atau kolom yang sama, maka huruf pertama diganti dengan huruf pada perpotongan baris huruf pertama dengan kolom huruf kedua. Huruf kedua diganti
dengan huruf pada titik sudut keempat dari persegi panjang yang dibentuk dari tiga huruf yang digunakan sampai sejauh ini.

    Sebagai contoh:
    
    chiperteks : IS
    
    plainteks : KR

    |   |   |   |   |   |
    |---|---|---|---|---|
    | P	| O	| R	| S	| A |
    | B	| C	| D	| E	| F |
    | G	| H	| I	| K | L |
    | M	| N	| Q	| T	| U |
    | V	| W	| X	| Y	| Z |

4. Huruf z dibuang karena tidak mengandung makna.

>*Catatan: Chipertext* selalu memiliki jumlah karakter *genap*.

### 4. Affine Chiper

Affine Chiper adalah jenis chiper substitusi monoalfabetik. Dalam Chiper Affine, huruf-huruf alfabet berukuran m pertama-tama dipetakan ke bilangan bulat dalam rentang 0-25. Chipper ini merupakan perluasan dari Caesar Chiper.

**Encrypt**
```
C = E(x) = (ax + b) mod m 

Keterangan:
modulus m: ukuran alfabet
a dan b: kunci sandi.
a harus dipilih sedemikian rupa sehingga a dan m adalah koprima.
```
- Contoh:

    plainteks: P O R O S (16 15 18 15 19)

    m = 26, a = 7, b = 9 

    |   Plainteks  | P  | O  | R  | O  | S  |
    |--------------|----|----|----|----|----|
    |       x      | 16 | 15 | 18 | 15 | 19 |
    | (ax+b) mod m | 17 | 10 | 5  | 10 | 12 |
    |   Chiperteks | K  | D  | Y  | D  | F  |`

    maka, kata `POROS` apabila di-enkripsi akan menjadi `KDYDF`.

**Decrypt**
```
P = D(x) = a^-1 (x - b) mod m

Keterangan:
a^-1 : invers perkalian modular dari modulo m, yaitu memenuhi persamaan
1 = a a^-1 mod m 
```
- Contoh:

    plainteks: P O R O S (16 15 18 15 19)

    m = 26, a = 7, b = 9 

    |   Plainteks     | K  | D  | Y  | D  | X  |
    |-----------------|----|----|----|----|----|
    |        x        | 17 | 10 | 5  | 10 | 12 |
    | a^-1(x-b) mod m | 16 | 15 | 18 | 15 | 19 |
    |   Chiperteks    | P  | O  | R  | O  | S  |

    maka, kata `KDYDF` apabila di-deskripsi akan menjadi `POROS`. 

Berikut ini adalah salah satu [link](https://cryptii.com/pipes/affine-cipher) web yang dapat kita gunakan untuk encode/decode teks dengan Affine Chipper.

### 5. Enigma Chiper

![ilustrasi](https://dmdlnu87i51n1.cloudfront.net/v1/uk/ckaqntxdq0alo0113sgrsmave/0x1494:4758x2498/1200x630/200604enigma.jpg)

Enigma adalah mesin yang digunakan Jerman selama Perang Dunia II untuk mengenkripsi/dekripsi pesan-pesan militer. Mesin Enigma dipatenkan oleh seorang insinyur asal Jerman yang bernama Arthur Scherbius pada tahun 1918, yang kemudian digunakan oleh militer dan pemerintah Jerman Nazi sebelum dan selama Perang Dunia II. Mesin ini memiliki 7 komponen utama, yaitu kotak enigma, *plugboard*, *keyboard*, *lampboard*, *reflektor*, penggerak rotor, dan rotor. 

Cara kerja mesin enigma adalah berdasarkan perputraan rotor yang ada di dalamnya. Misalkan kita ingin meng-enkripsi sebuah huruf, ketika huruf A diketikkan pada *keyboard*, maka arus listrik akan mengalir melewati *plugboard*, kemudian melewati 3 buah rotor, dilanjutkan ke *reflektor*, dan setelah itu dibalikkan kembali melewati 3 rotor yang selanjutnya diteruskan ke *plugboard*, sehingga huruf yang dienkripsi  ditampilkan dengan bentuk lampu yang menyala. Perputaran rotor disini sama halnya dengan sebuah Odometer, yaitu jika rotor pertama telah menyelesaikan satu putaran penuh, maka rotor ditengah akan berubah satu posisi, dan seterusnya untuk rotor yang berikutnya.
