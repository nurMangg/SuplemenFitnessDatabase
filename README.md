# SuplemenFitnessDatabase
Database Suplemen Fitness - Built With Mysql phpmyadmin

*Pemilihan Suplemen Fitness Menggunakan Metode SAW - Using View Mysql*

How To Works :
1. Create View Pembagi
2. Create View Normalisasi
3. Create View Hasil



## VIEW PEMBAGI

```mysql
CREATE VIEW pembagi AS SELECT MIN(harga) AS harga, MAX(isi) AS isi, MAX(protein) AS protein, MIN(gula) AS gula, MAX(kalori) AS kalori FROM fitness;
```

## VIEW NORMALISASI

```mysql
CREATE VIEW normalisasi AS SELECT f.nama_suplemen AS nama, p.harga / f.harga AS harga, f.isi / p.isi AS isi, f.protein / p.protein AS protein, p.gula / f.gula AS gula, f.kalori / p.kalori AS kalori FROM fitness AS f join pembagi AS p;
```


## VIEW HASIL

```mysql
CREATE VIEW Hasil AS SELECT n.nama AS Nama, (SELECT bobot FROM kriteria WHERE nama = 'harga') * n.harga + (SELECT bobot FROM kriteria WHERE nama = 'isi') * n.isi + (SELECT bobot FROM kriteria WHERE nama = 'protein') * n.protein + (SELECT bobot FROM kriteria WHERE nama = 'gula') * n.gula + (SELECT bobot FROM kriteria WHERE nama = 'kalori') * n.kalori AS Hasil FROM normalisasi AS n JOIN kriteria AS k GROUP BY n.nama ORDER BY Hasil DESC;
```

