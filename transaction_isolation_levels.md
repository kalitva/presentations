###Transaction Isolations

#### Schema

```sql
create table products (
  id int primary key,
  name varchar(255) not null,
  price varchar(255) not null,
  quantity int
);

create table sales (
  id int primary key,
  product_id int not null references products (id),
  quantity int not null
);
```

##### Dirty Read (use mysql)

```sql

insert into products values (1, 'phone', '1000', 100);

set transaction isolation level read uncommitted;
begin:

                                                                   begin;

select quantity from products where name = 'phone';

                                                                   insert into sales values (1, 1, 10);
                                                                   update products set quantity = (quantity - 10) where name = 'phone';

-- shows 90, beacuse of another transaction
select quantity from products where name = 'phone';

commit;
                                                                   rollback;
```

##### Non-repetable reads

```sql

insert into products values (2, 'laptop', '2000', 100);

begin transaction isolation level read committed;

                                                                   begin;
select quantity from products where name = 'laptop';

                                                                   insert into sales values (1, 2, 10);
                                                                   update products set quantity = (quantity - 10) where id = 2;

-- shows 100
select quantity from products where name = 'laptop';

                                                                   commit;

-- shows 90
select quantity from products where name = 'laptop';
commit;
```

##### Phantom reads

```sql
insert into products values (3, 'car', '10000', 10);

insert into sales values (2, 3, 1);
insert into sales values (3, 3, 2);
update products set quantity = (quantity - 3) where name = 'car';

begin transaction isolation level repeatable read;

select sum(quantity) from sales;

                                                                   begin;
                                                                   insert into sales values (4, 3, 1);
                                                                   commit;

select sum(quantity) from sales;
commit;
```
