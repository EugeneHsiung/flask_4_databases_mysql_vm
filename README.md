# flask_4_databases_mysql_vm

# Azure setup 
1. Go to Microsoft Azure, click on hambuger sign, virtual machines, create
2. create resource group, create VM name, Size: Standard_B1ms
3. Under `Administrator account`, `Authentication type`, click `password` , create password 
4. Under `Inbound port rules`, `Select inbound ports`, drop down, click HTTP, HTTPS, SSH
5. click next until review + create, click create and let the deployment complete
6. click go to resource, under Networking, go to network settings, click create port rule, inbound port rule,
7. Under `Destination port ranges`, change `Destination port range` to `3306` and add
8. Go to google shell, in the terminal, type in `ssh usernname@public ip address`
9. Type in `Y`, and type in password, click enter. Terminal should show: usernmae@VMname
10. Type in `sudo apt-get update` and enter, type in `sudo apt install mysql-server mysql-client` and enter, click Y
11. Type in `sudo mysql` and your terminal should say "mysql"
12. Type in `show databases;` to show existing databases 
13. Type in `CREATE USER 'username'@'%' IDENTIFIED BY 'password';`
14. To confirm type in: `select user from mysql.user;`
15. Type in `GRANT ALL PRIVILEGES ON *.* TO 'username'@'%' WITH GRANT OPTION;`
16. To confirm: `show grants for Eugenius;` type in `\quit`, `sudo nano /etc/mysql/mysql.conf.d/mysqld.cnf`, scroll down to blind-address and type in 0.0.0.0, click control O, enter, control X
17. Type in: `/etc/init.d/mysql restart`, enter password
18. Go to MySQL Workbench, press +, type in a connection name, copy ip address, make sure port is 3306, type in password
19. Go to MySQL workbench and press create, put in your IP address, user name, and password from the shell.
20. Test connection and press Ok 

# MySQL Workbench Database
- In MySQL workbench, create a database:
  
```
create database heart; 
use heart; 
CREATE TABLE patients (
    patient_id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    date_of_birth DATE
);

CREATE TABLE medications (
    medication_id INT PRIMARY KEY AUTO_INCREMENT,
    medication_name VARCHAR(100) NOT NULL
);
```

- Create fake data:
  
```
INSERT INTO patients (first_name, last_name, date_of_birth) VALUES 
('john', 'smith', '1921-10-15'),
('kait', 'mom', '1911-10-17'),
('bob', 'hum', '1931-10-20');

INSERT INTO medications (medication_id,medication_name) VALUES
(1, 'ibuprofen'), 
(2, 'albuterol'), 
(3, 'laxis');
```
# Flask integration: 
1. I resued templates from the previous flask [assignment](https://github.com/EugeneHsiung/azure_flask_deployment1) and included a ```base.html``` , ```medications.html``` , and ```patients.html``` . These html files are representative of the database created in MySQL workbench. 
2. The contents of the html files are shown in this [folder](https://github.com/EugeneHsiung/flask_4_databases_mysql_vm/blob/main/templates/base.html)
3. A ```.gitignore``` file was created and inside the file has a ```.env``` file. This was created to store the IP address of the VM (virtual machine), database name, username, and password
4. Lastly, I modified the app.py file with the appropriate html files. The contents can be seen in this [file](https://github.com/EugeneHsiung/flask_4_databases_mysql_vm/blob/main/app.py)
