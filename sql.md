

# T-SQL Kavramları


T-SQL Veritabanı İşlemleri Aşağıdaki Gruplara Ayrılır.

# DDL Komutları  

Bu komutlar veritabanı şemalarını ve yapılarını tanımlamak için kullanılır. DDL komutları şunları içerir:

### CREATE: Yeni bir tablo, veritabanı, indeks vb. oluşturur.

Create Komutu ile bir nesne oluşturulur. CREATE DATABASE bir veritabanı oluşturur.

```sql
CREATE DATABASE Nortwind;
```

Veritabanında yeni bir tablo oluşturmak için aşağıdaki komut kullanılır.

```sql
CREATE TABLE Kullanici (
    ID INT PRIMARY KEY,
    Adi VARCHAR(50),
    Soyadi VARCHAR(50)
);
```

### ALTER: Varolan bir tablonun yapısını değiştirir.

PRIMARY KEY  Birincil anahtar oluşturur. Aşağıdaki komut satırı ile bir tabloya primarykey eklendiğini görüyoruz.

```sql
ALTER TABLE Kullanici ADD PRIMARY KEY (ID);
```

FOREIGN KEY  Yabancı anahtar oluşturur.

```sql

ALTER TABLE TabloAdi
ADD FOREIGN KEY (ID) REFERENCES DigerTablo(ID);
```


### DROP: Varolan bir tablo, veritabanı, indeks vb. siler.

DROP Komutu bir nesnesi siler DROP DATABASE ile bir veritabanı silirken  DROP TABLE Users ile bir tabloyu silebilirsiniz.

```sql
DROP DATABASE MyDB;
```
DROP TABLE komutu ile bir veritabanı içerisindeki tabloyu siler. Bu tabloyu ve içerisindeki verilerle herşeyi siler.

```sql
DROP TABLE Users;
```

### TRUNCATE 

Bir tablonun tüm verilerini istatistiklerini siler ve indexlerini sıfırlar.


# DML Komutları 

veritabanındaki verileri işlemek için kullanılır. DML komutları şunları içerir:

### SELECT:

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


### INSERT: Yeni veri ekler.

INSERT INTO  Komutu Veri ekler.

```sql
INSERT INTO TabloAdi (ID, Adi, Soyadi)
VALUES (1, 'Ali', 'Veli');
```


### UPDATE: Varolan veriyi günceller.

UPDATE Komutu Tablo üzerinde belirlediğiniz kriterlerdeki satırları günceller.

```sql
UPDATE TabloAdi
SET Adi = 'Ahmet'
WHERE ID = 1;
```

### DELETE: Varolan veriyi siler.

DELETE Komutu Tablodan belirlediğiniz kriterlerdeki satırları siler.

```sql
DELETE FROM Kullanici
WHERE ID = 1;
```



# DCL Komutları 

DCL Komutları veritabanı erişim kontrolü ve yetkilendirmeyi yönetir.

### GRANT

GRANT komutu, kullanıcılara veya rollerine belirli izinler verir. Örneğin, employees tablosu üzerinde SELECT izni vermek için aşağıdaki komutu kullanabilirsiniz:

```sql
GRANT SELECT ON employees TO some_user;
```

Bu komut, some_user adlı kullanıcının employees tablosu üzerinde sorgu yapabilmesini sağlar.

### REVOKE: Kullanıcılardan belirli yetkileri alır.

REVOKE komutu, daha önce verilmiş olan izinleri geri alır. Örneğin, some_user adlı kullanıcının employees tablosu üzerindeki SELECT iznini geri almak için aşağıdaki komutu kullanabilirsiniz:

sql
```sql
REVOKE SELECT ON employees FROM some_user;
```

Bu komut, some_user adlı kullanıcının employees tablosu üzerinde sorgu yapabilme yeteneğini kaldırır.



# TCL (Transaction Control Language) 

TCL, veritabanı işlemlerini kontrol etmek için kullanılır.

### COMMIT: Tüm işlemleri onaylar ve kalıcı hale getirir.
### ROLLBACK: Son COMMIT'e kadar olan değişiklikleri geri alır.
### SAVEPOINT: İşlemlerin belirli bir noktasını kaydeder.
### SET TRANSACTION: İşlem özelliklerini ayarlar.




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



### Transactionlar 
BEGIN TRANSACTION Transaction Başlatılır. 

```sql
BEGIN TRANSACTION;
```

Begin Transaction dan sonra tablolarda yapılan veri ekleme ve güncelleme işlemleri tablolarda geçerli olmaz. Geçerli olma hali Commit komutu çalıştırıldığında olur.  Yani birkaç tabloya birden veri ekleme güncelleme işlemi yapılır ve bu işlemler ya kommit edilir yada rollback edilir. Commit edildiğinde tablolarda yapılan değişiklikler geçerli olurken rollback edildiğinde tablolarda yapılan işlemler geçersiz olur.

```sql
COMMIT
```

ROLLBACK  Transaction ı geri alır ve yapılan işlemler geçersiz olur.

```sql
ROLLBACK 
```