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

--     client 1                                                        client 2

set transaction isolation level read uncommitted;
begin:

                                                                   begin;

select quantity from products where name = 'phone';

                                                                   insert into sales values (1, 1, 20);
                                                                   update products set quantity = (quantity - 20) where id = 1;

-- get 80, beacuse of another transaction
select quantity from products where name = 'phone';

-- successfuly updated
insert into sales values (2, 1, 10);
-- will be waiting for another transaction
update products set quantity = (quantity - 10) where id = 1;

commit;
                                                                   rollback;
-- get 90
select quantity from products where name = 'phone';









-- begin transaction isolation level read uncommitted;
