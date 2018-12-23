# Incapatanarea 

Costache Radu
Grupa 253
Prof. Coordonator: Cristiana Popescu

## Scenariu 

In anul 2077, refuzul oamenilor de a accepta schimbari necesare este mai daunator societatii ca niciodata. Desi ultimii zeci de ani au fost o dovada clara ca unele schimbari sunt necesare pentru bunastarea tuturor, oamenii refuza sa incerce sa fie deschisi ideilor noi. De aceea, incapatanarea este declarata boala. 
Se doreste crearea unei baze de date in care sa fie stocate informatii despre pacientii internati in azile speciale in care se trateaza aceasta boala mentala, ce medici ii tratateaza in functie de cat de avansata este boala, ce tratamente le sunt prescrise si ce medicamente. 

## ERD & Mapare
![Mapare](http://costin.dev.eiddew.com/imgdb/mapares.jpg)
![ERD](http://costin.dev.eiddew.com/imgdb/diagram.jpg)



# Crearea tabelelor

### PACIENTI
```sql
CREATE TABLE PACIENTI
(
    id INT PRIMARY KEY AUTO_INCREMENT,
    id_camera INT,
    nume VARCHAR(255) NOT NULL,
    data_internare DATETIME NOT NULL,
    sex TINYINT DEFAULT 2 NOT NULL
);
```

### CAMERE
```sql
create table CAMERE
(
	id int auto_increment primary key,
	id_complex int null,
	nr_paturi int default '2' not null
);
```

### COMPLEXURI
```sql
CREATE TABLE COMPLEXURI
(
    id INT PRIMARY KEY AUTO_INCREMENT,
    nume VARCHAR(255) NOT NULL,
    adresa VARCHAR(255) NOT NULL
);
```

### EXAMINARI
```sql
CREATE TABLE EXAMINARI
(
    id INT PRIMARY KEY AUTO_INCREMENT,
    id_pacient INT NOT NULL,
    data DATETIME NOT NULL
);
```


### REZULTATE
```sql
CREATE TABLE REZULTATE
(
    id INT PRIMARY KEY AUTO_INCREMENT,
    id_examinare INT NOT NULL,
    tip TINYINT DEFAULT 0 NOT NULL
);
```

### MEDICI
```sql
CREATE TABLE MEDICI
(
    id INT PRIMARY KEY AUTO_INCREMENT,
    id_rezultat INT NOT NULL,
    nume VARCHAR(255) NOT NULL,
    specializare VARCHAR(255) NOT NULL
);
```


### TRATAMENTE
```sql
CREATE TABLE TRATAMENTE
(
    id INT PRIMARY KEY AUTO_INCREMENT,
    id_medic INT NOT NULL,
    denumire VARCHAR(255) NOT NULL,
    comentarii TEXT,
    data_inceput DATETIME NOT NULL,
    data_sfarsit DATETIME NOT NULL
);
```
### MEDICAMENTE
```sql
CREATE TABLE MEDICAMENTE
(
    id INT PRIMARY KEY AUTO_INCREMENT,
    id_tratament INT NOT NULL,
    denumire VARCHAR(255) NOT NULL,
    cantitate INT NOT NULL,
    gramaj DECIMAL(3,1) NOT NULL
);
```

#### drop_table
```sql
create table drop_table
(
	id int null
)
;
```

# Actualizari ale structurii tabelelor 
```sql
ALTER TABLE PACIENTI
ADD CONSTRAINT PACIENTI_CAMERE_id_fk
FOREIGN KEY (id_camera) REFERENCES CAMERE (id);

ALTER TABLE CAMERE
ADD CONSTRAINT CAMERE_COMPLEXURI_id_fk
FOREIGN KEY (id_complex) REFERENCES COMPLEXURI (id);

ALTER TABLE EXAMINARI
ADD CONSTRAINT EXAMINARI_PACIENTI_id_fk
FOREIGN KEY (id_pacient) REFERENCES PACIENTI (id);

ALTER TABLE REZULTATE
ADD CONSTRAINT REZULTATE_EXAMINARI_id_fk
FOREIGN KEY (id_examinare) REFERENCES EXAMINARI (id);

ALTER TABLE MEDICI
ADD CONSTRAINT MEDICI_REZULTATE_id_fk
FOREIGN KEY (id_rezultat) REFERENCES REZULTATE (id);

ALTER TABLE TRATAMENTE
ADD CONSTRAINT TRATAMENTE_MEDICI_id_fk
FOREIGN KEY (id_medic) REFERENCES MEDICI (id);

ALTER TABLE MEDICAMENTE
ADD CONSTRAINT MEDICAMENTE_TRATAMENTE_id_fk
FOREIGN KEY (id_tratament) REFERENCES TRATAMENTE (id);


ALTER TABLE MEDICAMENTE MODIFY gramaj DECIMAL(3,1);
```
#### DROP 
```sql
DROP TABLE proiect.drop_table;
```

# Inserts
```sql
# insert into complexuri

INSERT INTO proiect.COMPLEXURI (nume, adresa) VALUES ('Spitalu 9', 'Pacii 2');
INSERT INTO proiect.COMPLEXURI (nume, adresa) VALUES ('Magheru ', 'Magheru 15');
INSERT INTO proiect.COMPLEXURI (nume, adresa) VALUES ('Ungheru', 'Ungheru 22');
INSERT INTO proiect.COMPLEXURI (nume, adresa) VALUES ('Grigore Alexandrescu', 'Splaiul 2');
INSERT INTO proiect.COMPLEXURI (nume, adresa) VALUES ('Marie Curie', 'Berceni 222');


# insert into camere

INSERT INTO proiect.CAMERE (id_complex, nr_paturi) VALUES (1, 2);
INSERT INTO proiect.CAMERE (id_complex, nr_paturi) VALUES (1, 2);
INSERT INTO proiect.CAMERE (id_complex, nr_paturi) VALUES (1, 2);
INSERT INTO proiect.CAMERE (id_complex, nr_paturi) VALUES (2, 2);
INSERT INTO proiect.CAMERE (id_complex, nr_paturi) VALUES (2, 2);


# insert into pacienti

INSERT INTO proiect.PACIENTI (id_camera, nume, data_internare, sex) VALUES (1, 'George George', '2017-12-19 22:51:12', 1);
INSERT INTO proiect.PACIENTI (id_camera, nume, data_internare, sex) VALUES (1, 'Marin Marin', '2017-12-18 22:57:00', 1);
INSERT INTO proiect.PACIENTI (id_camera, nume, data_internare, sex) VALUES (2, 'Andrei Andrei', '2017-12-17 22:58:43', 1);
INSERT INTO proiect.PACIENTI (id_camera, nume, data_internare, sex) VALUES (4, 'Maria Maria', '2017-12-16 23:02:33', 2);
INSERT INTO proiect.PACIENTI (id_camera, nume, data_internare, sex) VALUES (4, 'Alina Alina', '2017-12-16 23:03:11', 2);

#insert into examinari
INSERT INTO proiect.EXAMINARI (id_pacient, data) VALUES (1, '2017-12-19 22:51:12');
INSERT INTO proiect.EXAMINARI (id_pacient, data) VALUES (2, '2017-12-18 22:57:02');
INSERT INTO proiect.EXAMINARI (id_pacient, data) VALUES (3, '2017-12-17 22:58:43');
INSERT INTO proiect.EXAMINARI (id_pacient, data) VALUES (4, '2017-12-16 23:02:33');
INSERT INTO proiect.EXAMINARI (id_pacient, data) VALUES (5, '2017-12-16 23:03:11');

#insert into rezultate

INSERT INTO proiect.REZULTATE (id_examinare, tip) VALUES (1, 1);
INSERT INTO proiect.REZULTATE (id_examinare, tip) VALUES (2, 1);
INSERT INTO proiect.REZULTATE (id_examinare, tip) VALUES (3, 1);
INSERT INTO proiect.REZULTATE (id_examinare, tip) VALUES (4, 1);
INSERT INTO proiect.REZULTATE (id_examinare, tip) VALUES (5, 1);



#insert into medici

INSERT INTO proiect.MEDICI (id_rezultat, nume, specializare) VALUES (1, 'Doc Gigel', 'Incapatanare cronica');
INSERT INTO proiect.MEDICI (id_rezultat, nume, specializare) VALUES (2, 'Doc Gigel', 'Incapatanare cronica');
INSERT INTO proiect.MEDICI (id_rezultat, nume, specializare) VALUES (3, 'Doc Mirel', 'Incapatanare acuta');
INSERT INTO proiect.MEDICI (id_rezultat, nume, specializare) VALUES (4, 'Doc Miner', 'Incapatanare avansata');
INSERT INTO proiect.MEDICI (id_rezultat, nume, specializare) VALUES (5, 'Doc Miner', 'Incapatanare avansata');


# insert into tratamente
INSERT INTO proiect.TRATAMENTE (id_medic, denumire, comentarii, data_inceput, data_sfarsit) VALUES (1, 'Tratamentos icuos', null, '2017-12-24 00:42:35', '2017-12-28 00:42:43');
INSERT INTO proiect.TRATAMENTE (id_medic, denumire, comentarii, data_inceput, data_sfarsit) VALUES (2, 'Tratamentos icuos', 'Se recomanda precautie in interactiunea cu pacientul', '2017-12-22 00:43:18', '2017-12-29 00:43:23');
INSERT INTO proiect.TRATAMENTE (id_medic, denumire, comentarii, data_inceput, data_sfarsit) VALUES (3, 'Tratamentos duoduo', null, '2017-12-24 00:42:35', '2017-12-28 00:42:43');
INSERT INTO proiect.TRATAMENTE (id_medic, denumire, comentarii, data_inceput, data_sfarsit) VALUES (4, 'Tratamentos triados', null, '2017-12-22 00:43:18', '2017-12-28 00:42:43');
INSERT INTO proiect.TRATAMENTE (id_medic, denumire, comentarii, data_inceput, data_sfarsit) VALUES (5, 'Tratamentos triados', null, '2017-12-22 00:43:18', '2018-01-20 00:44:54');


#insert into medicamente
INSERT INTO proiect.MEDICAMENTE (id_tratament, denumire, cantitate, gramaj) VALUES (1, 'Medicamentos hapciu', 12, null);
INSERT INTO proiect.MEDICAMENTE (id_tratament, denumire, cantitate, gramaj) VALUES (2, 'Medicamentos hapciu', 24, null);
INSERT INTO proiect.MEDICAMENTE (id_tratament, denumire, cantitate, gramaj) VALUES (3, 'Medicamentos boom-boom', 1, 20.5);
INSERT INTO proiect.MEDICAMENTE (id_tratament, denumire, cantitate, gramaj) VALUES (4, 'Medicamentos bumcha', 2, 4.0);
INSERT INTO proiect.MEDICAMENTE (id_tratament, denumire, cantitate, gramaj) VALUES (5, 'Medicamentos bumcha', 4, 8.0);

```

# Updates
```sql
update MEDICI set specializare = "Incapanare Cronica" where nume = "Doc Gigel"
update PACIENTI set nume = "Maryn Maryn" where nume = "Marin Marin"
update CAMERE set nr_paturi = 4 where id_complex = 2
update COMPLEXURI set adresa = concat('Str. ', adresa)
update MEDICAMENTE set denumire = replace(denumire, 'mentos', 'MENTOS')
```


# Tabele

### Complexuri
| id | nume | adresa |
| --- | --- | --- |
| 1 | Spitalu 9 | Str. Pacii 2 |
| 2 | Magheru  | Str. Magheru 15 |
| 3 | Ungheru | Str. Ungheru 22 |
| 4 | Grigore Alexandrescu | Str. Splaiul 2 |
| 5 | Marie Curie | Str. Berceni 222 |

### Camere
| id | id_complex | nr_paturi |
| --- | --- | --- |
| 1 | 1 | 2 |
| 2 | 1 | 2 |
| 3 | 1 | 2 |
| 4 | 2 | 4 |
| 5 | 2 | 4 |

### Pacienti
| id | id_camera | nume | data_internare | sex |
| --- | --- | --- | --- | --- |
| 1 | 1 | George George | 2017-12-19 22:51:12 | 1 |
| 2 | 1 | Maryn Maryn | 2017-12-18 22:57:00 | 1 |
| 3 | 2 | Andrei Andrei | 2017-12-17 22:58:43 | 1 |
| 4 | 4 | Maria Maria | 2017-12-16 23:02:33 | 2 |
| 5 | 4 | Alina Alina | 2017-12-16 23:03:11 | 2 |

### Examinari
| id | id_pacient | data |
| --- | --- | --- |
| 1 | 1 | 2017-12-19 22:51:12 |
| 2 | 2 | 2017-12-18 22:57:02 |
| 3 | 3 | 2017-12-17 22:58:43 |
| 4 | 4 | 2017-12-16 23:02:33 |
| 5 | 5 | 2017-12-16 23:03:11 |

### Rezultate
| id | id_examinare | tip |
| --- | --- | --- |
| 1 | 1 | 1 |
| 2 | 2 | 1 |
| 3 | 3 | 1 |
| 4 | 4 | 1 |
| 5 | 5 | 1 |


### Medici
| id | id_rezultat | nume | specializare |
| --- | --- | --- | --- |
| 1 | 1 | Doc Gigel | Incapanare Cronica |
| 2 | 2 | Doc Gigel | Incapanare Cronica |
| 3 | 3 | Doc Mirel | Incapatanare acuta |
| 4 | 4 | Doc Miner | Incapatanare avansata |
| 5 | 5 | Doc Miner | Incapatanare avansata |


### Tratamente
| id | id_medic | denumire | comentarii | data_inceput | data_sfarsit |
| --- | --- | --- | --- | --- | --- |
| 1 | 1 | Tratamentos icuos | NULL | 2017-12-24 00:42:35 | 2017-12-28 00:42:43 |
| 2 | 2 | Tratamentos icuos | Se recomanda precautie in interactiunea cu pacientul | 2017-12-22 00:43:18 | 2017-12-29 00:43:23 |
| 3 | 3 | Tratamentos duoduo | NULL | 2017-12-24 00:42:35 | 2017-12-28 00:42:43 |
| 4 | 4 | Tratamentos triados | NULL | 2017-12-22 00:43:18 | 2017-12-28 00:42:43 |
| 5 | 5 | Tratamentos triados | NULL | 2017-12-22 00:43:18 | 2018-01-20 00:44:54 |


### Medicamente
| id | id_tratament | denumire | cantitate | gramaj |
| --- | --- | --- | --- | --- |
| 1 | 1 | MedicaMENTOS hapciu | 12 | NULL |
| 2 | 2 | MedicaMENTOS hapciu | 24 | NULL |
| 3 | 3 | MedicaMENTOS boom-boom | 1 | 20.5 |
| 4 | 4 | MedicaMENTOS bumcha | 2 | 4.0 |
| 5 | 5 | MedicaMENTOS bumcha | 4 | 8.0 |

#
 
# Interogari

#
#### 1. Sa se afiseze numele tuturor pacientilor
```sql
    select nume from PACIENTI
```
| nume |
| --- |
| George George |
| Maryn Maryn |
| Andrei Andrei |
| Maria Maria |
| Alina Alina |

#### 2. Sa se afiseze numele pacientelor
```sql
    select nume from PACIENTI where sex = 2
```

| nume |
| --- |
| Maria Maria |
| Alina Alina |



#### 3. Sa se afiseze in ce camera sta fiecare pacient
```sql
    select nume,id_camera from PACIENTI 
```
| nume | id_camera |
| --- | --- |
| George George | 1 |
| Maryn Maryn | 1 |
| Andrei Andrei | 2 |
| Maria Maria | 4 |
| Alina Alina | 4 |


#### 4. Sa se afiseze in ce complex si la ce adresa poate fi gasit fiecare pacient
```sql
select PACIENTI.nume, COMPLEXURI.nume, COMPLEXURI.adresa from PACIENTI
join CAMERE on PACIENTI.id_camera = CAMERE.id
join COMPLEXURI on CAMERE.id_complex = COMPLEXURI.id
```
| nume | nume | adresa |
| --- | --- | --- |
| George George | Spitalu 9 | Str. Pacii 2 |
| Maryn Maryn | Spitalu 9 | Str. Pacii 2 |
| Andrei Andrei | Spitalu 9 | Str. Pacii 2 |
| Maria Maria | Magheru  | Str. Magheru 15 |
| Alina Alina | Magheru  | Str. Magheru 15 |

#### 5. Sa se afiseze ce medic a tratat vreodata fiecare pacient
```sql
select PACIENTI.nume, MEDICI.nume from PACIENTI
join EXAMINARI on PACIENTI.id = EXAMINARI.id_pacient
join REZULTATE on EXAMINARI.id = REZULTATE.id_examinare
join MEDICI on REZULTATE.id = MEDICI.id_rezultat
```
| nume | nume |
| --- | --- |
| George George | Doc Gigel |
| Maryn Maryn | Doc Gigel |
| Andrei Andrei | Doc Mirel |
| Maria Maria | Doc Miner |
| Alina Alina | Doc Miner |

#### 6. Sa se afiseze toate tratamentele prescrise si medicul care le-a prescris
```sql
select MEDICI.nume as "PRESCRIS DE MEDICUL", TRATAMENTE.*from TRATAMENTE
join MEDICI on TRATAMENTE.id_medic = MEDICI.id
```
| PRESCRIS DE MEDICUL | id | id_medic | denumire | comentarii | data_inceput | data_sfarsit |
| --- | --- | --- | --- | --- | --- | --- |
| Doc Gigel | 1 | 1 | Tratamentos icuos | NULL | 2017-12-24 00:42:35 | 2017-12-28 00:42:43 |
| Doc Gigel | 2 | 2 | Tratamentos icuos | Se recomanda precautie in interactiunea cu pacientul | 2017-12-22 00:43:18 | 2017-12-29 00:43:23 |
| Doc Mirel | 3 | 3 | Tratamentos duoduo | NULL | 2017-12-24 00:42:35 | 2017-12-28 00:42:43 |
| Doc Miner | 4 | 4 | Tratamentos triados | NULL | 2017-12-22 00:43:18 | 2017-12-28 00:42:43 |
| Doc Miner | 5 | 5 | Tratamentos triados | NULL | 2017-12-22 00:43:18 | 2018-01-20 00:44:54 |

#### 7. Sa se afiseze ce medicamente a prescris fiecare medic
```sql
select MEDICI.nume as "PRESCRIS DE MEDICUL", MEDICAMENTE.*from MEDICAMENTE
  join TRATAMENTE on MEDICAMENTE.id_tratament = TRATAMENTE.id
join MEDICI on TRATAMENTE.id_medic = MEDICI.id
```
| PRESCRIS DE MEDICUL | id | id_tratament | denumire | cantitate | gramaj |
| --- | --- | --- | --- | --- | --- |
| Doc Gigel | 1 | 1 | MedicaMENTOS hapciu | 12 | NULL |
| Doc Gigel | 2 | 2 | MedicaMENTOS hapciu | 24 | NULL |
| Doc Mirel | 3 | 3 | MedicaMENTOS boom-boom | 1 | 20.5 |
| Doc Miner | 4 | 4 | MedicaMENTOS bumcha | 2 | 4.0 |
| Doc Miner | 5 | 5 | MedicaMENTOS bumcha | 4 | 8.0 |

#### 8. Sa se afiseze ce medicamente au fost prescrise pentru fiecare pacient
```sql
select PACIENTI.nume, MEDICAMENTE.* from PACIENTI
join EXAMINARI on PACIENTI.id = EXAMINARI.id_pacient
join REZULTATE on EXAMINARI.id = REZULTATE.id_examinare
join MEDICI on REZULTATE.id = MEDICI.id_rezultat
join TRATAMENTE on MEDICI.id = TRATAMENTE.id_medic
join MEDICAMENTE on TRATAMENTE.id = MEDICAMENTE.id_tratament
```
| nume | id | id_tratament | denumire | cantitate | gramaj |
| --- | --- | --- | --- | --- | --- |
| George George | 1 | 1 | MedicaMENTOS hapciu | 12 | NULL |
| Maryn Maryn | 2 | 2 | MedicaMENTOS hapciu | 24 | NULL |
| Andrei Andrei | 3 | 3 | MedicaMENTOS boom-boom | 1 | 20.5 |
| Maria Maria | 4 | 4 | MedicaMENTOS bumcha | 2 | 4.0 |
| Alina Alina | 5 | 5 | MedicaMENTOS bumcha | 4 | 8.0 |

#### 9. Sa se determine toate medicamentele diferite prescrise pentru pacientul George George
```sql
select DISTINCT (MEDICAMENTE.denumire) from PACIENTI
  join EXAMINARI on PACIENTI.id = EXAMINARI.id_pacient
  join REZULTATE on EXAMINARI.id = REZULTATE.id_examinare
  join MEDICI on REZULTATE.id = MEDICI.id_rezultat
  join TRATAMENTE on MEDICI.id = TRATAMENTE.id_medic
  join MEDICAMENTE on TRATAMENTE.id = MEDICAMENTE.id_tratament
where PACIENTI.nume = "George George"
```
| denumire |
| --- |
| MedicaMENTOS hapciu |

#### 10. Sa se determine tratamentele care au data de sfarsit in anul viitor, pentru pre-comandarea medicamentelor necesare
```sql
select * from TRATAMENTE where data_sfarsit >= "2018-01-01"
```
| id | id_medic | denumire | comentarii | data_inc | data_sf |
| --- | --- | --- | --- | --- | --- |
| 5 | 5 | Tratamentos triados | NULL | 2017-12-22 00:43:18 | 2018-01-20 00:44:54 |


#### 11. Sa se afiseze pacientii care au fost examinati in momentul internarii 
```sql
select PACIENTI.*, EXAMINARI.* from PACIENTI
join EXAMINARI on PACIENTI.id = EXAMINARI.id_pacient
where PACIENTI.data_internare = EXAMINARI.data
```
| id | id_cam | nume | data_int | sex | id | id_pacient | data |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1 | George George | 2017-12-19 22:51:12 | 1 | 1 | 1 | 2017-12-19 22:51:12 |
| 3 | 2 | Andrei Andrei | 2017-12-17 22:58:43 | 1 | 3 | 3 | 2017-12-17 22:58:43 |
| 4 | 4 | Maria Maria | 2017-12-16 23:02:33 | 2 | 4 | 4 | 2017-12-16 23:02:33 |
| 5 | 4 | Alina Alina | 2017-12-16 23:03:11 | 2 | 5 | 5 | 2017-12-16 23:03:11 |

#### 12. Sa se afiseze pacientii care nu au fost examinati in momentul internarii 
```sql
select PACIENTI.*, EXAMINARI.* from PACIENTI
join EXAMINARI on PACIENTI.id = EXAMINARI.id_pacient
where PACIENTI.data_internare != EXAMINARI.data
```
| id | id_camera | nume | data_int | sex | id | id_pac | data |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 2 | 1 | Maryn Maryn | 2017-12-18 22:57:00 | 1 | 2 | 2 | 2017-12-18 22:57:02 |


#### 13. Sa se afiseze toate specializarile (diferite) ale medicilor care au fost asignati pacientilor
```sql
select specializare from MEDICI GROUP BY specializare
```

| specializare |
| --- |
| Incapanare Cronica |
| Incapatanare acuta |
| Incapatanare avansata |


#### 14. Sa se afisze ce medicamente au fost prescrise si pot avea diferite gramaje
```sql
select * from MEDICAMENTE where gramaj is not null
```
| id | id_tratament | denumire | cantitate | gramaj |
| --- | --- | --- | --- | --- |
| 3 | 3 | MedicaMENTOS boom-boom | 1 | 20.5 |
| 4 | 4 | MedicaMENTOS bumcha | 2 | 4.0 |
| 5 | 5 | MedicaMENTOS bumcha | 4 | 8.0 |


#### 15. Sa se afiseze ce medicamente trebuiesc trimise in complexul "Spitalu 9"
```sql
select MEDICAMENTE.* from COMPLEXURI
join CAMERE on COMPLEXURI.id = CAMERE.id_complex
join PACIENTI on CAMERE.id = PACIENTI.id_camera
join EXAMINARI on PACIENTI.id = EXAMINARI.id_pacient
join REZULTATE on EXAMINARI.id = REZULTATE.id_examinare
join MEDICI on REZULTATE.id = MEDICI.id_rezultat
join TRATAMENTE on MEDICI.id = TRATAMENTE.id_medic
join MEDICAMENTE ON TRATAMENTE.id = MEDICAMENTE.id_tratament
where COMPLEXURI.nume = "Spitalu 9"
```
| id | id_tratament | denumire | cantitate | gramaj |
| --- | --- | --- | --- | --- |
| 1 | 1 | MedicaMENTOS hapciu | 12 | NULL |
| 2 | 2 | MedicaMENTOS hapciu | 24 | NULL |
| 3 | 3 | MedicaMENTOS boom-boom | 1 | 20.5 |



