# Tugas Praktikum { Pertemuan ke 14 } 

## Profil
|**Nama**|**NIM**|**Kelas**|**Matkul**|
|----|---|-----|------|
|Muhammad Arif Mulyanto|312310359|TI.23.A.5|Basis Data|
# Soal

![prak 14 1](https://github.com/MuhArifyanto/MYSQL8/assets/147913440/a3aaf7ac-a87c-44d3-8c9b-e01376ed4a8d)

# ER-Diagram

![prak 14 2](https://github.com/MuhArifyanto/MYSQL8/assets/147913440/c84a2137-ad25-4ca8-90be-cee51d251c93)

# Tabel Data

![prak 14 3](https://github.com/MuhArifyanto/MYSQL8/assets/147913440/fc2f7487-f7fb-4a8d-b446-ffd44d9f7540)

# Soal Latihan Praktikum 6

- ## 1. Departemen Apa Saja Yang Terlibat Dalam Tiap-tiap Project.

```
SELECT Project.nama AS Project, GROUP_CONCAT(Departemen.nama) AS Departemen
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
GROUP BY Project.id_proj;
```
***Output :***

![prak 14 4](https://github.com/MuhArifyanto/MYSQL8/assets/147913440/ea2f1f60-4ca4-4b5e-bbab-4d83472c9fdc)

## 2. Jumlah Karyawan Tiap Departemen Yang Bekerja Pada Tiap-tiap Project.

```
SELECT Project.nama AS Project, Departemen.nama AS Departemen, COUNT(*) AS 'Jumlah Karyawan'
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
GROUP BY Project.id_proj, Departemen.id_dept;
```
***Output :***

![prak 14 5](https://github.com/MuhArifyanto/MYSQL8/assets/147913440/757c4614-ddd4-4ac5-b9f0-433bcd2c1a47)

## 3. Ada Berapa Project Yang Sedang Dikerjakan Oleh Departemen ***RnD***? (ket: project berjalan adalah yang statusnya 1).

```
SELECT COUNT(*) AS 'Jumlah Project'
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
WHERE Departemen.nama = 'RnD' AND Project.status = 1;
```
***Output :***

![prak 14 6](https://github.com/MuhArifyanto/MYSQL8/assets/147913440/0a5d6b77-0fe8-4fa0-85f2-13ad0424725d)


## 4. Berapa banyak Project yang sedang dikerjakan oleh Ari ?

```
SELECT COUNT(*) AS 'Jumlah Project'
FROM Project_detail
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
WHERE Karyawan.nama = 'Ari' AND Project_detail.id_proj IN (SELECT id_proj FROM Project WHERE status = 1);
```
***Output :***

![prak 14 7](https://github.com/MuhArifyanto/MYSQL8/assets/147913440/c88b9486-a36c-458b-bd22-049ac292f47f)

## 5. Siapa Saja Yang Mengerjakan Project B ?

```
SELECT Karyawan.nama
FROM Project_detail
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
WHERE Project_detail.id_proj IN (SELECT id_proj FROM Project WHERE nama = 'B');
```
***Output :***

![prak 14 8](https://github.com/MuhArifyanto/MYSQL8/assets/147913440/3c5baf0b-a2b2-4956-b95a-aea5331bf966)

