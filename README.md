# Tugas 13 MySQL

Buat ulang procedure penilaian(). Stored procedure penilaian() nantinya menerima 1 buah parameter berupa kode nim mahasiswa. Berdasarkan kode nim ini, cari nilai IP semester_1 dari mahasiswa tersebut. Hasil akhir dari procedure penilaian() berupa string, tergantung nilai IP semester_1 dari mahasiswa tersebut.


Aturannya adalah sebagai berikut:

- IPK 0.00 - 1.00: ‘Serius kuliah g sih?’
- IPK 1.01 - 2.00: ‘Kebanyakan main’
- IPK 2.01 - 3.00: ‘Berusaha lagi’
- IPK 3.01 - 4.00: ‘Mantap, pertahankan!’
- Selain itu: ‘Nilai tidak sesuai’

Berikut hasil akhir yang diinginkan dari pemanggilan stored procedure penilaian():

```
CALL penilaian('17080305');
-- Mantap, pertahankan!
```

```
CALL penilaian('17140143');
-- Berusaha lagi
```

Silahkan teman-teman coba rancang kode programnya!


Tips: 

Membuat procedure ini butuh beberapa langkah:

1. Ambil nilai argumen yang berupa nim lalu input ke dalam SELECT...WHERE untuk mencari nilai semester_1 dari mahasiswa tersebut.

2. Siapkan sebuah variabel untuk menampung nilai semester_1 hasil dari langkah nomor 1.

3. Buat kondisi IF ELSEIF ELSE atau CASE puntuk mengkonversi nilai semester_1 menjadi string dengan aturan di dalam soal.

## Query
```
DELIMITER $$

CREATE PROCEDURE penilaian(nim CHAR(8))
BEGIN
	DECLARE nilai DECIMAL(4,2) DEFAULT 0;
	SET nilai = ( 
		SELECT semester_1 FROM nilai_mahasiswa WHERE nilai_mahasiswa.nim = nim
	);
	IF nilai <= 1 THEN
		SELECT 'Serius kuliah g sih?';
	ELSEIF nilai <= 2 THEN
		SELECT 'Kebanyakan main';
	ELSEIF nilai <= 3 THEN
		SELECT 'Berusaha lagi';
	ELSEIF nilai <= 4 THEN
		SELECT 'Mantap, pertahankan!';
	ELSE
		SELECT 'Nilai tidak sesuai';
	END iF;
END$$

DELIMITER ;
```
