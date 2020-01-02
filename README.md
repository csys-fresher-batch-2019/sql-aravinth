# ReserveMe
### >https://ReserveMe.in

## Features
  ### >users can be able to view all trains.
## Feature 1: list of all trains

```sql
   create table train_lists(
   train_num number ,
   train_name varchar2(50) not null unique,
   source_station varchar2(50) ,
   destination_station varchar2(50),
   class varchar2(50),
   constraint train_num_pk primary key(train_num),
   constraint class_ck check(class in ('non-ac-sleeper','non-ac-seater','ac-sleeper','ac-seater')),
   constraint source_dest_ck check(source_station<>destination_station));
   
   insert into  train_lists(train_num,train_name,source_station,destination_station,class)values
   (123,'indian express','chennai','covai','sleeper');
   insert into  train_lists(train_num,train_name,source_station,destination_station,class)values
   (321,'sahapthi express','covai','madurai','non-ac-sleeper');
   insert into  train_lists(train_num,train_name,source_station,destination_station,class)value
   (467,'dindugal express','chengalpattu','chennai','ac-seater');
   insert into  train_lists(train_num,train_name,source_station,destination_station,class)value
   (426,'covai express','chennai','covai','ac-seater');   
```   
| s.no | train_num | train_name       | source_station | destination_station | class          |
|------|-----------|------------------|----------------|---------------------|----------------|
| 1    | 123       | indian express   | chennai        | covai               | ac-sleeper     |
| 2    | 321       | sahapthi express | covai          | madurai             | non-ac-sleeper |
| 3    | 467       | dindugal express | chengalpattu   | chennai             | ac-sleeper     |
| 4    | 426       | covai express    | chennai        | covai               | ac-sleeper     |

## Feature 2: Passanger information
```sql
   create table passenger_details(
   train_num number,
   p_name varchar2(50) not null,
   p_id number,
   no_of_tickets number not null,
   p_age number not null,
   p_gender char(1) not null,
   p_contact number(10) not null,
   constraints train_num_fk foreign key(train_num) references train_lists(train_num),
   constraints p_id primary key(p_id),
   constraints p_age_ck check(p_age>=1),
   constraints p_gender_ck check(p_gender in('M','F','O')),
   constraints no_of_tickets check(no_of_tickets>=1),
   constraints p_contact_ck check(p_contact>999999999));
   create sequence p_id
   start with 1000
   increment by 1
   insert into passenger_details(train_num,p_name,p_id,no_of_tickets,p_age,p_gender,p_contact) values (123,'Aravinth',p_id.nextval,5,33,'M',8531946805);
   insert into passenger_details(train_num,p_name,p_id,no_of_tickets,p_age,p_gender,p_contact) values (321,'sahana',p_id.nextval,6,19,'F',9876543210);
   insert into passenger_details(train_num,p_name,p_id,no_of_tickets,p_age,p_gender,p_contact) values (123,'praveen',p_id.nextval,7,60,'M',8765432190);
   insert into passenger_details(train_num,p_name,p_id,no_of_tickets,p_age,p_gender,p_contact) values (426,'amrish',p_id.nextval,34,45,'M',7890654673);
   select * from passenger_details where train_num = 123;
```   
| s.no | train_num | p_nmae   | p_id | n0.of.tickets  | p_age | p_gender | p_contact  |
|------|-----------|----------|------|----------------|-------|----------|------------|
| 1    | 123       | Aravinth | 1000 | 5              | 33    | M        | 8531946805 |
| 2    | 321       | sahana   | 1001 | 6              | 19    | F        | 9876543210 |
| 3    | 123       | praveen  | 1002 | 7              | 60    | M        | 8765432190 |
| 4    | 426       | amrish   | 1003 | 34             | 45    | M        | 7890654673 |
