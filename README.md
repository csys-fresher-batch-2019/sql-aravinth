# ReserveMe
### https://ReserveMe.in

## Features
  ### >users can be able to view all trains.
## Feature 1: Creating an Account

```sql
   create table user_account(
user_name varchar2(50) not null,
user_id number,
user_password varchar2(50) not null,
gender char(1) not null,
dob date not null,
contact_number number(10) not null unique,
mail_id varchar2(50) not null unique,
constraint user_id_pk primary key(user_id),
constraints gender_ck check(gender in('M','F','O')),
constraints p_contact_ck check(contact_number>999999999));
  
```   
| S.no | USER_ID | USER_PASSWORD | GENDER | DOB        | CONTACT_NUMBER | MAIL_ID               |
|------|---------|---------------|--------|------------|----------------|-----------------------|
| 1    | 1000    | 2000          | M      | 01-10-1999 | 9842231946     | aravinth@gmail.com    |
| 2    | 1020    | 1234          | M      | 31-05-1999 | 8787877872     | praveen@gmail.com     |
| 3    | 1080    | sincostan     | M      | 13-04-1999 | 6379152730     | dharunks001@gmail.com |

## Feature 1: User Id Sequence

```sql
create sequence user_id
start with 1000
increment by 1;
```
## Feature 3: List the Train Lists
```sql
   create table train_lists(
   train_num number ,
   train_name varchar2(50) not null unique,
   source_station varchar2(50) ,
   destination_station varchar2(50),
   ticket_price number not null,
   journey_date date not null,
   travelling_time varchar2(20) not null,
   constraint train_num_pk primary key(train_num),
   constraint source_dest_ck check(source_station<>destination_station));
   insert into train_lists values(123,'indian express','chennai','covai',200,date '2020-01-26','8:00 to 20:00');
   insert into train_lists values(321,'covai express','chennai','covai',250,date '2020-01-26','10:00 to 22:30');
   insert into  train_lists values(467,'dindugal express','dindugal','chennai',150,date '2020-01-27','06:00 to 13:00');
   insert into  train_lists values(426,'sathapthi express','chennai','madurai',300,date '2020-01-26','21:30 to 04:30');
   insert into  train_lists values(427,'nilgiri express','chennai','covai',300,date '2020-01-27','21:30 to 04:30');
   insert into  train_lists values(597,'american express','chennai','theni',300,date '2020-01-27','21:30 to 04:30');
```   
| S.no | TRAIN_NUM | TRAIN_NAME        | SOURCE_STATION | DESTINATION_STATION | TICKET_PRICE | JOURNEY_DATE | TRAVELLING_TIME |
|------|-----------|-------------------|----------------|---------------------|--------------|--------------|-----------------|
| 1    | 123       | indian express    | chennai        | covai               | 200          | 26-01-2020   | 8:00 to 20:00   |
| 2    | 321       | covai express     | chennai        | covai               | 250          | 26-01-2020   | 10:00 to 22:30  |
| 3    | 426       | sathapthi express | chennai        | madurai             | 300          | 26-01-2020   | 21:30 to 04:30  |

## Feature 4: Seat Availabilities
```sql
 create table seat_availabilities(
   train_num number,
   tot_no_of_seats number not null,
   no_of_seats_available number not null,
   constraints train_num_fk1 foreign key(train_num) references train_lists (train_num));
   insert into seat_availabilities(train_num,tot_no_of_seats,no_of_seats_available) values(123,200,200);
   insert into seat_availabilities(train_num, tot_no_of_seats, no_of_seats_available) values(123,500,500);
   insert into seat_availabilities( train_num, tot_no_of_seats, no_of_seats_available) values( 467,450,450);
   insert into seat_availabilities( train_num, tot_no_of_seats, no_of_seats_available) values( 426,250,250);
```   
| s.no | train.num | tot.no.of.seats | available.seats |
|------|-----------|-----------------|-----------------|
| 1    | 123       | 200             | 200              |
| 2    | 321       | 500             | 500              |
| 3    | 426       | 250             | 250              |
## Feature 5: Passenger Details
```sql
create table passenger_details(
   train_num number,
   user_id number,
   booking_id number,
   passenger_name varchar2(50) not null,
   phone_number number(10) not null,
   no_of_tickets number not null,
   book_status varchar2(10)default 'pending',
   constraints user_id_fk foreign key(user_id) references user_account(user_id),
   constraints booking_id primary key(booking_id),
   constraints phone_number_ck check(phone_number>999999999),
   constraints book_status_ck check( book_status in('pending','booked','cancelled')),
   constraints no_of_tickets_ck check(no_of_tickets>0)
   );
 
```
| S.no | TRAIN_NUM | USER_ID | BOOKING_ID | PASSENGER_NAME | PHONE_NUMBER | NO_OF_TICKETS | BOOK_STATUS |
|------|-----------|---------|------------|----------------|--------------|---------------|-------------|
| 1    | 123       | 1000    | 2000       | Aravinth       | 9842231946   | 1             | booked      |
| 2    | 123       | 1001    | 2001       | Dharun         | 6379152730   | 2             | booked      |
| 3    | 321       | 1002    | 2002       | Dinesh         | 8756445621   | 1             | booked      |


## Feature 6:  Booking Id Sequence
```sql
create sequence booking_id
   start with 2000
   increment by 1;
```
## Feature 7:  Payment Status
```sql
create table payment_status(
   train_num number,
   user_id number,
   booking_id number,
   tot_ticket_price number,
   pay_status varchar2(10)default 'pending',
   payment_mode varchar2(20),
   constraint ps_payment_mode check ( payment_mode in ('cash','creditcard','wallet')),
   constraints pay_status_ck check( pay_status in('paid','pending','failed','returned','cash')),
   constraints user_id_fk1 foreign key(user_id) references user_account(user_id),
   constraints train_num_fk2 foreign key(train_num) references train_lists(train_num),
   constraints booking_id_fk foreign key(booking_id) references passenger_details(booking_id),
   constraints tot_ticket_price_ck check(tot_ticket_price>0));
```
