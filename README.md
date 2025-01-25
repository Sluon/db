# db


--CREATE DATABASE Algebra;


USE Algebra;

--CREATE TABLE Polaznici
--(
--	Sifra int PRIMARY KEY,
--	Sifra int UNIQUE NOT NULL CHECK(Sifra BETWEEN 1 AND 1000),
--	OIB int unique,
--	Ime nvarchar(50) NOT NULL,
--	Prezime nvarchar(50) NOT NULL,
--	Adresa nvarchar(700) NULL,
--	CONSTRAINT CheckSifra CHECK(Sifra BETWEEN 1 AND 1000) --explicit
--);


--ALTER TABLE Polaznici
--ADD BrojTelefona int; 

--ALTER TABLE Polaznici
--ALTER COLUMN BrojTelefona varchar(20);

--ALTER TABLE Polaznici
--DROP COLUMN BrojTelefona;

--DROP TABLE Polaznici;

--USE Algebra;
--DROP DATABASE priv;


--USE Algebra;

--CREATE TABLE Seminari
--(
--	Sifra int PRIMARY KEY,
--	Naziv nvarchar(250)
--);

CREATE TABLE Upisi
(
	Sifra int IDENTITY(1,1) PRIMARY KEY,
	SifraPolaznika int FOREIGN KEY REFERENCES Polaznici(Sifra),
	SifraSeminara int FOREIGN KEY REFERENCES Seminari(Sifra)
)

------



begin transaction pizdun

--insert into Polaznici
--(Sifra, Ime, Prezime)
--values
--(7, 'k', 'n'),
--(8, 'f', 'g'),
--(9, '+', 'đ')
--;

delete Seminari;

drop table Upisi;
drop table Seminari;
drop table Polaznici;

--commit transaction
rollback tran pizdun

------

-- 1. Kreiranje baze podataka
-- Sintaksa: CREATE DATABASE NazivBazePodataka

CREATE DATABASE Algebra;

USE Algebra;

-- 2. Kreiranje tablice
/* Sintaksa:
	CREATE TABLE NazivTablice
	(
		NazivStupca TipStupca,
		NazivStupca TipStupca,
		NazivStupca TipStupca
	)
*/
CREATE TABLE Polaznici 
(
	Sifra	int PRIMARY KEY CHECK(Sifra BETWEEN 1 AND 1000),
	--Sifra	int UNIQUE NOT NULL CHECK(Sifra BETWEEN 1 AND 1000),
	OIB		int UNIQUE,
	Ime		nvarchar(50) NOT NULL,
	Prezime	nvarchar(50) NOT NULL,
	Adresa	nvarchar(200) null
	--CONSTRAINT CheckSifra CHECK(Sifra BETWEEN 1 AND 1000)
);

--3. Promjena tablice, dodavanje novog atributa (stupac)
/* Sintaksa:
	ALTER TABLE NazivTablice 
		ADD NazivStupca TipStupca
*/

ALTER TABLE Polaznici
ADD BrojTelefona int;

-- 4. Promjena tablice, promjena atributa (stupca)
/*
	ALTER TABLE NazivTablice
		ALTER COLUMN NazivStupca TipStupca
*/

ALTER TABLE Polaznici
ALTER COLUMN BrojTelefona varchar(20);

-- 5. Brisanje stupca
/* Sintaksa:
	ALTER TABLE NazivTablice
		DROP COLUMN NazivStupca
*/

ALTER TABLE Polaznici
DROP COLUMN BrojTelefona;

-- 6. Brisanje tablice
/* Sintaksa:
	DROP TABLE NazivTablice
*/

DROP TABLE Polaznici;

-- 7. Brisanje cijele baze podataka
/* Sintaksa:
	DROP DATABASE NazivBazePodataka
*/
USE master;
DROP DATABASE Algebra;

---
-- 1. NULL i NOT NULL polja
-- 2. CHECK Constraint (ograničenje) - eksplicitno
-- 3. CHECK ograničenje i UNIQUE - implicitno
-- 4. Primarni ključ

CREATE TABLE Polaznici 
(
	Sifra	int PRIMARY KEY CHECK(Sifra BETWEEN 1 AND 1000),
	OIB		int UNIQUE,
	Ime		nvarchar(50) NOT NULL,
	Prezime	nvarchar(50) NOT NULL,
	Adresa	nvarchar(200) null
);

CREATE TABLE Seminari
(
	Sifra	int PRIMARY KEY,
	Naziv	nvarchar(250)
);

-- 5. Foreign key -> vanjski/strani ključ

CREATE TABLE Upisi
(
	Sifra			int PRIMARY KEY,
	SifraPolaznika	int FOREIGN KEY REFERENCES Polaznici(Sifra),
	SifraSeminara	int FOREIGN KEY REFERENCES Seminari(Sifra)
);

TRUNCATE TABLE Polaznici;

INSERT INTO Polaznici VALUES
(10, 2222222, 'Pero', 'Perić', 'Vrtna 10a');

INSERT INTO Polaznici (Sifra, Ime, Prezime) VALUES
(15, 'Marko', 'Marković');

INSERT INTO Polaznici (Sifra, Ime, Prezime, OIB) VALUES
(25, 'Ana', 'Marković', 4343);

INSERT INTO Polaznici (Sifra, Ime, Prezime, OIB) VALUES
(2, 'Ivo', 'Vidović', 123),
(3, 'Luka', 'Vidović', 124),
(4, 'Branko', 'Vidović', 125);

INSERT INTO Seminari VALUES
(1, 'modul 1'),
(2, 'modul 2');

INSERT INTO Upisi VALUES 
(1, 2, 1),
(2, 2, 2),
(3, 3, 1);

BEGIN TRANSACTION

DELETE FROM Upisi;
DELETE FROM Seminari;
DELETE FROM Polaznici; 

DROP TABLE Upisi;
DROP TABLE Seminari;
DROP TABLE Polaznici;

--ROLLBACK TRANSACTION
COMMIT TRANSACTION

CREATE TABLE Polaznici 
(
	Sifra	int IDENTITY(1,1) PRIMARY KEY,
	OIB		int,
	Ime		nvarchar(50) NOT NULL,
	Prezime	nvarchar(50) NOT NULL,
	Adresa	nvarchar(200) null
);

CREATE TABLE Seminari
(
	Sifra	int PRIMARY KEY,
	Naziv	nvarchar(250)
);

CREATE TABLE Upisi
(
	Sifra			int IDENTITY(1,1) PRIMARY KEY,
	SifraPolaznika	int FOREIGN KEY REFERENCES Polaznici(Sifra),
	SifraSeminara	int FOREIGN KEY REFERENCES Seminari(Sifra)
);

INSERT INTO Polaznici VALUES
(2222222, 'Pero', 'Perić', 'Vrtna 10a');

INSERT INTO Polaznici (Ime, Prezime) VALUES
('Marko', 'Marković');

INSERT INTO Polaznici (Ime, Prezime, OIB) VALUES
('Ana', 'Marković', 4343),
('Ivo', 'Vidović', 123),
('Luka', 'Vidović', 124),
('Branko', 'Vidović', 125);

INSERT INTO Seminari VALUES
(1, 'Modul C#/.NET'),
(2, 'Modul Baze podataka');

INSERT INTO Upisi VALUES 
(3, 1),
(4, 1),
(4, 2),
(5, 1),
(5, 2);

UPDATE Polaznici
SET Adresa = NULL;

UPDATE Polaznici
SET Adresa = 'Vrtna 30a'
WHERE Sifra = 3;

UPDATE Polaznici
SET Adresa = 'Uska 23'
WHERE Prezime = 'Vidović';

UPDATE Polaznici
SET OIB = 12321321, Adresa = 'Cvjetni trg'
WHERE Ime = 'Ana';

BEGIN TRAN 
DELETE FROM Upisi;
DELETE FROM Polaznici WHERE Prezime = 'Marković' AND Ime = 'Ana';
--DELETE FROM Polaznici WHERE Sifra BETWEEN 5 AND 8;
--DELETE FROM Polaznici WHERE Prezime = 'Marković' OR Prezime = 'Vidović';
--DELETE FROM Polaznici WHERE Prezime IN ('Marković', 'Vidović');
ROLLBACK TRAN

SELECT *
FROM Polaznici;

SELECT Sifra, Ime, Prezime
FROM Polaznici;

SELECT Sifra, Ime
FROM Polaznici
WHERE Prezime = 'Marković';

SELECT *
FROM Polaznici
WHERE OIB > 2;

SELECT *
FROM Polaznici
WHERE Sifra BETWEEN 5 AND 7;

SELECT *
FROM Polaznici
WHERE (Sifra BETWEEN 5 AND 7) OR (OIB > 2 AND Prezime = 'Marković');

select * from polaznici;
select * from seminari;
select * from upisi;

select * 
from upisi 
inner join polaznici on upisi.SifraPolaznika = Polaznici.Sifra
inner join Seminari on upisi.SifraSeminara = Seminari.Sifra;

select Polaznici.Sifra, Polaznici.Ime, Polaznici.Prezime, Polaznici.Adresa, Seminari.Sifra, Seminari.Naziv
from upisi 
inner join polaznici on upisi.SifraPolaznika = Polaznici.Sifra
inner join Seminari on upisi.SifraSeminara = Seminari.Sifra;

select Polaznici.Sifra as ID_polaznika, Polaznici.Ime, Polaznici.Prezime, Polaznici.Adresa, 
	Seminari.Sifra as ID_seminara, Seminari.Naziv
from upisi 
inner join polaznici on upisi.SifraPolaznika = Polaznici.Sifra
inner join Seminari on upisi.SifraSeminara = Seminari.Sifra;

select Polaznici.Sifra as ID_polaznika, Polaznici.Ime, Polaznici.Prezime, Polaznici.Adresa, 
	Seminari.Sifra as ID_seminara, Seminari.Naziv
from upisi 
inner join polaznici on upisi.SifraPolaznika = Polaznici.Sifra
inner join Seminari on upisi.SifraSeminara = Seminari.Sifra
order by polaznici.Ime asc, polaznici.oib desc

select p.Sifra as ID_polaznika, p.Ime, p.Prezime, p.Adresa, 
	s.Sifra as ID_seminara, s.Naziv
from upisi u
inner join polaznici p on u.SifraPolaznika = p.Sifra
inner join Seminari s on u.SifraSeminara = s.Sifra
order by p.Ime asc, p.oib desc

------

