# Baza relationala 

Costache Radu
Grupa 353
Prof. Coordonator: Sorina Predut

## Scenariu 

In anul 2099, refuzul oamenilor de a accepta schimbari necesare este mai daunator societatii ca niciodata. Desi ultimii zeci de ani au fost o dovada clara ca unele schimbari sunt necesare pentru bunastarea tuturor, oamenii refuza sa incerce sa fie deschisi ideilor noi. De aceea, incapatanarea este declarata boala. 

Se doreste crearea unei baze de date in care sa fie stocate informatii despre pacientii internati in azile speciale in care se trateaza aceasta boala mentala, ce medici ii tratateaza in functie de cat de avansata este boala, ce tratamente le sunt prescrise si ce medicamente.

Examinarile pacientilor vor fi automate, ei fiind nevoiti sa raspunda la chestionare. 
In functie de rezultatul examinarii, pacientului ii va fi asignat un doctor care sa fie 
cat mai potrivit pentru a-l ajuta. Medicul ii va prescrie tratamentul ( care este compus din diferite
 medicamente, in functie de recomandarea medicului ). 
 



## ERD & Mapare
###ERD
Tabela PACIENTI

|||||
| ------------- |:-------------:| :-----:|-----:|
| id            | int | PK | * |
| nume            | varchar(255) |  | * |
| data_internare            | datetime |  | * |
| sex            | int |  | * |
| id_camera            | int | FK | * |


Tabela EXAMINARI

|||||
| ------------- |:-------------:| :-----:|-----:|
| id            | int | PK | * |
| id_pacient            | int | FK | * |
| data     | datetime |  | * |

Tabela REZULTATE

|||||
| ------------- |:-------------:| :-----:|-----:|
| id            | int | PK | * |
| id_examinare            | int | FK | * |
| tip     | int |  | * |

Tabela MEDICI

|||||
| ------------- |:-------------:| :-----:|-----:|
| id            | int | PK | * |
| id_rezultat            | int | FK | * |
| specializare            | varchar(255) |  | * |
| nume            | varchar(255) |  | * |

Tabela TRATAMENTE

|||||
| ------------- |:-------------:| :-----:|-----:|
| id            | int | PK | * |
| id_medic           | int | FK | * |
| denumire            | varchar(255) |  | * |
| comentarii         | varchar(255) |  | * |
| data_inceput     | datetime |  | * |
| data_sfarsit | datetime |  | * |

Tabela MEDICAMENTE

|||||
| ------------- |:-------------:| :-----:|-----:|
| id            | int | PK | * |
| id_tratament       | int | FK | * |
| denumire            | varchar(255) |  | * |
| cantitate         | int |  | * |
| gramaj         | int |  | o |

Tabela MEDICAMENTE

|||||
| ------------- |:-------------:| :-----:|-----:|
| id            | int | PK | * |
| id_complex       | int | FK | * |
| nume            | varchar(255) |  | * |
| nr_paturi | int |  | * |

Tabela COMPLEXURI

|||||
| ------------- |:-------------:| :-----:|-----:|
| id            | int | PK | * |
| nume            | varchar(255) |  | * |
| adresa | varchar(255)  |  | * |


##
![Mapare](http://costin.dev.eiddew.com/db2/ERD.png)






