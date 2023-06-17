# Praktikum 6
Nama : Anggita Risqi Nur Clarita

NIM : 312210450

Kelas : TI.22.A.4

Mata Kuliah : Basis Data

Dosen Pengampu : Agung Nugroho, S.Kom., M.Kom.

## DAFTAR ISI <br>
| No | Description | Link |
|-----|------|-----|
|1|Soal Praktikum 6|[Click Here](#soal-praktikum-6)|
|2|ER-D Praktikum 6|[Click Here](#er-d-praktikum-6)|
|3|Input Data Studi Kasus Karyawan|[Click Here](#input-data-studi-kasus-karyawan)|
|4|Latihan Praktikum 6|[Click Here](#latihan-praktikum-6)|


## Soal Praktikum 6
[Link Soal (Drive)](https://drive.google.com/file/d/14HKkMEMXLBzzsqoWxPMgUi4npP7SVwaa/view)

## ER-D Praktikum 6
![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/ER-D.png)

## Input Data Studi Kasus Karyawan
![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/Input%20Data.png)

> **Keterangan** : Terdapat 5 tabel yang terdiri dari tabel Perusahaan, Departemen, Karyawan, Project dan Project Detail.

### *Script SQL berdasarkan Tabel Perusahaan*
```sql
CREATE TABLE Perusahaan(
id_p VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
alamat VARCHAR(45) DEFAULT NULL
);

INSERT INTO Perusahaan (id_p, nama, alamat) VALUES
('P01', 'Kantor Pusat', NULL),
('P02', 'Cabang Bekasi', NULL);
SELECT * FROM Perusahaan;
```
#### *Output Tabel Perusahaan :*
![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/1.png)


### *Script SQL berdasarkan Tabel Departemen*
```sql
CREATE TABLE Departemen(
id_dept VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
id_p VARCHAR(10) NOT NULL,
manajer_nik VARCHAR(10) DEFAULT NULL
);

INSERT INTO Departemen (id_dept, nama, id_p, manajer_nik) VALUES
('D01', 'Produksi', 'P02', 'N01'),
('D02', 'Marketing', 'P01', 'N03'),
('D03', 'RnD', 'P02', NULL),
('D04', 'Logistik', 'P02', NULL);
SELECT * FROM Departemen;
```
#### *Output Tabel Departemen :*
![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/2.png)


### *Script SQL berdasarkan Tabel Karyawan*
```sql
CREATE TABLE Karyawan(
nik VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
id_dept VARCHAR(10) NOT NULL,
sup_nik VARCHAR(10) DEFAULT NULL
);

INSERT INTO Karyawan (nik, nama, id_dept, sup_nik) VALUES
('N01', 'Ari', 'D01', NULL),
('N02', 'Dina', 'D01', NULL),
('N03', 'Rika', 'D03', NULL),
('N04', 'Ratih', 'D01', 'N01'),
('N05', 'Riko', 'D01', 'N01'),
('N06', 'Dani', 'D02', NULL),
('N07', 'Anis', 'D02', 'N06'),
('N08', 'Dika', 'D02', 'N06');
SELECT * FROM Karyawan;
```
#### *Output Tabel Karyawan :*
![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/3.png)


### *Script SQL berdasarkan Tabel Project*
```sql
CREATE TABLE Project(
id_proj VARCHAR(10) PRIMARY KEY,
nama VARCHAR(45) NOT NULL,
tgl_mulai DATETIME,
tgl_selesai DATETIME,
status TINYINT(1)
);

INSERT INTO Project (id_proj, nama, tgl_mulai, tgl_selesai, status) VALUES
('PJ01', 'A', '2019-01-10', '2019-03-10', '1'),
('PJ02', 'B', '2019-02-15', '2019-04-10', '1'),
('PJ03', 'C', '2019-03-21', '2019-05-10', '1');
SELECT * FROM Project;
```
#### *Output Tabel Project :*
![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/4.png)


### *Script SQL berdasarkan Tabel Project Detail*
```sql
CREATE TABLE Project_detail(
id_proj VARCHAR(10) NOT NULL,
nik VARCHAR(10) NOT NULL
);

INSERT INTO Project_detail (id_proj, nik) VALUES
('PJ01', 'N01'),
('PJ01', 'N02'),
('PJ01', 'N03'),
('PJ01', 'N04'),
('PJ01', 'N05'),
('PJ01', 'N07'),
('PJ01', 'N08'),
('PJ02', 'N01'),
('PJ02', 'N03'),
('PJ02', 'N05'),
('PJ03', 'N03'),
('PJ03', 'N07'),
('PJ03', 'N08');
SELECT * FROM Project_detail;
```
#### *Output Tabel Project Detail :*
![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/5.png)


### Menampilkan nama Manajer tiap Departemen
**Script :**

```sql
Select Departemen.nama AS Departemen, Karyawan.nama AS Manajer
FROM Departemen
LEFT JOIN Karyawan ON Karyawan.nik = Departemen.manajer_nik;
```

**Output :**

![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/6.png)

### Menampilkan nama Supervisor tiap Karyawan
**Script :**

```sql
SELECT Karyawan.nik, Karyawan.nama, Departemen.nama AS Departemen, Supervisor.nama AS Supervisor
FROM Karyawan
LEFT JOIN Karyawan AS Supervisor ON Supervisor.nik = Karyawan.sup_nik
LEFT JOIN Departemen ON Departemen.id_dept = Karyawan.id_dept;
```

**Output :**

![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/7.png)

### Menampilkan daftar Karyawan yang bekerja pada Project A
**Script :**

```sql
SELECT Karyawan.nik, Karyawan.nama
FROM Karyawan
JOIN Project_detail ON Project_detail.nik = Karyawan.nik
JOIN Project ON Project.id_proj = Project_detail.id_proj
WHERE Project.nama = 'A';
```

**Output :**

![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/8.png)


## Latihan Praktikum 6

### 1. Departemen apa saja yang terlibat dalam tiap-tiap Project
**Script :**

```sql
SELECT Project.nama AS Project, GROUP_CONCAT(Departemen.nama) AS Departemen
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
GROUP BY Project.id_proj;
```

**Output :**

![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/9.png)

> **Keterangan** : Menampilkan Departemen yang terlibat tiap Project.

### 2. Jumlah Karyawan tiap Departemen yang bekerja pada tiap-tiap project
**Script :**

```sql
SELECT Project.nama AS Project, Departemen.nama AS Departemen, COUNT(*) AS 'Jumlah Karyawan'
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
GROUP BY Project.id_proj, Departemen.id_dept;
```

**Output :**

![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/10.png)

> **Keterangan** : Menampilkan jumlah Karyawan yang bekerja pada tiap project.

### 3. Ada berapa Project yang sedang dikerjakan oleh Departemen *RnD*? *(ket: project berjalan adalah yang statusnya 1)*
**Script :**

```sql
SELECT COUNT(*) AS 'Jumlah Project'
FROM Project
INNER JOIN Project_detail ON Project.id_proj = Project_detail.id_proj
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
INNER JOIN Departemen ON Karyawan.id_dept = Departemen.id_dept
WHERE Departemen.nama = 'RnD' AND Project.status = 1;
```

**Output :**

![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/11.png)

> **Keterangan** : Menampilkan jumlah Project yang dikerjakan oleh Departemen RnD.

### 4. Berapa banyak Project yang sedang dikerjakan oleh Ari?
**Script :**

```sql
SELECT COUNT(*) AS 'Jumlah Project'
FROM Project_detail
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
WHERE Karyawan.nama = 'Ari' AND Project_detail.id_proj IN (SELECT id_proj FROM Project WHERE status = 1);
```

**Output :**

![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/12.png)

> **Keterangan** : Menampilkan jumlah Project yang dikerjakan oleh Karyawan bernama Ari.

### 5. Siapa saja yang mengerjakan Project B?
**Script :**

```sql
SELECT Karyawan.nama
FROM Project_detail
INNER JOIN Karyawan ON Project_detail.nik = Karyawan.nik
WHERE Project_detail.id_proj IN (SELECT id_proj FROM Project WHERE nama = 'B');
```

**Output :**

![image](https://github.com/AnggitaRisqiNC/Praktikum-6/blob/main/screenshot/13.png)

> **Keterangan** : Menampilkan nama-nama Karyawan yang mengerjakan Project B.

## Finish