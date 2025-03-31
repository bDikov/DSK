# Credit Information Retrieval API  

## Task  
Implement a REST API to retrieve credit information.  

## Description  
You are part of the team developing an ASP.NET application for processing credits. Each credit contains:  
- Credit number  
- Client name  
- Requested amount  
- Credit request date  
- Credit status  

The statuses can be - Paid, AwaitingPayment, Created.  

For each credit, an unlimited number of invoices can be attached. Each invoice contains:  
- Invoice number  
- Invoice amount  

## Requirements  
1. Describe how you would structure the database containing this information (describe the tables and the relationships between them).  
2. Use an in-memory SQLite database for the purposes of this task. Create the tables and insert test data into them (each time the application starts).  
3. Create two endpoints that return the following information:  
   - An endpoint that returns all credits with information about the invoices for each credit.  
   - An endpoint that returns the total sum of credits with the "Paid" status, the total sum of credits with the "AwaitingPayment" status, and the percentage of each of these amounts in relation to the total sum of all credits with the statuses "Paid" and "AwaitingPayment".  

### Additional requirements:  
- Add necessary tests to validate that the task has been completed.  
- Use Dapper for all SQL queries.  
