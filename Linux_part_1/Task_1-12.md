### Задание

1. Используя команду cat в терминале операционной системы Linux, создать два файла "Домашние животные"
   (заполнив файл "собаками", "кошками", "хомяками") и "Вьючные животные" (заполнив файл "лошадьми", "верблюдами" и "
   ослами"),
   а затем объединить их. Просмотреть содержимое созданного файла. Переименовать файл, дав ему новое имя "Друзья
   человека".
2. Создать директорию, переместить файл туда.
3. Подключить дополнительный репозиторий MySQL. Установить любой пакет из этого репозитория.
4. Установить и удалить deb-пакет с помощью dpkg.
5. Выложить историю команд в терминале Ubuntu.
6. Нарисовать диаграмму, в которой есть классы - родительский, домашние животные и вьючные животные,
   в составы которых в случае домашних животных войдут классы: собаки, кошки, хомяки, а в класс вьючные животные войдут:
   лошади, верблюды и ослы.
7. В подключенном MySQL репозитории создать базу данных “Друзья человека”.
8. Создать таблицы с иерархией из диаграммы в БД.
9. Заполнить низкоуровневые таблицы именами (животных), командами которые они выполняют и датами рождения.
10. Удалить из таблицы верблюдов, т.к. верблюдов решили перевезти в другой питомник на зимовку.
    Объединить таблицы "лошади", и "ослы" в одну таблицу.
11. Создать новую таблицу "молодые животные" в которую попадут все животные старше 1 года, но младше 3 лет
    и в отдельном столбце, с точностью до месяца, подсчитать возраст животных в новой таблице.
12. Объединить все таблицы в одну, при этом сохраняя поля, указывающие на прошлую принадлежность к старым таблицам.

### Решение

1.
<details>
    <summary>Команды Bash (развернуть)</summary>

```bash
cat > "Домашние животные"
Собаки
Кошки
Хомяки

'Ctrl+d'
```

```bash
cat > "Вьючные животные"
Лошади
Ослы
Верблюды

'Ctrl+d'
```

```bash
cat "Домашние животные" "Вьючные животные" > Animals
cat Animals
mv "Animals" "Друзья человека"
```

</details>

![pictures for project]([)](https://github.com/Vailbi/Control_work_/blob/main/Linux_part_1/screenshots/1-1.png?raw=true)
![pictures for project]([)](https://github.com/Vailbi/Control_work_/blob/main/Linux_part_1/screenshots/1-2.png?raw=true)

2.

<details>
    <summary>Команды Bash (развернуть)</summary>

```bash
mkdir folder_new
mv 'Друзья человека' folder_new/
ls
cd folder_new/
ls
```

</details>

![pictures for project](/Users/fedorhoruzij/Desktop/Control_work/Linux_part_1/screenshots/2.png)

3.
<details>
    <summary>Команды Bash (развернуть)</summary>

```bash
sudo apt-get update
sudo apt update
sudo apt install mysql-server
sudo service mysql status
```

</details>

![pictures for project](/Users/fedorhoruzij/Desktop/Control_work/Linux_part_1/screenshots/3.png)

4.

Устанавливаем deb-пакет через из официального репозитория 
```bash
apt install nginx
```
Также можно скачать отдельно деб пакет и установить командой:
```bash
dpkg -i "Название пакета"
```
Рекомендуется устанавливать из оф. реп-ия
удаляем командой:
```bash
dpkg -r nginx
```
![pictures for project](/Users/fedorhoruzij/Desktop/Control_work/Linux_part_1/screenshots/4.png)

5.

![pictures for project](/Users/fedorhoruzij/Desktop/Control_work/Linux_part_1/screenshots/5.png)

6.

![pictures for project](/Users/fedorhoruzij/Desktop/Control_work/Linux_part_1/screenshots/diagram.png)

7.

![pictures for project](/Users/fedorhoruzij/Desktop/Control_work/Linux_part_1/screenshots/7.png)

8.

<details>
    <summary>SQL запросы (развернуть)</summary>

```sql
USE Друзья_человека;

CREATE TABLE Родительский_класс (
  id INT PRIMARY KEY AUTO_INCREMENT,
  тип VARCHAR(50)
);


CREATE TABLE Домашние_животные (
  id INT PRIMARY KEY,
  вид VARCHAR(50),
  FOREIGN KEY (id) REFERENCES Родительский_класс(id)
);


CREATE TABLE Собаки (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Домашние_животные(id)
);


CREATE TABLE Кошки (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Домашние_животные(id)
);


CREATE TABLE Хомяки (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Домашние_животные(id)
);


CREATE TABLE Вьючные_животные (
  id INT PRIMARY KEY,
  вид VARCHAR(50),
  FOREIGN KEY (id) REFERENCES Родительский_класс(id)
);


CREATE TABLE Лошади (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Вьючные_животные(id)
);


CREATE TABLE Верблюды (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Вьючные_животные(id)
);


CREATE TABLE Ослы (
  id INT PRIMARY KEY,
  имя VARCHAR(50),
  команда VARCHAR(50),
  дата_рождения DATE,
  FOREIGN KEY (id) REFERENCES Вьючные_животные(id)
);

show databases;
show tables;
```

</details>

![pictures for project](/Users/fedorhoruzij/Desktop/Control_work/Linux_part_1/screenshots/8.png)

9.

<details>
    <summary>SQL запросы (развернуть)</summary>

```sql
INSERT INTO Верблюды ( имя, команда, дата_рождения)
VALUES ('Горбатый', 'Пошел пошел', '2019-09-01'),
       ('Губатый', 'Стоять' '2020-11-12'),
       ('Волосатый', 'Пей давай' '2021-04-05');

INSERT INTO Кошки ( имя, команда, дата_рождения)
VALUES ('Филька', 'Кис-кис-кис', '2020-01-21'),
       ('Рыся', 'Мур-мур-мур', '2021-03-09');

INSERT INTO Лошади ( имя, команда, дата_рождения)
VALUES ('Хромомой', 'Нооо!', '2020-01-21'),
       ('Косой', 'Бррррр', '2022-03-08');

INSERT INTO Ослы ( имя, команда, дата_рождения)
VALUES ('Ишачело', 'Гойда!', '2019-01-21'),
       ('Зелепыня', 'Дайдай', '2021-03-08');

INSERT INTO Собаки ( имя, команда, дата_рождения)
VALUES ('Бобик', 'Голос', '2019-01-21'),
       ('Рекс', 'Сидеть', '2020-03-08');

INSERT INTO Хомяки ( имя, команда, дата_рождения)
VALUES ('Защекан', 'Взять, '2022-01-21'),
       ('ШерлокХомс', 'ФырФыр', '2023-03-08');
```

</details>

10.

<details>
    <summary>SQL запросы (развернуть)</summary>

```sql
TRUNCATE TABLE Верблюды;
```

```sql
CREATE TABLE Парнокопытные AS
SELECT * FROM Лошади
UNION
SELECT * FROM Ослы;
```

</details>

11.

<details>
    <summary>SQL запросы (развернуть)</summary>

```sql
CREATE TABLE Парнокопытные AS
SELECT *, TIMESTAMPDIFF(MONTH, дата_рождения, CURDATE()) AS возраст_в_месяцах
FROM (
    SELECT 'Собаки' AS тип_животного, имя, команда, дата_рождения FROM Собаки
    UNION ALL
    SELECT 'Кошки' AS тип_животного, имя, команда, дата_рождения FROM Кошки
    UNION ALL
    SELECT 'Хомяки' AS тип_животного, имя, команда, дата_рождения FROM Хомяки
    UNION ALL
    SELECT 'Лошади' AS тип_животного, имя, команда, дата_рождения FROM Лошади
    UNION ALL
    SELECT 'Ослы' AS тип_животного, имя, команда, дата_рождения FROM Ослы
) AS животные
WHERE дата_рождения >= DATE_SUB(CURDATE(), INTERVAL 3 YEAR)
AND дата_рождения <= DATE_SUB(CURDATE(), INTERVAL 1 YEAR);

```

</details>

12.

<details>
    <summary>SQL запросы (развернуть)</summary>

```sql
CREATE TABLE Полный_состав AS
SELECT 'Собаки' AS тип_животного, имя, команда, дата_рождения FROM Собаки
UNION ALL
SELECT 'Кошки' AS тип_животного, имя, команда, дата_рождения FROM Кошки
UNION ALL
SELECT 'Хомяки' AS тип_животного, имя, команда, дата_рождения FROM Хомяки
UNION ALL
SELECT 'Лошади' AS тип_животного, имя, команда, дата_рождения FROM Лошади
UNION ALL
SELECT 'Ослы' AS тип_животного, имя, команда, дата_рождения FROM Ослы;

```

</details>
