# 4pr

1)очистить данные и привести к 3 НФ. 

    create table car_data as
        select 
            field1 as id, -- идентификаторы
            trim(replace(replace(price, '₽'), ' ')) as price, -- цена
            trim(replace(substr(двигатель, 0, instr(двигатель, '/')-1), 'л')) as L_in_engine, -- литраж двигателя
       trim(replace(substr(substr(двигатель, instr(двигатель, '/')+1), 0, instr(substr(двигатель, instr(двигатель, '/')+1), '/')-1), 'л.с.')) as horsepower, --           лошадиные силы
        lower(trim(substr(substr(двигатель, instr(двигатель, '/')+1), instr(substr(двигатель, instr(двигатель, '/')+1), '/')+1))) as type_of_fuel, -- тип топлива
        коробка as gearbox, -- коробка
        case
           when instr(кузов, ' ') != 0
               then trim(substr(кузов, 0, instr(кузов, ' '))) 
                else кузов
        end as car_body, -- кузов
       case
           when instr(кузов, ' ') != 0
                then trim(replace(substr(кузов, instr(кузов, ' ')), 'дв.'))
       end as door_quantity, -- кол-во дверей
       привод as drive, -- привод
       trim(replace(replace(пробег, 'км'), ' ')) as mileage,
       lower(руль) as rudder, -- руль
       lower(состояние) as condition, -- состояние
        lower(таможня) as customs, -- таможня
        цвет as color, -- цвет
       год_выпуска as year_of_release -- год выпуска
    from source_data;

    create table car_body as
    select
          distinct
        car_body
    from car_data;
    
    alter table car_body
    add (id int);
    
    update car_body set id = 1 where car_body = 'Купе';
    update car_body set id = 2 where car_body = 'Внедорожник';
    update car_body set id = 3 where car_body = 'Кабриолет';
    update car_body set id = 4 where car_body = 'Минивен';
    update car_body set id = 5 where car_body = 'Пикап';
    update car_body set id = 6 where car_body = 'Лимузин';
    update car_data set car_body = 1 where car_body = 'Купе';
    update car_data set car_body = 2 where car_body = 'Внедорожник';
    update car_data set car_body = 3 where car_body = 'Кабриолет';
    update car_data set car_body = 4 where car_body = 'Минивен';
    update car_data set car_body = 5 where car_body = 'Пикап';
    update car_data set car_body = 6 where car_body = 'Лимузин';

    create table drive as
    select
       distinct
       drive
    from car_data;
    
    alter table drive
    add (id int);
    
    update drive set id = 1 where drive = 'полный';
    update drive set id = 2 where drive = 'передний';
    update car_data set drive = 1 where drive = 'полный';
    update car_data set drive = 2 where drive = 'передний';

    create table rudder as
    select
        distinct
       rudder
    from car_data;
    
    alter table rudder
    add (id int);
    
    update rudder set id = 1 where rudder = 'левый';
    update rudder set id = 2 where rudder = 'правый';
    update car_data set rudder = 1 where rudder = 'левый';
    update car_data set rudder = 2 where rudder = 'правый';

    create table condition as
    select
       distinct
       condition
    from car_data;
    
    alter table condition
    add (id int);
    
    update condition set id = 1 where condition = 'не требует ремонта';
    update car_data set condition = 1 where condition = 'не требует ремонта';

    create table customs as
    select
       distinct
       customs
    from car_data;
    
    alter table customs
    add (id int);
    
  
    update customs set id = 1 where customs = 'растаможен';
    update car_data set customs = 1 where customs = 'растаможен';

    create table color as
    select
        distinct
        color
    from car_data;
    
    alter table color
    add (id int);
    
    update color set id = 1 where color = 'Белый';
    update color set id = 2 where color = 'Красный';
    update color set id = 3 where color = 'Черный';
    update color set id = 4 where color = 'Синий';
    update color set id = 5 where color = 'Зеленый';
    update color set id = 6 where color = 'Фиолетовый';
    update color set id = 7 where color = 'Оранжевый';
    update color set id = 8 where color = 'Голубой';
    update color set id = 9 where color = 'Желтый';
    update color set id = 10 where color = 'Коричневый';
    update color set id = 11 where color = 'Пурпурный';
    update color set id = 12 where color = 'Серый';
    update car_data set color = 1 where color = 'Белый';
    update car_data set color = 2 where color = 'Красный';
    update car_data set color = 3 where color = 'Черный';
    update car_data set color = 4 where color = 'Синий';
    update car_data set color = 5 where color = 'Зеленый';
    update car_data set color = 6 where color = 'Фиолетовый';
    update car_data set color = 7 where color = 'Оранжевый';
    update car_data set color = 8 where color = 'Голубой';
    update car_data set color = 9 where color = 'Желтый';
    update car_data set color = 10 where color = 'Коричневый';
    update car_data set color = 11 where color = 'Пурпурный';
    update car_data set color = 12 where color = 'Серый';

    create table year_of_release as
    select
        distinct
        year_of_release
    from car_data;

    alter table year_of_release
    add (id int);

    update year_of_release set id = 1 where year_of_release = '2012';
    update year_of_release set id = 2 where year_of_release = '2008';
    update year_of_release set id = 3 where year_of_release = '1999';
    update year_of_release set id = 4 where year_of_release = '2012';
    update year_of_release set id = 5 where year_of_release = '2021';
    update year_of_release set id = 6 where year_of_release = '2018';
    update year_of_release set id = 7 where year_of_release = '2020';
    update year_of_release set id = 8 where year_of_release = '2016';
    update year_of_release set id = 9 where year_of_release = '1992';
    update year_of_release set id = 10 where year_of_release = '2015';
    update year_of_release set id = 11 where year_of_release = '2012';
    update year_of_release set id = 12 where year_of_release = '2017';
    update year_of_release set id = 13 where year_of_release = '2011';
    update year_of_release set id = 14 where year_of_release = '2003';
    update year_of_release set id = 15 where year_of_release = '2002';
    update year_of_release set id = 16 where year_of_release = '2005';
    update year_of_release set id = 17 where year_of_release = '2004';
    update year_of_release set id = 18 where year_of_release = '2007';
    update year_of_release set id = 19 where year_of_release = '2005';
    update year_of_release set id = 20 where year_of_release = '2000';
    
    update year_of_release year_of_release id = 1 where year_of_release = '2012';
    update year_of_release year_of_release id = 2 where year_of_release = '2008';
    update year_of_release year_of_release id = 3 where year_of_release = '1999';
    update year_of_release year_of_release id = 4 where year_of_release = '2012';
    update year_of_release year_of_release id = 5 where year_of_release = '2021';
    update year_of_release year_of_release id = 6 where year_of_release = '2018';
    update year_of_release year_of_release id = 7 where year_of_release = '2020';
    update year_of_release year_of_release id = 8 where year_of_release = '2016';
    update year_of_release year_of_release id = 9 where year_of_release = '1992';
    update year_of_release year_of_release id = 10 where year_of_release = '2015';
    update year_of_release year_of_release id = 11 where year_of_release = '2012';
    update year_of_release year_of_release id = 12 where year_of_release = '2017';
    update year_of_release year_of_release id = 13 where year_of_release = '2011';
    update year_of_release year_of_release id = 14 where year_of_release = '2003';
    update year_of_release year_of_release id = 15 where year_of_release = '2002';
    update year_of_release year_of_release id = 16 where year_of_release = '2005';
    update year_of_release year_of_release id = 17 where year_of_release = '2004';
    update year_of_release year_of_release id = 18 where year_of_release = '2007';
    update year_of_release year_of_release id = 19 where year_of_release = '2005';
    update year_of_release year_of_release id = 20 where year_of_release = '2000';
    
    

    create table gearbox as 
    select 
        distinct
        gearbox
    from car_data;

    alter table gearbox
    add (id int);


    update gearbox set id = 1 where gearbox = 'механическая';
    update gearbox set id = 2 where gearbox = 'автоматическая';
    update gearbox set id = 3 where gearbox = 'роботизированная';
    update gearbox set id = 4 where gearbox = 'вариатор';

    update car_data set gearbox = 1 where gearbox = 'механическая';
    update car_data set gearbox = 2 where gearbox = 'автоматическая';
    update car_data set gearbox = 3 where gearbox = 'роботизированная';
    update car_data set gearbox = 4 where gearbox = 'вариатор';


    create table type_of_fuel as
    select 
        distinct
        type_of_fuel
    from car_data;


    alter table type_of_fuel
    add (id int);

    update type_of_fuel set id = 1 where type_of_fuel = 'бензин';

    update car_data set type_of_fuel = 1 where type_of_fuel = 'бензин';


    create table horsepower as
    select
        distinct
        horsepower
    from car_data;

    alter table horsepower
    add (id int);

    update horsepower set id = 1 where horsepower = 200;
    update horsepower set id = 2 where horsepower = 100;
    update horsepower set id = 3 where horsepower = 85;
    update horsepower set id = 4 where horsepower = 189;
    update horsepower set id = 5 where horsepower = 148;
    update horsepower set id = 6 where horsepower = 132;
    update horsepower set id = 7 where horsepower = 158;
    update horsepower set id = 8 where horsepower = 70;
    update horsepower set id = 9 where horsepower = 1450;
    update horsepower set id = 10 where horsepower = 188;
    update horsepower set id = 11 where horsepower = 139;
    update horsepower set id = 12 where horsepower = 164;
    update horsepower set id = 13 where horsepower = 181;
    update horsepower set id = 14 where horsepower = 189;
    update horsepower set id = 15 where horsepower = 63;
    update horsepower set id = 16 where horsepower = 202;
    update horsepower set id = 17 where horsepower = 208;
    update horsepower set id = 18 where horsepower = 258;
    update horsepower set id = 19 where horsepower = 255;
    
    update horsepower set horsepower = 1 where horsepower = 200;
    update horsepower set horsepower = 2 where horsepower = 100;
    update horsepower set horsepower = 3 where horsepower = 85;
    update horsepower set horsepower = 4 where horsepower = 189;
    update horsepower set horsepower = 5 where horsepower = 148;
    update horsepower set horsepower = 6 where horsepower = 132;
    update horsepower set horsepower = 7 where horsepower = 158;
    update horsepower set horsepower = 8 where horsepower = 70;
    update horsepower set horsepower = 9 where horsepower = 1450;
    update horsepower set horsepower = 10 where horsepower = 188;
    update horsepower set horsepower = 11 where horsepower = 139;
    update horsepower set horsepower = 12 where horsepower = 164;
    update horsepower set horsepower = 13 where horsepower = 181;
    update horsepower set horsepower = 14 where horsepower = 189;
    update horsepower set horsepower = 15 where horsepower = 63;
    update horsepower set horsepower = 16 where horsepower = 202;
    update horsepower set horsepower = 17 where horsepower = 208;
    update horsepower set horsepower = 18 where horsepower = 258;
    update horsepower set horsepower = 19 where horsepower = 255;

    create table l_in_engine as 
    select
        distinct
        l_in_engine
    from car_data;

    alter table l_in_engine
    add (id int); 

    update l_in_engine set id = 1 where l_in_engine = 2.1;
    update l_in_engine set id = 2 where l_in_engine = 3.1;
    update l_in_engine set id = 3 where l_in_engine = 2.1;
    update l_in_engine set id = 4 where l_in_engine = 1.1;
    update l_in_engine set id = 5 where l_in_engine = 1.1;
    update l_in_engine set id = 6 where l_in_engine = 0.1;
    update l_in_engine set id = 7 where l_in_engine = 1.1;
    update l_in_engine set id = 8 where l_in_engine = 1.1;
    update l_in_engine set id = 9 where l_in_engine = 1.1;
    update car_data set l_in_engine = 1 where l_in_engine = 2.1;
    update car_data set l_in_engine = 2 where l_in_engine = 3.1;
    update car_data set l_in_engine = 3 where l_in_engine = 2.1;
    update car_data set l_in_engine = 4 where l_in_engine = 1.1;
    update car_data set l_in_engine = 5 where l_in_engine = 1.1;
    update car_data set l_in_engine = 6 where l_in_engine = 0.1;
    update car_data set l_in_engine = 7 where l_in_engine = 1.1;
    update car_data set l_in_engine = 8 where l_in_engine = 1.1;
    update car_data set l_in_engine = 9 where l_in_engine = 1.1;

2)создать представление, которое считает кол-во автомобилей на каждый год

    create view task_two as
        select 
            year_of_release,
            count(id) as count_of_year
        from car_data
        group by year_of_release;

3)создать представление, которое считает кол-во машин дороже средней цены и кол-во автомобилей дешевле средней цены. 

    create view task_three as 
    select 
        more_of_mean,
        count(more_of_mean) as count_more_and_low_of_mean_price_car
    from (select
            case
              when price > (select avg(price) from car_data)
                then 1
                else 0
            end as more_of_mean
          from car_data)
    group by more_of_mean;

4)создать представление, которое считает разницу между средней ценой растаможенных и не растаможенных машин. 

    create view not_customs as 
    select
        avg(price) as price
    from car_data
    where customs like 'не растаможен';

    create view customs as 
    select
        avg(price) as price
    from car_data
    where customs like 'растаможен';

    create view task_four as 
    select
        case
            when t2.price is null
                then t1.price
            when t1.price is null
                then t2.price
            else t1.price - t2.price
        end as difference
    from customs t1
    join not_customs t2
    on 1 = 1;


    -- задание 1
    select * from car_data;
    select * from l_in_engine;
    select * from horsepower;
    select * from type_of_fuel;
    select * from gearbox;
    select * from car_body;
    select * from drive;
    select * from rudder;
    select * from condition;
    select * from customs;
    select * from color;
    select * from year_of_release;

задание 2

    select * from task_two;

задание 3

    select * from task_three;

задание 4

    select * from task_four;
