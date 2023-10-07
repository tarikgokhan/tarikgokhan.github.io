

# T-SQL Kavramları


T-SQL Veritabanı İşlemleri Aşağıdaki Gruplara Ayrılır.

# DDL, veritabanı şemalarını ve yapılarını tanımlamak için kullanılır. DDL komutları şunları içerir:

### CREATE: Yeni bir tablo, veritabanı, indeks vb. oluşturur.
### ALTER: Varolan bir tablonun yapısını değiştirir.
### DROP: Varolan bir tablo, veritabanı, indeks vb. siler.
### TRUNCATE: Bir tablonun tüm verilerini siler fakat yapısını korur.
### DML (Data Manipulation Language)

# DML, veritabanındaki verileri işlemek için kullanılır. DML komutları şunları içerir:

### SELECT: Veritabanından veri çeker.
### INSERT: Yeni veri ekler.
### UPDATE: Varolan veriyi günceller.
### DELETE: Varolan veriyi siler.
### DCL (Data Control Language)

# DCL, veritabanı erişim kontrolü ve yetkilendirmeyi yönetir.

### GRANT: Kullanıcılara belirli yetkiler verir.
### REVOKE: Kullanıcılardan belirli yetkileri alır.


# TCL (Transaction Control Language) 

TCL, veritabanı işlemlerini kontrol etmek için kullanılır.

### COMMIT: Tüm işlemleri onaylar ve kalıcı hale getirir.
### ROLLBACK: Son COMMIT'e kadar olan değişiklikleri geri alır.
### SAVEPOINT: İşlemlerin belirli bir noktasını kaydeder.
### SET TRANSACTION: İşlem özelliklerini ayarlar.

Bu komutlardan Bazılarını örneklerle açıklayalım.

# DDL İşlemleri 

### Veritabanı Oluşturma
Create Komutu ile veritabanı oluşturulur.

```sql
CREATE DATABASE Nortwind;
```

### Veritabanı Seçme

Use Komutu Veritabanını Seçer

```sql
USE Nortwind;
```

### Veritabanı Silme

DROP Komutu Veritabanını siler.

```sql
DROP DATABASE Nortwind;
```


### Tablo Oluşturma

Veritabanında yeni bir tablo oluşturmak için aşağıdaki komut kullanılır.

```sql
CREATE TABLE Kullanici (
    ID INT PRIMARY KEY,
    Adi VARCHAR(50),
    Soyadi VARCHAR(50)
);
```

# DML İşlemleri 

### Tabloya Satır Ekleme

INSERT INTO  Komutu Veri ekler.

```sql
INSERT INTO TabloAdi (ID, Adi, Soyadi)
VALUES (1, 'Ali', 'Veli');
```

#### Tablodan Satır Güncelleme

UPDATE Komutu Tablo üzerinde belirlediğiniz kriterlerdeki satırları günceller.

```sql
UPDATE TabloAdi
SET Adi = 'Ahmet'
WHERE ID = 1;
```

### Tablodan Satır Silme

DELETE Komutu Tablodan belirlediğiniz kriterlerdeki satırları siler.

```sql
DELETE FROM Kullanici
WHERE ID = 1;
```


SELECT  Veriyi sorgular.

```sql
SELECT * FROM Kullanici;
```

WHERE Filtre ekler.

```sql
SELECT * FROM Kullanici
WHERE Adi = 'Ali';
```


GROUP BY Veriyi gruplar.


```sql
SELECT Adi, COUNT(*)
FROM Kullanici
GROUP BY Adi;
```

### Join İşlemleri

INNER JOIN : İki tabloyu birleştirir.

```sql
SELECT * FROM Tablo1
INNER JOIN Tablo2 ON Tablo1.ID = Tablo2.ID;
```


LEFT JOIN

Sol tabloyu temel alır.

```sql
SELECT * FROM Tablo1
LEFT JOIN Tablo2 ON Tablo1.ID = Tablo2.ID;
```


### Fonksiyonlar ve Prosedürler

COUNT()  Eleman sayar.

```sql
SELECT COUNT(*) FROM TabloAdi;
```


SUM()  Belirtilen sütundaki sayıları toplar ve toplam sayı olarak gösterir.

```sql
SELECT SUM(SutunAdi) FROM TabloAdi;
```


### İndeksler ve Kısıtlamalar

PRIMARY KEY  Birincil anahtar oluşturur. Aşağıdaki komut satırı ile bir tabloya primarykey eklendiğini görüyoruz.

```sql
ALTER TABLE Kullanici ADD PRIMARY KEY (ID);
```

FOREIGN KEY  Yabancı anahtar oluşturur.

```sql

ALTER TABLE TabloAdi
ADD FOREIGN KEY (ID) REFERENCES DigerTablo(ID);

```

### Transactionlar 
BEGIN TRANSACTION Transaction Başlatılır. 

```sql
BEGIN TRANSACTION;
```

Begin Transaction dan sonra tablolarda yapılan veri ekleme ve güncelleme işlemleri tablolarda geçerli olmaz. Geçerli olma hali Commit komutu çalıştırıldığında olur.  Yani birkaç tabloya birden veri ekleme güncelleme işlemi yapılır ve bu işlemler ya kommit edilir yada rollback edilir. Commit edildiğinde tablolarda yapılan değişiklikler geçerli olurken rollback edildiğinde tablolarda yapılan işlemler geçersiz olur.

```sql
COMMIT
```

```sql
ROLLBACK  Transaction ı geri alır ve yapılan işlemler geçersiz olur.
```