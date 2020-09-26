# simple_sqlalch_pgres
A pythonic way to interact with postgreSQL databases to query data as pandas dataframe for manipulation,  
cleaning, analysis, and visualization. A simplified SQL Alchemy integration for postgreSQL databases with  
(or without) ssh enabled. Check out my story post about this repo [here](https://medium.com/@erikyan02/how-to-query-postgresql-using-python-with-ssh-in-3-steps-cde626444817)
  
### Includes functionality from:
1. SSHTunnelForwarder  
2. Paramiko
3. SQL Alchemy  
4. Pandas  

### ASSUMPTIONS:
1. Must initiate psql_user and psql_password arguments to successfully access postgres remotely.  
Best practice is to use environment variables, however getpass may be used in-place  
2. SSH currently only supports pem certificate authentication 

### EXAMPLES:
  
p_host = '123.0.0.0'  
p_port = 5432  
db = 'database_name'  
ssh = True  
ssh_user = 'ssh_user'  
ssh_host = 'ip address or web address'  
ssh_pkey = '/path/to/user_authentication.pem'  
pgres = Postgresql_connect(pgres_host=p_host, pgres_port=p_port, db=db, ssh=ssh, ssh_user=ssh_user, ssh_host=ssh_host, ssh_pkey=ssh_pkey)  
#initiates connection to PostgreSQL database. In this instance we use ssh and must specify our ssh credentials.
  
pgres.schemas(db='database_name')  
#returns the number of schemas and all schema names within the specified database as a pandas dataframe  
  
  
pgres.tables(db='database_name',schema='schema_name')  
#returns the number of tables and all table names within the specified schema as a pandas dataframe  
  
  
sql_statement = """  
    SELECT column_name, data_type  
    FROM information_schema.columns  
    WHERE table_name = 'ey_test_table'  
    ;  
    """  
query_df = pgres.query(db='database_name', query=sql_statement)  
query_df  
#returns the results of an sql statement as a pandas dataframe. 
#This example returns the column names and data types of table 'ey_test_table'.
