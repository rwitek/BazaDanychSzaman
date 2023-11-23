# BazaDanychSzaman

Baza danych Szaman to ośrodek zdrowia w której przechowywane są informacje takie jak: wizyty pacjentów, lekarze, choroby, ...
Poniżej jest zapisany kod tworzący bazę danych

-- Instrukcja tworząca bazę
CREATE DATABASE Szaman
GO
USE Szaman
GO
-- Instrukcje tworzące tabele
CREATE TABLE medykamenty
(
id_lekarstwa int PRIMARY KEY NOT NULL,
nazwa_lekarstwa varchar(20) NOT NULL,
opis_lekarstwa varchar(25) NOT NULL,
dawkowanie varchar(30) NOT NULL
)
CREATE TABLE jednostka_chorobowa
(
id_choroby int PRIMARY KEY NOT NULL,
nazwa_choroby varchar(25) NOT NULL,
krótki_opis varchar(80) NOT NULL,
id_lekarstwa int NOT NULL,
CONSTRAINT FK_id_lekarstwa FOREIGN KEY (id_lekarstwa) REFERENCES medykamenty(id_lekarstwa)
)
CREATE TABLE pacjenci
(
id_pacjenta int PRIMARY KEY NOT NULL,
imie varchar(25) NULL,
nazwisko varchar(30) NOT NULL,
adres varchar(40) NOT NULL
)
CREATE TABLE specjalizacje
(
id_specjalizacji int PRIMARY KEY NOT NULL,
nazwa varchar(40) NOT NULL
)
CREATE TABLE lekarze
(
id_lekarza int PRIMARY KEY NOT NULL,
imie varchar(25) NULL,
nazwisko varchar(30) NOT NULL,
id_specjalizacji int NOT NULL,
CONSTRAINT FK_specjalizacje FOREIGN KEY (id_specjalizacji) REFERENCES
specjalizacje(id_specjalizacji)
ON UPDATE CASCADE
)
CREATE TABLE wizyty_pacjentów
(
id_wizyty int PRIMARY KEY NOT NULL,
id_pacjenta int NOT NULL,
id_lekarza int NOT NULL,
id_choroby int NULL,
data_wizyty date NOT NULL,
CONSTRAINT data_przyszla CHECK (data_wizyty <= GetDate()),
CONSTRAINT FK_id_pacjenta FOREIGN KEY (id_pacjenta) REFERENCES pacjenci(id_pacjenta)
ON UPDATE CASCADE,
CONSTRAINT FK_id_lekarza FOREIGN KEY (id_lekarza) REFERENCES lekarze(id_lekarza)
ON UPDATE CASCADE,
CONSTRAINT FK_id_choroby FOREIGN KEY (id_choroby) REFERENCES
jednostka_chorobowa(id_choroby)
ON UPDATE CASCADE
)
--Dane dołączane do tabel
INSERT INTO medykamenty
VALUES (1,'Detonal', 'Na kaszel suchy','2 razy dziennie'),
(2,'Gynoxin', 'Przeciw wirusowy','1 raz na dwa dni'),
(3,'Driptane','Antybakteryjny', '7 razy w ciągu tygodnia'),
(4,'Karbis', 'Przeciwko grypie','5 razy w ciągu tygodnia'),
(5,'Heviran', 'Na kaszel mokry','1 raz dziennie'),
(6,'Ocusept', 'Krople antybiotykowe','2 razy co trzy dni')

INSERT INTO jednostka_chorobowa
VALUES (1,'Grypa', 'Choroba wirusowa, powoduje gorączkę oraz ogólne osłabienie 
organizmu',4),
(2,'Zapalenie oskrzeli', 'Infekcja dróg oddechowych, powoduje silny kaszel',1),
(3,'Covid- 19', 'Choroba koronawirusowa, charakteryzuje go utrata węchu i smaku',2),
(4,'Zapalenie płuc', 'Choroba infekcyjno-bakteryjna, powoduje trudności w oddychaniu oraz 
kaszel',3),
(5,'Ospa', 'Choroba zakaźna, powoduje charakterystyczną wysypkę',2),
(6,'Zapalenie spojówek', 'Choroba bakteryjna, powoduje swędzenie oraz pieczenie oczu',2)

INSERT INTO pacjenci
VALUES (1,'Piotr','Zalewski','Smoleń 10'),
(2,'Krystian','Nowak','Kraków ul. Czekoladowa 365'),
(3,'Stanisław','Kowalski','Olkusz ul. Mickiewicza 21'),
(4,'Elżbieta','Wójcik','Rybik ul. Dębowa 4'),
(5,'Cezary','Woźniak','Chełm 224'),
(6,'Karol','Lewandowski','Kaliś 22'),
(7,'Jan','Mazur','Warszawa ul. Centralna 39'),
(8,'Natalia','Kaczmarska','Gdańsk ul. Atlantycka 300'),
(9,'Zuzanna','Borkowska','Szczecin ul. Pomorska 20')

INSERT INTO specjalizacje
VALUES (1,'Medycyna rodzinna'),
(2,'Epidemiologia'),
(3,'Choroby zakaźne'),
(4,'Okulistyka')

INSERT INTO lekarze
VALUES (1,'Paulina','Siasta',1),
(2,'Konrad','Tomaszewski',2),
(3,'Krystyna','Żurek',3),
(4,'Karolina','Przybylska',4)

INSERT INTO wizyty_pacjentów
VALUES (1,2,3,1,'2022-03-16'),
(2,2,4,6,'2022-05-10'),
(3,5,1,4,'2022-01-25'),
(4,1,4,6,'2022-01-03'),
(5,9,1,NULL,'2022-12-13'),
(6,3,1,2,'2022-01-20'),
(7,8,2,3,'2022-10-24'),
(8,7,3,5,'2022-02-10'),
(9,6,1,1,'2022-04-06'),
(10,5,2,3,'2022-10-30'),
(11,4,4,NULL,'2022-09-12'),
(12,8,3,5,'2022-09-17'),
(13,2,1,2,'2022-06-14'),
(14,7,1,4,'2022-12-29'),
(15,6,2,3,'2022-02-26'),
(16,4,3,1,'2022-11-15'),
(17,5,3,5,'2022-07-21'),
(18,2,2,NULL,'2022-06-10'),
(19,3,4,6,'2022-08-10'),
(20,2,1,2,'2022-02-10'),
(21,4,1,1,'2022-04-11'),
(22,1,2,3,'2022-11-11'),
(23,6,1,NULL,'2022-03-28'),
(24,2,3,5,'2022-12-13')
