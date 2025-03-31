# Implement a REST API to Retrieve Credit Information  

## Description  
You are part of the team developing an **ASP.NET** application for processing credits. Each credit contains the following information:  

- **Credit number**  
- **Client name**  
- **Requested amount**  
- **Credit request date**  
- **Credit status** (which can be: *Paid*, *AwaitingPayment*, or *Created*)  

Furthermore, for each credit, an unlimited number of invoices can be attached. Each invoice contains:  

- **Invoice number**  
- **Invoice amount**  

---  

## Requirements  

### 1. Database Structure  
To store the information regarding credits and invoices, we will structure the database with two main tables: `Credits` and `Invoices`.  

#### Table: Credits  
- **CreditId** (Primary Key, Integer, Auto-increment)  
- **CreditNumber** (String, Unique)  
- **ClientName** (String)  
- **RequestedAmount** (Decimal)  
- **RequestDate** (DateTime)  
- **Status** (String, can be 'Paid', 'AwaitingPayment', 'Created')  

#### Table: Invoices  
- **InvoiceId** (Primary Key, Integer, Auto-increment)  
- **InvoiceNumber** (String, Unique)  
- **InvoiceAmount** (Decimal)  
- **CreditId** (Foreign Key, Integer, references `Credits(CreditId)`)  

#### Relationships  
- A **one-to-many** relationship between `Credits` and `Invoices` (one credit can have multiple invoices).  

### 2. In-Memory SQLite Database  
For the purposes of this task, we will use an in-memory **SQLite** database. The application will create the necessary tables and insert test data each time it starts.  

#### Database Initialization Example  
```csharp  
using Microsoft.Data.Sqlite;  
using System.Data;  

public class DatabaseInitializer  
{  
    public static IDbConnection InitializeDatabase()  
    {  
        var connection = new SqliteConnection("DataSource=:memory:");  
        connection.Open();  

        using (var command = connection.CreateCommand())  
        {  
            command.CommandText = @"  
                CREATE TABLE Credits (  
                    CreditId INTEGER PRIMARY KEY AUTOINCREMENT,  
                    CreditNumber TEXT NOT NULL UNIQUE,  
                    ClientName TEXT NOT NULL,  
                    RequestedAmount REAL NOT NULL,  
                    RequestDate TEXT NOT NULL,  
                    Status TEXT NOT NULL  
                );  

                CREATE TABLE Invoices (  
                    InvoiceId INTEGER PRIMARY KEY AUTOINCREMENT,  
                    InvoiceNumber TEXT NOT NULL UNIQUE,  
                    InvoiceAmount REAL NOT NULL,  
                    CreditId INTEGER NOT NULL,  
                    FOREIGN KEY (CreditId) REFERENCES Credits(CreditId)  
                );  
            ";  
            command.ExecuteNonQuery();  
        }  

        // Insert test data here...  

        return connection;  
    }  
}  
