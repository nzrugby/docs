# ASP.NET CORE APP Access SQL SERVER Docker on Linux
## 1. Pull sqlserver docker image from docker
      In ubuntu bash input: sudo docker pull microsoft.com/mssql-server-linux:latest
      Once pull operation finish you can type 'docker images' command to check this image
## 2. Run sqlserver container 
      In ubuntu bash input: sudo docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=<YourStrong!Passw0rd>' \
                                  -p 1433:1433 --name sql1 \
                                  -d microsoft.com/mssql-server-linux-latest
      This command will generate a sqlserver container in ubuntu. Use 'docker ps -a' command to check current containers. Now Sqlserver has already run in linux
## 3. Use code-first to connect to sqlserver docker
      Create a new console project in visual studio 2017 with .netcore 2.1
      Under the project folder creating a Student.cs file. This file includes the test model.
      Under the project folder creating a StudentDbContext.cs file which will be mapped to database in sqlserver.
      Inside StudentDbContext.cs includes following code:
        
        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            optionsBuilder.UseSqlServer(@"Server=192.168.1.67,1433;Database=dockertest;User ID=SA;Password=<YourStrong!Passw0rd>;");
        }
        
        'Server=192.168.1.67' means sqlsever ip address with 1433 port. 'Database=dockertest' means create a new database named dockertest in server. 'User ID=SA' means root login user is SA. SA is default system administrator.
             
      Under the project open program.cs and add following code:
      ![alt text](https://user-images.githubusercontent.com/31294078/47691778-4359ee00-dc58-11e8-9926-94821b1da323.png)
