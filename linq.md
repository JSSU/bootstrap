Use Entity Framework connect data from database in code behind:

+ Find the Entity Container Name --[Entity Container Name]
+ In  `code behind` use LINQ:
    * Create context use LINQ: var query = from it(whatever name) in [Entity Container Name].[Table Name]
    * query is everything in table and could use:
        ```
            foreach (var res in query)
                Console.WriteLine("{0} | {1} | {2}", res.ID, res.Agency_Name, res.Ini);
        ```
    * Bind Gridview:
        ```
            [GridView ID].DataSource = query;
            [GridView ID].DataBind();
        ```


var personIni = dbcontext.New_DPW_Manager
                .Where(p => p.ID == 1)
                .Select(p=>p.Ini)
                .ToArray();
//.FirstOrDefault()

/** Insert **/
```
public void LinqToSqlInsert01() {
    var q =
        from c in db.Customers
        where c.Region == "WA"
        select c;

    Console.WriteLine("*** BEFORE ***");
    ObjectDumper.Write(q);

    Console.WriteLine();
    Console.WriteLine("*** INSERT ***");
    var newCustomer = new Customer { CustomerID = "MCSFT",
                                     CompanyName = "Microsoft",
                                     ContactName = "John Doe",
                                     ContactTitle = "Sales Manager",
                                     Address = "1 Microsoft Way",
                                     City = "Redmond",
                                     Region = "WA",
                                     PostalCode = "98052",
                                     Country = "USA",
                                     Phone = "(425) 555-1234",
                                     Fax = null
                                   };
    db.Customers.InsertOnSubmit(newCustomer);
    db.SubmitChanges();

    Console.WriteLine();
    Console.WriteLine("*** AFTER ***");
    ObjectDumper.Write(q);

    Cleanup64();  // Restore previous database state
}
```
/** Update **/
```
public void LinqToSqlInsert04() {
    var q =
        from c in db.Customers
        where c.CustomerID == "ALFKI"
        select c;

    Console.WriteLine("*** BEFORE ***");
    ObjectDumper.Write(q);

    Console.WriteLine();
    Console.WriteLine("*** UPDATE ***");
    Customer cust = db.Customers.First(c => c.CustomerID == "ALFKI");
    cust.ContactTitle = "Vice President";
    db.SubmitChanges();

    Console.WriteLine();
    Console.WriteLine("*** AFTER ***");
    ObjectDumper.Write(q);

    Cleanup67();  // Restore previous database state
}
```
//-------------============--------------------
Northwnd db = new Northwnd(@"c:\Northwnd.mdf");

// Query for a specific customer.
var cust =
    (from c in db.Customers
     where c.CustomerID == "ALFKI"
     select c).First();

// Change the name of the contact.
cust.ContactName = "New Contact";

// Create and add a new Order to the Orders collection.
Order ord = new Order { OrderDate = DateTime.Now };
cust.Orders.Add(ord);

// Delete an existing Order.
Order ord0 = cust.Orders[0];

// Removing it from the table also removes it from the Customer’s list.
db.Orders.DeleteOnSubmit(ord0);

// Ask the DataContext to save all the changes.
db.SubmitChanges();
//---------------------------------------------------
/** delete **/
```
public void LinqToSqlInsert06() {
    Console.WriteLine("*** BEFORE ***");
    ObjectDumper.Write(from c in db.OrderDetails
                              where c.OrderID == 10255
                              select c);

    Console.WriteLine();
    Console.WriteLine("*** DELETE ***");
    //Beverages
    //[table]                 [database][table]     [c]is a colum  
    OrderDetail orderDetail = db.OrderDetails.First(c => c.OrderID == 10255 && c.ProductID == 36);

    db.OrderDetails.DeleteOnSubmit(orderDetail);
    db.SubmitChanges();

    Console.WriteLine();
    Console.WriteLine("*** AFTER ***");
    ClearDBCache();
    ObjectDumper.Write(from c in db.OrderDetails where c.OrderID == 10255 select c);

    Cleanup69();  // Restore previous database state
}
```


You need to add reference to System.Data.Linq assembly in your test project. The assembly reference is added to your main project when creating dbml file (data context). in order to use all of the LinqToSQL functionality, you need to reference System.Data.Linq in all of the projects where DataContext is used.

```
            //var dbchange = (from it in dbcontext.New_DPW_Manager
            //                select it
            //           ).First();

            var db = (from it in dbcontext.New_DPW_Manager
                            select it
                       ).ToArray();
            var dbchange = db[0];
            //create table class
            New_DPW_Manager managerdb=new New_DPW_Manager();
            managerdb.M_Name = mainName.Value;
            //dbchange.M_Name = mainName.Value;

            DirName.Value = mainName.Value;
            DirTitle.Value = dbcontext.SaveChanges().ToString();
            //dbchange.M_Name = mainName.Value;
            //dbchange.M_Title = mainTitle.Value;
            //dbchange.Tel = mainTel.Value;
            //dbchange.Email = mainEmail.Value;
            //dbchange.Office_Address = mainAddress.Value;
            //dbchange.Department = mainDepartment.Value;
            //dbchange.Agency_Name = mainAgency.Value;
            //DirName.Value = dbcontext.SaveChanges().ToString();
```

