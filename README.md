# First_repository
This is my first GitHub Repository<br>
<b><h1>
Author- NIRAVBHAI</h1><b>
CREATE TABLE client_master_25 (
  clientno VARCHAR2(6) PRIMARY KEY,
  name VARCHAR2(15) NOT NULL,
  address1 VARCHAR2(5),
  address2 VARCHAR2(5),
  city VARCHAR2(15),
  pincode NUMBER(6),
  state VARCHAR2(15),
  baldue NUMBER(10,2),
  CONSTRAINT chk_cliet CHECK (clientno LIKE 'C%')
);
desc client_master_25 
select*from client_master_25;
insert into client_master_25 values('C00001','Rakesh Joshi', NULL, NULL, 'Mumbai', 400054,'Maharashtra', 15000)
insert into client_master_25 values('C00002','Mayur Patel', NULL, NULL, 'Madras', 780001,'Tamilnadu', 0)
insert INTO CLIENT_MASTER_25 VALUES ('C00003', 'Ishita Mehta', NULL, NULL, 'Mumbai', 400057, 'Maharashtra', 5000);
INSERT INTO CLIENT_MASTER_25 VALUES ('C00004', 'Amit Solanki', NULL, NULL, 'Bangalore', 560001, 'Karnataka', 0);
INSERT INTO CLIENT_MASTER_25 VALUES ('C00005', 'Hiren Pandya', NULL, NULL, 'Mumbai', 400060, 'Maharashtra', 2000);
INSERT INTO CLIENT_MASTER_25 VALUES ('C00006', 'Dipak Sharma', NULL, NULL, 'Mangalore', 560050, 'Karnataka', 0);


//second table

CREATE TABLE product_master_25 (
    productno     VARCHAR2(6) PRIMARY KEY,
    description   VARCHAR2(15) NOT NULL,
    profitpercent NUMBER(4,2) NOT NULL,
    unitmaster    VARCHAR2(7) NOT NULL,
    qtyonhand     NUMBER(4) NOT NULL,
    reorderlvl    NUMBER(3) NOT NULL,
    sellprice     NUMBER(5,2) NOT NULL,
    costprice     NUMBER(5,2) NOT NULL,
    CONSTRAINT chk_productno CHECK (productno LIKE 'P%'),
    CONSTRAINT chk_sellprice CHECK (sellprice != 0),
    CONSTRAINT chk_costprice CHECK (costprice != 0)
);
desc product_master_25
select*from product_master_25
iNSERT INTO PRODUCT_MASTER_25 VALUES ('P00001', 'T-Shirts', 5, 'Piece', 200, 50, 350, 250);
INSERT INTO PRODUCT_MASTER_25 VALUES ('P0345', 'Shirts', 6, 'Piece', 150, 50, 500, 350);
INSERT INTO PRODUCT_MASTER_25 VALUES ('P06734', 'Cotton Jeans', 5, 'Piece', 100, 20, 600, 450);
INSERT INTO PRODUCT_MASTER_25 VALUES ('P07865', 'Jeans', 5, 'Piece', 100, 20, 750, 500);
INSERT INTO PRODUCT_MASTER_25 VALUES ('P07868', 'Trousers', 2, 'Piece', 150, 50, 850, 550);
INSERT INTO PRODUCT_MASTER_25 VALUES ('P07885', 'Pull Overs', 2.5, 'Piece', 80, 30, 700, 450);
INSERT INTO PRODUCT_MASTER_25 VALUES ('P07965', 'Denim Shirts', 4, 'Piece', 100, 40, 350, 250);
INSERT INTO PRODUCT_MASTER_25 VALUES ('P07975', 'Lycra Tops', 5, 'Piece', 70, 30, 300, 175);
INSERT INTO PRODUCT_MASTER_25 VALUES ('P08865', 'Skirts', 5, 'Piece', 75, 30, 450, 300);

//third table

create table salesman_master_25 (salesmanno varchar(6)primary key, salesmanname varchar(15)not null, address1 varchar(10)not null, address2 varchar(10), city varchar(10), pincode number(6), state varchar(12), salamt number(8,2)not null, tgttoget number(6,2)not null, ytdsales number(6,2)not null, remarks varchar(10), constraint chk_salesmanno check(salesmanno like 'S%'), constraint chk_salamt check(salamt!=0), constraint chk_tgttoget check(tgttoget!=0), constraint chk_ytdsales check(ytdsales!=0));
desc salesman_master_25
select*from  salesman_master_25
INSERT INTO SALESMAN_MASTER_25 VALUES ('S00001', 'Aman', 'A/14 Worli', NULL, 'Mumbai', 400002, 'Maharashtra', 3000, 100, 50, 'Good');
INSERT INTO SALESMAN_MASTER_25 VALUES ('S00002', 'Omkar', '65 Nariman', NULL, 'Mumbai', 400001, 'Maharashtra', 3000, 200, 100, 'Good');
INSERT INTO SALESMAN_MASTER_25 VALUES ('S00003', 'Raj', 'P-7 Bandra', NULL, 'Mumbai', 400032, 'Maharashtra', 3000, 200, 100, 'Good');
INSERT INTO SALESMAN_MASTER_25 VALUES ('S00004', 'Ashish', 'A/5 Juhu', NULL, 'Mumbai', 400044, 'Maharashtra', 3000, 200, 100, 'Good');

//forth table

CREATE TABLE sales_order_25 (
    orderno      VARCHAR2(6) PRIMARY KEY,
    clientno     VARCHAR2(6) REFERENCES client_master_25(clientno),
    orderdate    DATE NOT NULL,
    delyaddr     VARCHAR2(20),
    salesmanno   VARCHAR2(6) REFERENCES salesman_master_25(salesmanno),
    delytype     CHAR(1),
    billyn       CHAR(1),
    delydate     DATE,
    orderstatus  VARCHAR2(10),
    
    CONSTRAINT chk_orderno CHECK (orderno LIKE 'O%'),
    CONSTRAINT chk_delytype CHECK (delytype IN ('p', 'f')),
    CONSTRAINT chk_delydate CHECK (delydate > orderdate),
    CONSTRAINT chk_orderstatus CHECK (
        orderstatus IN ('in process', 'fulfilled', 'backorder', 'cancelled')
    )
);
