# FINAL-PROJECT
CREATE DATABASE LIBRARY;
USE LIBRARY;

CREATE TABLE Branch(Branch_no INT PRIMARY KEY,
Manager_Id VARCHAR(10),
Branch_address VARCHAR(50),
Contact_no BIGINT);

INSERT INTO Branch VALUES(1,'101','ERNAKULAM',9999999999);
INSERT INTO Branch VALUES(2,'102','KOZHIKODE',9999998889);
INSERT INTO Branch VALUES(3,'103','KANNUR',9900099999);
INSERT INTO Branch VALUES(4,'104','MALAPPURAM',9996669999);
INSERT INTO Branch VALUES(5,'105','WAYNAD',9999997779);
INSERT INTO Branch VALUES(6,'106','IDUKKI',9993339999);
INSERT INTO Branch VALUES(7,'107','ALAPPUZHA',9922299999);

select * from Branch;

CREATE TABLE Employee(Emp_Id VARCHAR(10) PRIMARY KEY,
Emp_name VARCHAR(20),
Position VARCHAR(20),
Salary INT);

INSERT INTO Employee VALUES('101','AYSHA','MANAGER',56000);
INSERT INTO Employee VALUES('102','BEEGAM','ASSISTANT MANAGER',51000);
INSERT INTO Employee VALUES('103','NYNA','DEPARTMENT HEAD',23000);
INSERT INTO Employee VALUES('104','NYHA','CLERK',50000);
INSERT INTO Employee VALUES('105','FASIL','HELPER',7000);
INSERT INTO Employee VALUES('106','MUHAMMED','DEPARTMENT STAFF',43000);
INSERT INTO Employee VALUES('107','SONU','ASSISTANT',45000);

SELECT * FROM Employee;


CREATE TABLE Customer(Customer_Id INT PRIMARY KEY,
Customer_name VARCHAR(20),
Customer_address VARCHAR(50),
Reg_date DATE);

INSERT INTO Customer VALUES(1000,'abcd','elettil','2021-01-01');
INSERT INTO Customer VALUES(1001,'abcde','thamarassery','2021-08-01');
INSERT INTO Customer VALUES(1002,'abcdef','malayattoor','2021-09-01');
INSERT INTO Customer VALUES(1003,'abcdefg','kodanad','2022-01-01');
INSERT INTO Customer VALUES(1004,'abcdefgh','batheri','2021-09-09');
INSERT INTO Customer VALUES(1005,'abcdfg','bandipur','2022-08-01');

select * from Customer;

CREATE TABLE IssueStatus(Issue_Id INT PRIMARY KEY,
Issued_cust INT, 
Issued_book_name VARCHAR(50),
Issue_date DATE,
Isbn_book INT,FOREIGN KEY (Issued_cust) references Customer(Customer_Id),
foreign key (Isbn_book) references Books(ISBN));

INSERT INTO IssueStatus VALUES(500,1000,'i too had a love story','2023-06-03',200);
INSERT INTO IssueStatus VALUES(501,1000,'can love happens twice','2022-03-03',201);
INSERT INTO IssueStatus VALUES(502,1003,'pathummayude aadu','2023-06-08',202);
INSERT INTO IssueStatus VALUES(503,1003,'aadu jeevitham','2023-05-03',203);
INSERT INTO IssueStatus VALUES(504,1004,'i too had a love','2023-06-05',204);
INSERT INTO IssueStatus VALUES(505,1005,'history returns','2022-09-03',205);
INSERT INTO IssueStatus VALUES(506,1000,'a look back to history','2023-06-04',206);
INSERT INTO IssueStatus VALUES(507,1004,'wings of fire','2023-06-03',207);
INSERT INTO IssueStatus VALUES(508,1005,'my story','2023-03-03',208);
INSERT INTO IssueStatus VALUES(509,1003,'i too had a story','2023-03-04',209);

select * from IssueStatus;

CREATE TABLE ReturnStatus(Return_Id INT PRIMARY KEY,
Return_cust INT,
Return_book_name VARCHAR(30),
Return_date DATE,
Isbn_book2 INT,FOREIGN KEY (Isbn_book2) references Books(ISBN));

INSERT INTO ReturnStatus VALUES(400,1000,'can love happens twice','2022-06-03',201);
INSERT INTO ReturnStatus VALUES(401,1003,'aadu jeevitham','2023-06-03',203);
INSERT INTO ReturnStatus VALUES(402,1005,'history returns','2022-10-03',205);
INSERT INTO ReturnStatus VALUES(403,1004,'wings of fire','2023-08-03',207);
INSERT INTO ReturnStatus VALUES(404,1003,'i too had a story','2023-06-03',209);

select * from ReturnStatus;
 
 CREATE TABLE Books(ISBN INT PRIMARY KEY, 
Book_title VARCHAR(50),
Category VARCHAR(20),
Rental_Price INT,
Status VARCHAR(5), 
Author VARCHAR(30),
Publisher VARCHAR(50));

INSERT INTO Books VALUES(200,'i too had a love story','politics',300,'no','aysha','sk publications');
INSERT INTO Books VALUES(201,'can love happens twice','politics',301,'yes','fazy','nyha publications');
INSERT INTO Books VALUES(202,'pathummayude aadu','politics',302,'no','nyna','pl publications');
INSERT INTO Books VALUES(203,'aadu jeevitham','love',303,'yes','nyha','op publications');
INSERT INTO Books VALUES(204,'i too had a love','love',304,'no','sonu','lk publications');
INSERT INTO Books VALUES(205,'history returns','love',305,'yes','shaja','adc publications');
INSERT INTO Books VALUES(206,'a look back to history','love',306,'no','sunisha','abc publications');
INSERT INTO Books VALUES(207,'wings of fire','history',307,'yes','sree','sk publications');
INSERT INTO Books VALUES(208,'my story','history',308,'no','riza','adc publications');
INSERT INTO Books VALUES(209,'i too had a story','history',309,'yes','radin','sk publications');

SHOW tables;
select * from Books;

select Book_title,Category,Rental_Price from Books;

select Emp_name,salary from Employee order by Salary desc;

select Customer.Customer_name,IssueStatus.Issued_book_name from Customer inner join IssueStatus on Customer.Customer_Id=IssueStatus.Issued_cust;

select count(Book_title),Category from Books group by Category;

select Emp_name,Position from Employee where Salary > 50000;

select Customer.Customer_name from Customer left join IssueStatus on Customer.Customer_Id=IssueStatus.Issued_cust where Reg_date<'2022-01-01' and IssueStatus.Issued_cust is null;


select count(Employee.Emp_Id),Branch.Branch_no from Branch inner join Employee on Branch.Manager_Id=Employee.Emp_Id group by Branch.Branch_no;

select Customer.Customer_name from Customer inner join IssueStatus on Customer.Customer_Id=IssueStatus.Issued_cust where Issue_date like'2023-06-__';

select Book_title from Books where Book_title like '%history%';

select Branch.Branch_no,count(Employee.Emp_Id) from Branch inner join Employee on Branch.Manager_Id=Employee.Emp_Id group by Branch_no having count(Employee.Emp_Id)>5;
