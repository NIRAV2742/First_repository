drop table client_master_25
desc client_master_25
drop table product_master_25
drop table salesman_master_25
drop table sales_order_25
drop table sales_order_details_25
//first table
create table client_master_25( clientno varchar(6)primary key, name varchar(15)not null, address1 varchar(5), address2 varchar(5), city varchar(15), pincode number(6), state varchar(15), baldue number(10,2), constraint chk_client check(clientno like 'C%'));
insert into client_master_25 values('C00001','Rakesh Joshi','','','Mumbai',400054,'Maharashtra',15000);
insert into client_master_25 values('C00002','Mayur Patel','','','Madras',780001,'Tamilnadu',0);
insert into client_master_25 values('C00003','Ishita mehta','','','Mumbai',400057,'Maharashtra',5000);
insert into client_master_25 values('C00004','Amit Solanki','','','Bangalore',560001,'Karnataka',0);
insert into client_master_25 values('C00005','Hiren Pandya','','','Mumbai',400060,'Maharashtra',2000);
insert into client_master_25 values('C00006','Dipak Sharma','','','Mangalore',560050,'Karnaraka',0);

//second table
create table product_master_25 (productno varchar(6)primary key, description varchar(15)not null, profitpercent number(4,2)not null, unitmaster varchar(7)not null, qtyonhand number(4)not null, reorderlvl number(3)not null, sellprice number(5,2)not null, costprice number(5,2), constraint chk_productno check(productno like 'p%'), constraint chk_sellprice check(sellprice!=0), constraint chk_costprice check(costprice!=0));
insert into product_master_25 values('P00001','T-Shirt',5,'piece',200,50,350,250);
insert into product_master_25 values('P0345','Shirt',6,'piece',150,50,350,500);
insert into product_master_25 values('P06734','Cotton Jeans',5,'piece',100,20,600,450);
insert into product_master_25 values('P07865','Jeans',5,'piece', 100, 20, 750, 500);
insert into product_master_25 values('P07868','Trouser',2,'piece', 150, 50, 850, 550);
insert into product_master_25 values('P07885','Pull Over',2.5,'piece', 80, 30, 700, 450);
insert into product_master_25 values('P07965','Denim Shirt',4,'piece', 100, 40, 350, 250);
insert into product_master_25 values('P07975','Lycra Tops',5,'piece', 70, 30, 300, 175);
insert into product_master_25 values('P08865','skirts',5,'piece', 75, 30, 450, 300);

//third table
create table salesman_master_25(salesmanno varchar(6)primary key, salesmanname varchar(15)not null, address1 varchar(10)not null, address2 varchar(10), city varchar(10), pincode number(6), state varchar(12), salamt number(8,2)not null, tgttoget number(6,2)not null, ytdsales number(6,2)not null, remarks varchar(10), constraint chk_salesmanno check(salesmanno like 'S%'), constraint chk_salamt check(salamt!=0),constraint chk_tgttoget check(tgttoget!=0),constraint chk_ytdsales check(ytdsales!=0));
insert into salesman_master_25 values('S00001','Aman','A/14','Worli', 'Mumbai', 400002, 'Maharashtra', 3000, 100, 50,'Good');
insert into salesman_master_25 values('S00002','Omkar','65','Nariman', 'Mumbai', 400001, 'Maharashtra', 3000, 200, 100,'Good');
insert into salesman_master_25 values('S00003','Raj','P-7','Bandra', 'Mumbai', 400032, 'Maharashtra', 3000, 200, 100,'Good');
insert into salesman_master_25 values('S00004','Ashish','A/5','Juhu', 'Mumbai', 400044, 'Maharashtra', 3000, 200, 1000,'Good');


 
//forth table
create table sales_order_25(orderno varchar(6)primary key, clientno varchar(6)references client_master_25(clientno), orderdate date not null, delyaddr varchar(20), salesmanno varchar(6) references salesman_master_25(salesmanno), delytype char(1), billyn char(1), delydate date, orderstatus varchar(10), constraint chk_orderno check(orderno like 'O%'), constraint chk_delytype check(delytype in('p','f')),constraint chk_delydate check(delydate>orderdate), constraint chk_orderstatus check(orderstatus in('in process','fulfilled','backorder','cancelled')));
INSERT INTO sales_order_25 VALUES ('O19001', 'C00001', DATE '2004-06-12', '', 'S00001', 'f', 'n', DATE '2004-07-20', 'in process');
INSERT INTO sales_order_25 VALUES ('O19002', 'C00002', DATE '2004-06-25', '', 'S00002', 'p', 'n', DATE '2004-07-27', 'cancelled');
INSERT INTO sales_order_25 VALUES ('O46865', 'C00003', DATE '2004-02-18', '', 'S00003', 'f', 'y', DATE '2004-02-20', 'fulfilled');
INSERT INTO sales_order_25 VALUES ('O19003', 'C00004', DATE '2004-04-03', '', 'S00001', 'f', 'y', DATE '2004-04-07', 'fulfilled');
INSERT INTO sales_order_25 VALUES ('O46866', 'C00005', DATE '2004-05-20', '', 'S00002', 'p', 'n', DATE '2004-05-22', 'cancelled');
INSERT INTO sales_order_25 VALUES ('O19008', 'C00006', DATE '2004-05-24', '', 'S00004', 'f', 'y', DATE '2004-07-04', 'fulfilled');

//fifth table
create table sales_order_details_25(orderno varchar(6) references sales_order_25(orderno), productno varchar(6) references product_master_25(productno), qtyordered number(8), qtydiso number(6), productrate number(10,2));
insert into sales_order_details_25 values('O19001', 'P00001', 4, 4, 525);
insert into sales_order_details_25 values('O19001', 'P07965', 2, 1, 8400);
insert into sales_order_details_25 values('O19001', 'P07885', 2, 1, 5250);
insert into sales_order_details_25 values('O19002', 'P00001', 10, 0, 525);
insert into sales_order_details_25 values('O46865', 'P07868', 3, 3, 3150);
insert into sales_order_details_25 values('O46865', 'P07885', 3, 1, 5250);
insert into sales_order_details_25 values('O46865', 'P00001', 10, 10, 525);
insert into sales_order_details_25 values('O46865', 'P0345', 4, 4, 1050);
insert into sales_order_details_25 values('O19003', 'P0345', 2, 2, 1050);
insert into sales_order_details_25 values('O19003', 'P06734', 1, 1, 12000);
insert into sales_order_details_25 values('O46866', 'P07965', 1, 0, 8400);
insert into sales_order_details_25 values('O46866', 'P07975', 1, 0, 1050);
insert into sales_order_details_25 values('O19008', 'P00001', 10, 5, 525);
insert into sales_order_details_25 values('O19008', 'P07975', 5, 3, 1050);



[A] Perform the following computations on table data: 
1. List the names of all clients having ‘a’ as the second letter in their names. 
SELECT NAME FROM CLIENT_MASTER_25 WHERE NAME LIKE '_a%';

2. List the clients who stay in a city whose First letter is ‘M’. 
SELECT * FROM CLIENT_MASTER_25 WHERE CITY LIKE 'M%';

3. List all the clients who stay in ‘Bangalore’ or ‘Mangalore’.
SELECT * FROM CLIENT_MASTER_25 WHERE CITY IN ('Bangalore', 'Mangalore');
 
4. List all clients whose BalDue is greater then value 10000. 
SELECT * FROM CLIENT_MASTER_25 WHERE BALDUE > 10000;

5. List all information from the Sales_Order table for orders placed in the month of June. 
SELECT * FROM SALES_ORDER_25 WHERE TO_CHAR(ORDERDATE, 'MM') = '06';

6. List the order information for ClientNo. ‘C00001’ and ‘C00002’.
SELECT * FROM SALES_ORDER_25 WHERE CLIENTNO IN ('C00001', 'C00002');
 
7. List products whose selling price is greater than 500 and less than or equal to 750. 
SELECT * FROM PRODUCT_MASTER_25 WHERE SELLPRICE > 500 AND SELLPRICE <= 750;

8. List product whose selling price is more than 500.
SELECT * FROM PRODUCT_MASTER_25 WHERE SELLPRICE > 500;
 
9. Calculate a new selling price as, original selling price *0.15.
 SELECT PRODUCTNO, DESCRIPTION, SELLPRICE * 0.15 AS new_price FROM PRODUCT_MASTER_23;

10. Rename the new column in the output of the above query as new_price. 
11. List the names, city and state of clients who are not in the state of ‘Maharashtra’.
SELECT NAME, CITY, STATE FROM CLIENT_MASTER_25 WHERE STATE <> 'Maharashtra';
 
12. Calculate the average price of all the products. 
SELECT AVG(SELLPRICE) AS avg_price FROM PRODUCT_MASTER_25;

13. Determine the maximum and minimum product prices. Rename the output as max_price and min_price 
respectively. 
SELECT MAX(SELLPRICE) AS max_price, MIN(SELLPRICE) AS min_price FROM PRODUCT_MASTER_25;

14. Count the number of products having price less than or equal to 500.
SELECT COUNT(*) FROM PRODUCT_MASTER_25 WHERE SELLPRICE <= 500;
 
15. List all the products whose QtyOnHand is less than reorder level. 
SELECT * FROM PRODUCT_MASTER_25 WHERE QTYONHAND < REORDERLVL;


[B] Exercise on Date Manipulation: 
1. List the order number and day on which clients placed their order. 
SELECT ORDERNO, TO_CHAR(ORDERDATE, 'Day') AS ORDER_DAY FROM SALES_ORDER_25;

2. List the month (in alphabets) and date when the orders must be delivered. 
SELECT TO_CHAR(DELYDATE, 'Month') AS MONTH_NAME, TO_CHAR(DELYDATE, 'DD') AS DAY FROM SALES_ORDER_25;

3. List the Order Date in the format ‘DD-Month-YY’. E.g. 20-November-02.
SELECT TO_CHAR(ORDERDATE, 'DD-Month-YY') AS FORMATTED_DATE FROM SALES_ORDER_25;
 
4. List the date, 15 days after today’s date. 
SELECT SYSDATE + 15 AS DATE_AFTER_15_DAYS FROM DUAL;


 
[C] Exercise on using Having and Group By Clauses: 
1. Print the description and total qty sold for each product. 
SELECT P.DESCRIPTION, SUM(SOD.QTYDISO) AS TOTAL_QTY
FROM SALES_ORDER_DETAILS_25 SOD
JOIN PRODUCT_MASTER_25 P ON SOD.PRODUCTNO = P.PRODUCTNO
GROUP BY P.DESCRIPTION;

2. Find the values of each product sold. 
SELECT PRODUCTNO, SUM(QTYDISO * PRODUCTRATE) AS TOTAL_VALUE
FROM SALES_ORDER_DETAILS_25
GROUP BY PRODUCTNO;

3. Calculate the average qty sold for each client that has maximum order value of 15000.00. 
SELECT S.CLIENTNO, AVG(SOD.QTYDISO) AS AVG_QTY
FROM SALES_ORDER_DETAILS_25 SOD
JOIN SALES_ORDER_25 S ON SOD.ORDERNO = S.ORDERNO
GROUP BY S.CLIENTNO
HAVING MAX(SOD.QTYDISO * PRODUCTRATE) <= 15000;

4. Find out the total of all the billed orders for the month of June. 
SELECT SUM(SOD.QTYDISO * PRODUCTRATE) AS TOTAL_BILLED
FROM SALES_ORDER_DETAILS_25 SOD
JOIN SALES_ORDER_25 S ON SOD.ORDERNO = S.ORDERNO
WHERE TO_CHAR(S.ORDERDATE, 'MM') = '06' AND S.BILLYN = 'Y';
 
[D] Exercise on Joins and Correlation: 
1. Find out the products, which have been sold to ‘Rakesh Joshi’.
SELECT DISTINCT P.PRODUCTNO, P.DESCRIPTION
FROM CLIENT_MASTER_25 C
JOIN SALES_ORDER_25 SO ON C.CLIENTNO = SO.CLIENTNO
JOIN SALES_ORDER_DETAILS_25 SOD ON SO.ORDERNO = SOD.ORDERNO
JOIN PRODUCT_MASTER_25 P ON SOD.PRODUCTNO = P.PRODUCTNO
WHERE C.NAME = 'Rakesh Joshi';
 
2. Find out the products and their quantities that will have to be delivered in the current month. 
SELECT P.PRODUCTNO, P.DESCRIPTION, SOD.QTYDISO AS QUANTITY FROM SALES_ORDER_25 SO JOIN SALES_ORDER_DETAILS_25 SOD ON SO.ORDERNO = SOD.ORDERNO JOIN PRODUCT_MASTER_25 P ON SOD.PRODUCTNO = P.PRODUCTNO WHERE TO_CHAR(SO.DELYDATE, 'MM') = TO_CHAR(SYSDATE, 'MM') AND TO_CHAR(SO.DELYDATE, 'YYYY') = TO_CHAR(SYSDATE, 'YYYY');

3. List the ProductNo and description of constantly sold (i.e. rapidly moving) products.
SELECT P.PRODUCTNO, P.DESCRIPTION FROM PRODUCT_MASTER_25 P JOIN SALES_ORDER_DETAILS_25 SOD ON P.PRODUCTNO = SOD.PRODUCTNO GROUP BY P.PRODUCTNO, P.DESCRIPTION HAVING COUNT(DISTINCT SOD.ORDERNO) > 1;
 
4. Find the names of clients who have purchased ‘Trousers’. 
SELECT DISTINCT C.NAME FROM CLIENT_MASTER_25 C JOIN SALES_ORDER_25 SO ON C.CLIENTNO = SO.CLIENTNO JOIN SALES_ORDER_DETAILS_25 SOD ON SO.ORDERNO = SOD.ORDERNO JOIN PRODUCT_MASTER_25 P ON SOD.PRODUCTNO = P.PRODUCTNO WHERE P.DESCRIPTION = 'Trouser';

5. List the products and orders from customers who have ordered less than 5 units of ‘Pull Overs’. 
SELECT SO.ORDERNO, C.NAME AS CLIENT_NAME, P.PRODUCTNO, P.DESCRIPTION, SOD.QTYORDERED FROM CLIENT_MASTER_25 C JOIN SALES_ORDER_25 SO ON C.CLIENTNO = SO.CLIENTNO JOIN SALES_ORDER_DETAILS_25 SOD ON SO.ORDERNO = SOD.ORDERNO JOIN PRODUCT_MASTER_25 P ON SOD.PRODUCTNO = P.PRODUCTNO WHERE P.DESCRIPTION = 'Pull Over' AND SOD.QTYORDERED < 5;

6. Find the products and their quantities for the orders placed by ‘Rakesh Joshi’ and ‘Mayur Patel’. 
SELECT C.NAME AS CLIENT_NAME, P.PRODUCTNO, P.DESCRIPTION, SOD.QTYDISO AS QUANTITY_DELIVERED FROM CLIENT_MASTER_25 C JOIN SALES_ORDER_25 SO ON C.CLIENTNO = SO.CLIENTNO JOIN SALES_ORDER_DETAILS_25 SOD ON SO.ORDERNO = SOD.ORDERNO JOIN PRODUCT_MASTER_25 P ON SOD.PRODUCTNO = P.PRODUCTNO WHERE C.NAME IN ('Rakesh Joshi', 'Mayur Patel');

7. Find the products and their quantities for the orders placed by ClientNo ‘C00001’ and ‘C00002’.
SELECT SO.CLIENTNO, P.PRODUCTNO, P.DESCRIPTION, SOD.QTYDISO AS QUANTITY_DELIVERED FROM SALES_ORDER_25 SO JOIN SALES_ORDER_DETAILS_25 SOD ON SO.ORDERNO = SOD.ORDERNO JOIN PRODUCT_MASTER_25 P ON SOD.PRODUCTNO = P.PRODUCTNO WHERE SO.CLIENTNO IN ('C00001', 'C00002'); 
 
[E] Exercise on Sub-queries: 
1. Find the ProductNo and description of non-moving products i.e. products not being sold. 
SELECT PRODUCTNO, DESCRIPTION FROM PRODUCT_MASTER_25 WHERE PRODUCTNO NOT IN ( SELECT DISTINCT PRODUCTNO FROM SALES_ORDER_DETAILS_25);

2. List the CustomerName, Address1, Address2, City and Pin Code for the client who has placed order no ‘O19001’. 
SELECT C.NAME AS CUSTOMER_NAME, C.ADDRESS1, C.ADDRESS2, C.CITY, C.PINCODE FROM CLIENT_MASTER_25 C JOIN SALES_ORDER_25 S ON C.CLIENTNO = S.CLIENTNO WHERE S.ORDERNO = 'O19001';

3. List the client names that have placed orders before the month of May-04 
SELECT DISTINCT C.NAME FROM CLIENT_MASTER_25 C JOIN SALES_ORDER_25 S ON C.CLIENTNO = S.CLIENTNO WHERE S.ORDERDATE < DATE '2004-05-01';

4. List if the product ‘Lycra Top’ has been ordered by any client and print the Client No.,  
              Name to whom it was sold. 
SELECT DISTINCT C.CLIENTNO, C.NAME FROM CLIENT_MASTER_25 C JOIN SALES_ORDER_25 SO ON C.CLIENTNO = SO.CLIENTNO JOIN SALES_ORDER_DETAILS_25 SOD ON SO.ORDERNO = SOD.ORDERNO JOIN PRODUCT_MASTER_25 P ON SOD.PRODUCTNO = P.PRODUCTNO WHERE P.DESCRIPTION = 'Lycra Tops';

5. List the names of clients who have placed orders worth Rs. 10000 or more. 
SELECT C.NAME, SUM(SOD.QTYDISO * SOD.PRODUCTRATE) AS TOTAL_ORDER_VALUE FROM CLIENT_MASTER_25 C JOIN SALES_ORDER_25 SO ON C.CLIENTNO = SO.CLIENTNO JOIN SALES_ORDER_DETAILS_25 SOD ON SO.ORDERNO = SOD.ORDERNO GROUP BY C.NAME HAVING SUM(SOD.QTYDISO * SOD.PRODUCTRATE) >= 10000;






declare
     nu1 number(2):=12;
begin
     if(nu1>99) then
          dbms_output.put_line('Bigest');
      else
          dbms_output.put_line('Smaller');
     end if;
end;

create table deluxe (id number(6), name char(10), city char(10));
desc deluxe
desc root
select*from deluxe
select*from root
select id, name from deluxe
select *from deluxe where name='Vipul'
select id,city from deluxe where name='John'
insert into deluxe values (012389, 'John', 'Chittal');
insert into deluxe(id, name, city)values(121220,'pop','perth');
insert into deluxe values(:id, :name, :city);
alter table deluxe add(mobileNo number(10));
alter table deluxe drop (mobileNo);
alter table deluxe rename city to address
alter table deluxe rename to root
alter table root modify(name varchar(10));
alter table root modify(address varchar(20));

