create table customers(
cust_id serial primary key,
cust_name varchar(100) not null
);

create table oders(
oder_id serial primary key,
order_date date not null,
price numeric not null,
cust_id integer not null,
foreign key(cust_id) references
customers(cust_id)
);


INSERT INTO customers (cust_name) VALUES
('Alice'),
('Bob'),
('Charlie'),
('David'),
('Eve');


INSERT INTO oders (order_date, price, cust_id) VALUES
('2024-01-10', 150.50, 1),
('2024-01-12', 200.00, 2),
('2024-01-15', 99.99, 3),
('2024-01-18', 250.75, 4),
('2024-01-20', 300.20, 5);