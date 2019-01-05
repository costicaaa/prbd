1. Sa se afiseze toate tratamentele prescrise si medicul care le-a prescris
   ```
   select MEDICI.nume as "PRESCRIS DE MEDICUL", TRATAMENTE.*from TRATAMENTE
   inner join MEDICI on TRATAMENTE.id_medic = MEDICI.id
   ```

2. Sa se afiseze toate specializarile (diferite) ale medicilor care au fost asignati pacientilor
   ```
   select specializare from MEDICI GROUP BY specializare
   ```

3. . Sa se afisze ce medicamente pot avea gramaj cuprins intre 3 si 10
    ```
    select * from MEDICAMENTE where gramaj between 3 and 10
    ```

4. sa se afiseze ce gramaje ale medicamentelor oficiale ( fara "test" in numele lor) diferite exista, cu gramaje cuprinse intre 3 si 10 si 15 si 20, ordonate descrescator
    ```
    select gramaj from MEDICAMENTE where MEDICAMENTE.denumire not like "%test%" group by gramaj having gramaj between 3 and 10 or gramaj between 15 and 20 order by gramaj desc
    ```
5. Numarul minim de paturi dintr-o camera
    ```
    select min(nr_paturi) from CAMERE
    ```

6. Numarul maxim de paturi dintr-o camera
     ```
    select max(nr_paturi) from CAMERE
    ```
7.  Numarul mediu de paturi dintr-o camera
    ```
    select round(truncate(avg(nr_paturi),2),2) from CAMERE
    ```
8. Numarul total de paturi
    ```
    select sum(nr_paturi) from CAMERE
    ```
9. Numarul de camere
    ```
    select count(*) from CAMERE
    ```
10. Sa se afiseze ziua din saptamana in care s-au internat pacientii George George si Maryn Maryn
    ```
    select concat(DAYOFWEEK(data_internare), ",",
           DATE_FORMAT(data_internare, "%W %M %Y"))
           as "Zi internare"
           from PACIENTI where nume in ("Maryn Maryn") or nume in ("George George")
    ```
    
11. Sa se afiseze medicamentele - daca gramajul este null , se va scrie "N/A"
     ```
    select denumire, ifnull(gramaj, "N/A") from MEDICAMENTE
    ```
12. verificati functia MOD
    ```
    select mod(count(*), count(*)) from PACIENTI
    ```
13. sa se afiseze rezultatele astfel : tip 1 = "Analiza Completa", tip 2 = "De examinat din nou"
    ``` 
    select id, tip,
           CASE
           when tip = 1 then "Analiza Completa"
           when tip = 2 then "De examinat din nou"
           else tip
           end
    from REZULTATE
    ```
14.  Sa se afiseze ce medicamente trebuiesc trimise in complexul  Spitalu 9

    ```
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
    
15. sa se afiseze informatiile despre camere, cu detalii despre complexurile in care se afla

    ```
    select * from COMPLEXURI
    right outer join  CAMERE C on COMPLEXURI.id = C.id_complex
    ```
    
16.  Sa se afiseze ce medicamente a prescris fiecare medic

    ```
    select MEDICI.nume as "PRESCRIS DE MEDICUL", MEDICAMENTE.*from MEDICAMENTE
    join TRATAMENTE on MEDICAMENTE.id_tratament = TRATAMENTE.id
    join MEDICI on TRATAMENTE.id_medic = MEDICI.id
    ```

17. Sa se afiseze ce medicamente au fost prescrise pentru fiecare pacient

  ```
    select PACIENTI.nume, MEDICAMENTE.* from PACIENTI
    join EXAMINARI on PACIENTI.id = EXAMINARI.id_pacient
    join REZULTATE on EXAMINARI.id = REZULTATE.id_examinare
    join MEDICI on REZULTATE.id = MEDICI.id_rezultat
    join TRATAMENTE on MEDICI.id = TRATAMENTE.id_medic
    join MEDICAMENTE on TRATAMENTE.id = MEDICAMENTE.id_tratament
  ```
  