zad 1:

CREATE TABLE pracownik (
    -> id_pracownik int PRIMARY KEY NOT NULL  AUTO_INCREMENT,
    -> imie varchar(40) NOT NULL,
    -> nazwisko varchar(60) NOT NULL,
    -> data_urodzenia date NOT NULL);

 INSERT INTO pracownik VALUES (default, "Adam", "Zdrojkowski", "2015-02-10");
 INSERT INTO pracownik VALUES (default, "Lebron", "James", "1982-12-20");
 INSERT INTO pracownik VALUES (default, "Robert", "Lewandowski", "1975-01-02");

 UPDATE pracownik SET data_urodzenia = "1973-03-25" WHERE id_pracownik = 3;

 zad2:

 CREATE TABLE zadanie ( id_zadania int PRIMARY KEY AUTO_INCREMENT, nazwa_zadania varchar(150) NOT NULL, priorytet enum('normalny', 'wysoki', 'niski'), opis text, pracownik int, foreign key (pracownik) references pracownik(id_pracownik) on delete set null);

alter table zadanie alter priorytet set default 'normalny';

INSERT INTO zadanie VALUES(default, 'posprzatac', 'niski', 'sprzatanie sali 23', 1),
    -> (default, 'rozmowa z klientem', default, 'rozmowa z klientem w sprawie kontraktu', 3),
    -> (default, 'wyplata pracownikom pieniedzy', 'wysoki', default, 2);

zad3:
CREATE TABLE projekt(
    -> id_projektu int PRIMARY KEY AUTO_INCREMENT,
    -> nazwa_projektu varchar(150),
    -> data_rozpoczecia date,
    -> data_zakonczenia date NULL);

ALTER TABLE projekt ADD COLUMN menadzer_projektu int;
ALTER TABLE projekt ADD FOREIGN KEY(menadzer_projektu) REFERENCES pracownik(id_pracownik);

INSERT INTO projekt VALUES( default, 'organizacja imprezy', '2025-10-28', default, 3), (default, 'wykonanie programu dla klienta', '2025-08-10', '2025-09-10', 2);

ALTER TABLE zadanie ADD COLUMN projekt int;
ALTER TABLE zadanie ADD FOREIGN KEY(projekt) REFERENCES projekt(id_projektu) ON DELETE CASCADE;

UPDATE zadanie SET projekt = 1 WHERE id_zadania = 1;
UPDATE zadanie SET projekt = 2 WHERE id_zadania = 2;

zad4:
 CREATE TABLE sprint(
    -> id_sprintu int PRIMARY KEY AUTO_INCREMENT,
    -> numer_sprintu int CHECK (numer_sprintu >= 0),
    -> data_rozpoczecia date,
    -> data_zakonczenia date);

ALTER TABLE zadanie ADD FOREIGN KEY(sprint) REFERENCES sprint(id_sprintu) ON DELETE SET NULL;

INSERT INTO sprint VALUES(default, 3, '2025-10-10', '2025-10-28');
UPDATE zadanie SET sprint = 1 WHERE id_zadania = 2;
UPDATE zadanie SET sprint = 1 WHERE id_zadania = 3;

zad5:
CREATE TABLE status(
    -> id_statusu int PRIMARY KEY AUTO_INCREMENT,
    -> nazwa_statusu varchar(20));

INSERT INTO status VALUES(default, 'gotowe'), (default, 'rozpoczete'), (default, 'w trakcie');

