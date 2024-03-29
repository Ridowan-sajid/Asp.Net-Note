# Asp.Net-Note

## ASP.net MVC

**Asp.Net MVC is a tool to create website which is design based on MVC(Model View Controller)**

# To Start

**To create website with asp.net we need to choose the option on picture given below.**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/1.png)

**Next**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Basic1.png)

# Structure of Asp.Net
|  Image      | Description |
| ----------- | ----------- |
| ![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/2.png) | * In **App Start** We have **RouterConfig.cs** where we set the router means after starting the app from where it will start. * In **Content** devs put all the bootstrap required to run bootstrap * In **Controllers** we create controller for our web page * In **fonts** devs put all the fonts. * In **Models** we can create model to create object based on that model. * In **Scripts** devs put all the javascript file which is required. * After creating controller we need to create view based on that controller in **Views** folder.   |

**It follow the MVC structure**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/mvc.png)


# How Asp web app work?

## Controller

**Everytime App will start from controller. First we need to create our controller(name extension: nameController). Inside controller we need to create action which is ultimately a function.**

**To create Controller:**

* Choose Controller folder -> right click -> Add -> Controller -> MVC 5 Controller Empty/other two can be choosed for ur own satisfaction -> Give a name(not ur name) -> Add

**Suppose our controller Name is HomeController.cs**


**HomeController.cs**

       public ActionResult Index()
        {
            return View();
        }
        
**Action will return a View. In views we need to create our own cshtml(html like) webpage. Every Action has their own view. That means When an action being called it will return an web page through view() from Views.**

**We can also sent something to views, to show in webpage by storing in a variable and then call the variable from the web page**

       public ActionResult Index()
        {
            ViewBag.name = "User";
            ViewBag.course = "Asp.Net";
            return View();
        }

**ViewBag.name and course can be used from index.cshtml webpage which is down below**

## Views

**Views->Home(which is a controller name)->index.cshtml**
    
    @{
        ViewBag.Title = "Index";
    }

    <h2>Login</h2>
    <h4>Name @ViewBag.name</h4>
     <h4>Name @ViewBag.course</h4>


    <form method="post">
        <input type="text" class="form-control" name="Uname" placeholder="Username" />
        <input type="password" class="form-control" name="Pass" placeholder="Password" />
        <input type="submit" value="Login" class="btn btn-danger" />
    </form>


**We can create views in short cut way through action:**

**In Action right click on view() function -> Add view -> MVC 5 View -> 
It will generate a box where** 

* View name: we have to give name of this view -> 
* Template: For now don't need to be hyped with Template ->
* Options: In option there is a check box named **Use a layout page** where we can set our own layout page. otherwise it will choose the default one. If we don't want any layout just unchecked the check box.

**Note: To create or see layout there is a folder called Shared which has all the layout. We can also create layout here.** 


## Model

**Model is like a blueprint to create Object. Example: We have a Customer class(Model) which has some field(name,age,password,gender). Then we can create some object which data are being taken through the Registration form. With those data we can create Customer Object. We can create as many object as we want through that form.**

**We create model inside Model folder**

**Example of a Model**

**Customer.cs**

       using System;
       using System.Collections.Generic;
       using System.Linq;
       using System.Web;

       namespace FormSubmission.Models
       {
           public class Customer
           {
               public string Uname { get; set; }
               public string age { get; set; }
               public string gender { get; set; }
               public string Pass { get; set; }
           }
       }




## Some answers:

* View Engine: It helps to run multiple language inside html(example: cshtml file)
* View Engine Razor: It helps to run c# syntax in html (vise versa). **To write c# we have to add an @ sign before c# syntax. Example(@if(){})**
* Layout: Common page for all web page. (example: Navbar)
* To redirect another action : **return RedirectToAction("Index","Home");** "Index": Action name, "Home": Controller name
* To redirect another website link: **return RedirectToAction("https://www.aiub.edu");**
* To create a link: **< a href="/Logged/Home" class="btn btn-primary" >Login</ a >; logged = controller; Home = view name;**


# Form Submission

**Method:**

* Get -> data passed via url.
* Post -> data passed to direct requested body

**Action**

* After submitting form, in which page we want to go; we can set our desired web page.
* We set action page same as form page to show validation message

**We can receive data at backend from < input /> 4 ways:**

* HttpRequestBase class -> **can be used in any web app**
* FormCollection ->**Can only be used in MVC**
* Variable name Mapping -> **can be used in any web app**
* Model Binding -> **can be used in any web app**


## HttpRequestBase class

**Form.html**

       < input name="Uname" />
       < input name="Pass" />

**FormController.cs**

       public ActionResult Index()
        {
            ViewBag.Name = Request["Uname"];
            ViewBag.Password = Request["Pass"];
            return View();
        }
        
## FormCollection object

**Form.html**

       < input name="Uname" />
       < input name="Pass" />

**FormController.cs**

       public ActionResult Index(FormCollection form)
        {
            ViewBag.Name = form["Uname"];
            ViewBag.Password = form["Pass"];
            return View();
        }
        
## Variable Name Maping

**Form.html**

       < input name="Uname" />
       < input name="Pass" />

**FormController.cs**

       public ActionResult Index(String Uname, String Pass)
        {
            ViewBag.Name = Uname;
            ViewBag.Password = Pass;
            return View();
        }

**Will automatically grab Uname and Pass from html form.**

## Model Binding

**Form.html**

       < input name="Uname" />
       < input name="Pass" />

**FormController.cs**

        public ActionResult Index(Login loging)
        {
            return View(loging);
        }

**In model we grab all the data as an array in loging, where Login is a registration model. After passing the loggin through View(). We can use those data in cshtml file the way given below**

       
       <h3>@Model.Uname</h3>
       <h3>@Model.Pass</h3>



# Annotation

**It is a tag which represent a block of code.It must be used in upside of a action method. When we run the method, annotation will run first. If annotation return us true then only the method will run otherwise it won't.**

**Example**

        [HttpGet]
        public ActionResult Index()
        {
            return View();
        }

**If the index view has a from which method is post, then it will give us true. Then Index() method will run.**

# Form Validation

**In Models =>**

     public class Register
       {
        [Required]
        [StringLength(10,ErrorMessage ="Name should not exceed 10 chars")]
        public string Name { get; set; }
        [Required(ErrorMessage ="Please provide id")]
        public string Id { get; set; }
       }

**In Controllers**
        
        public ActionResult Index(Register model) {
            if (ModelState.IsValid) { 
                return RedirectToAction("Index","Home");
            }
            return View(model); 
        }

**To know more: https://learn.microsoft.com/en-us/aspnet/core/mvc/models/validation?view=aspnetcore-7.0**


# Database Connection

**LINQ**

* Provide the feature of query like syntax in c#
* Can be applied to any collection that implements Ienumerable interface(ex. List, Array)
* Can convert to List, array, single instance
* General syntax: From **item** in **collection** where **condition** set item
* syntax better example: **from s in db.Customers
                      where s.id == id
                      select s**

**ORM**

* Object Relational Mapping
* Provides the quality to work with db in OO ways

**Entity Framework**

* ORM for .Net
* DB first -> use on existing project (:
* CODE first -> with code (:
* UML first -> rarely used

## Create connection with ms sql server

**First we have to choose a database to be connected**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Screenshot%20(359).png)

**Suppose we choose ECommerce Database to connect**

**Create a folder/or we can choose Model folder(though it will create a mess like me) - > right click on that foler -> Add -> New item -> Follow the screen shot given below**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Screenshot%20(361).png)

**Add -> EF designer from database -> New connection -> Follow the screen shot given below**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Screenshot%20(360).png)

**Ok -> checked on just Tables -> Finish -> Lastly Ctrl+B (otherwise you will gonna cry).**

**Even after this if you won't understand anything, Then Die. Just kidding. Follow the Link: https://www.youtube.com/watch?v=qSQy1c-XWPg&list=PPSV**

## After Update Database

**After update any table in database, We need to refresh in asp.net connection.**

**To refresh:**

**First we need to go Model1.edmx(name maybe varies, just concerned on edmx extension) file which contain whole design of our database.**
**Next We need click right button then some option will appear (related ss has been given below)**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/UpdateRefresh.png)

**If we added any new table in our database, we just need to checked on "table" => then finish**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/UpdateRefresh3.png)

**If we just update any table in our db we just need to clicked on "table" then => then finish**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/UpdateRefresh2.png)

# CRUD

**To do crud operation we need to create object of Entity framework. To know that Entity framework name to create object, just follow the given below screen shot**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Screenshot%20(362).png)


## Create


**Inside CustomerController.cs**

        [HttpGet]
        public ActionResult Register()
        {
            return View();
        }
        [HttpPost]
        public ActionResult Register(Customer customer)
        {
            var db = new ECommerceEntities1();
            db.Customers.Add(customer);
            db.SaveChanges();

            return RedirectToAction("CutomerList");
        }
        
**First Register action will run and show us the form. After getting submit with post method second register action will run. Second Register will take customer info through form to create a customer object. At first we just create an object of our Entities. Then next line we add our customer object inside database based on Customer table. Note Every time after doing anything with database run db.SaveChanges(). Otherwise it won't reflect on database. Then we just redirect to CustomerList Action which print all the customer list.**

**Register.cshtml**

       
       @{
           ViewBag.Title = "Register";
       }

       <h2>Register</h2>
       <form method="post">
           <input name="id" type="number" placeholder="id" />
           <input name="phone" type="text" placeholder="phone" />
           <input name="name" type="text" placeholder="name" />
           <input name="password" type="text" placeholder="password" />
           <input name="submit" type="submit" value="Register"/>
       </form>

## Read

**Inside CustomerController.cs**

        public ActionResult CutomerList()
        {
            var db = new ECommerceEntities1();
            var customerLi = db.Customers.ToList();
            return View(customerLi);
        }

**We first create an object of database. Then grab all the customer list from database as List. After that we sent that Customer List through view as Model.**

**CustomerList.cshtml**

       @model IEnumerable<Ecommerce.ECM.Customer>
       @{
           ViewBag.Title = "CutomerList";
       }


       <h2>List</h2>

       <table class="table">
           <tr>
               <th>
                   Id
               </th>
               <th>
                   Phone
               </th>
               <th>
                   Name
               </th>
               <th>
                   Password
               </th>
               <th>
                   Edit
               </th>
               <th>
                   Delete
               </th>
           </tr>



           @foreach (var item in Model)
           {
       <tr>
           <td>
               @item.id
           </td>
           <td>
               @item.name
           </td>
           <td>
               @item.phone
           </td>
           <td>
               @item.password
           </td>
           <td>
               <a href="/Customer/Edit/@item.id">Edit</a>
           </td>
           <td>
               <a href="/Customer/Delete/@item.id">Delete</a>
           </td>
       </tr>
           }


       </table>

**@model IEnumerable<Ecommerce.ECM.Customer> this line is for to collect all the data from CustomerList view which is sent through "return View(customerLi);". So why we are doing it because we may pass any types of Model we want but in this time we only want Customer model. Except Customer others model won't gonna be accepted**

* Ecommerce = Project name
* ECM = folder name where we created connection with db
* Customer = Class name

## Update

**Inside CustomerController.cs**

        [HttpGet]
        public ActionResult Edit(int id)
        {
            var db = new ECommerceEntities1();
            var st = (from s in db.Customers
                      where s.id == id
                      select s).SingleOrDefault();
            return View(st);
        }
        [HttpPost]
        public ActionResult Edit(Customer upstudent)
        {
            var db = new ECommerceEntities1();
            var exst = (from s in db.Customers
                        where s.id == upstudent.id
                        select s).SingleOrDefault();
            exst.phone = upstudent.phone;
            exst.name = upstudent.name;
            exst.password = upstudent.password;

            //db.Entry(exst).CurrentValues.SetValues(upstudent);
            db.SaveChanges();

            return RedirectToAction("CutomerList");
        }
        
        //Alternative to find from database
        db.Customers.Find(id);
        
        
**Work like "create", in first Edit action it will take a user id which sent by us. How we sent?**

**< a href="/Customer/Edit/@item.id" >Edit</ a > .**

**Next it will create a query to search that user from our database. SingleOrDefault() function used which will sent a user object because we won't get any list we will get one object only because id is unique. After that we just sent that object info to Edit view so that we can see it from front end.**

**After submitting with edited info second Edit action will run. This time we took all the info as "upstudent" which is sent through form. Next we just update all the info manually, we can do it easily by run this "db.Entry(exst).CurrentValues.SetValues(upstudent);"**

**Edit.cshtml**

       @{
           ViewBag.Title = "Edit";
       }

       <h2>Edit</h2>
       <form method="post">
           <input name="name" type="text" value="@Model.name" placeholder="name" />
           <input name="phone" type="text" value="@Model.phone" placeholder="phone" />
           <input name="password" type="text" value="@Model.password" placeholder="password" />
           <input name="submit" type="submit" value="Register" />
       </form>



## Delete

**Inside CustomerController.cs**

       public ActionResult Delete(int id)
        {
            var db = new ECommerceEntities1();
            var exst = (from s in db.Customers
                        where s.id == id
                        select s).SingleOrDefault();
            db.Customers.Remove(exst);
            db.SaveChanges();

            return RedirectToAction("CutomerList");
        }
        
**This time delete action will just take an id which was sent by us.**
**How did we sent?**
**< a href="/Customer/Delete/@item.id">Delete</ a >**

**Then it will search that object by using that id. After that it will remove that customer object from database.**

**There is no Delete views because we just deleting the customer object, we are not showing the customer anything. Though we can show the customer a pop up like "Do you really want to delete?"**




# Database Design

**First We need to designing a database with their corresponding relationship**
![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Database.jpg)

**Then, we have to create table with index column**
![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Design%20Database.png)

**After that we need to implement those design in our database server**
![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Catagory%20.png)
![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Customer.png)

**Order table is connected with Customer table with Many(Order) To One(Customer) relationship. We choose to set a foreign key in Order table of Customer table. Because Order table is Many and Customer is One. We have to remember one thing that is when we see a Many to One or One to Many, we will just go to Many table then create a foreign key of One table. Whole Process is given below how to do this.**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Order-1.png)

**Need to click "Add" to add**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Order-2.png)
![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Order-3.png)
![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Order-4.png)

**Create Just a Product table**
![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Product-1.png)

**Product and Order table are connected with Many to Many Relationship. But we won't gonna able to create Many to Many relationship in sql. So, to solve this issue we need to create a middle table which will gonna connected with both Product and Order table. For this example, we named this middle table is ProductOrder. We will set ProductOrder as Many and other both table(Product and Order) will be set as One position. So our relation would be like this:**

       Product(One) -- ProductOrder(Many) -- Order(One)
       
**Now we know how to create One to Many relationship in database**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/ProductOrder-2.png)
![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/ProductOrder-1.png)




# Code First approach

**(first we will code, based on that code we will create database).**

**First need to download entity framework by going our project then click right button on whole project file name**
* **click manage nugget packages**
* **search "Entityframework"** 
* **download it**

**Before, we just used ADO connection string , but this time we will create our own connection string. which is need to be done only for 1 time.**

* **In our peoject folder there is a file called Web.config, in this file scroll down in the below we will find </ configuration > which means the ending of configuration.** 
* **We will create our string before the ending of this </ configuration >**
* **create a tag connection string < connectionStrings > </ connectionStrings >** 
* **Inside it create another tag called add, on that add we will do our work like given below**

**< connectionStrings > 
< add name="PMSContext" connectionString="data source=FRAGILE; initial catalog=ECommerce; integrated security=true;" providerName="System.Data.Sqlclient"/>
</ connectionStrings >**

* **name="" can be anything.** 
* **data source= server name(my server name is fragile)**
* **initial catalog= Database name which I will use in this project,if there is no database as ECommerce it will create it's own.**
* **integrated security= To active windows authentication.**
* **If you have to use ur database by logged in,,,User Id="";Password=""; instead of connectionString="data source=FRAGILE;**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/CodeFirst1.png)


## Model and context modification:(context means database)

**Design:**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Design.png)

**Based on that design we will create our database**

**Step:**

* **Create a folder called EF under our project**
* **inside EF create another folder called Models**
* **inside Models we will create table's model which we want to be created in our database**
* **inside Models or inside EF foleder(preferable) we have to create a cs file which name is based on context name.(name="PMSContext", from < connectionStrings />). So, we will create a cs file called PMSContext.cs. this PMSContext class will inherit DbContext.**

**PMSContext.cs**

	using System;
	using System.Collections.Generic;
	using System.Data.Entity;
	using System.Linq;
	using System.Web;

	namespace EFCodeFirst.EF.Models
	{
	    public class PMSContext : DbContext
	    {
		public DbSet<Category> Categories { get; set; }
		public DbSet<Product> Products { get; set; }
		public DbSet<Order> Orders { get; set; }
		public DbSet<OrderDetail> OrderDetails { get; set; }
		public DbSet<User> Users { get; set; }
	    }
	}
	
	
**Category.cs**

	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Web;

	namespace EFCodeFirst.EF.Models
	{
	    public class Category
	    {
		public int Id { get; set; }
		public string Name { get; set; }
		public virtual ICollection<Product>Products { get; set; }
		public Category() {
		    Products = new List<Product>();
		}

	    }
	}


**Order.cs**

	using System;
	using System.Collections.Generic;
	using System.ComponentModel.DataAnnotations.Schema;
	using System.Linq;
	using System.Web;

	namespace EFCodeFirst.EF.Models
	{
	    public class Order
	    {
		public int Id { get; set; }
		public DateTime OrderDate { get; set; }
		public string Status { get; set; }
		public int Amount { get; set; }
		[ForeignKey("OrderedBy")]
		public string OrderedById { get; set; }
		public virtual User OrderedBy { get; set; }
		public virtual ICollection<OrderDetail> OrderDetails { get; set; }
		public Order() {
		    OrderDetails = new List<OrderDetail>();
		}
	    }
	}

**OrderDetail.cs**

	using System;
	using System.Collections.Generic;
	using System.ComponentModel.DataAnnotations.Schema;
	using System.Linq;
	using System.Web;

	namespace EFCodeFirst.EF.Models
	{
	    public class OrderDetail
	    {
		public int Id { get; set; }
		public int Qty { get; set; }
		public int Price { get; set; }
		[ForeignKey("Product")]
		public int PId { get; set; }
		[ForeignKey("Order")]
		public int OId { get; set; }
		public virtual Product Product{ get; set; }
		public virtual Order Order { get; set; }
	    }
	}


**Product.cs**

	using System;
	using System.Collections.Generic;
	using System.ComponentModel.DataAnnotations;
	using System.ComponentModel.DataAnnotations.Schema;
	using System.Linq;
	using System.Web;

	namespace EFCodeFirst.EF.Models
	{
	    public class Product
	    {
		[Key]
		public int Id { get; set; }
		[Required]
		[StringLength(100)]
		public string Name { get; set; }
		public int? Price { get; set; }//to make nullable used int?
		public int Qty { get; set; }
		[ForeignKey("Category")]
		public int CId { get; set; }
		public virtual Category Category { get; set; }
		public virtual ICollection<OrderDetail> OrderDetails { get; set; }
		public Product()
		{
		    OrderDetails = new List<OrderDetail>();
		}
	    }
	}

**User.cs**

	using System;
	using System.Collections.Generic;
	using System.ComponentModel.DataAnnotations;
	using System.Linq;
	using System.Web;

	namespace EFCodeFirst.EF.Models
	{
	    public class User
	    {
		[Key]
		[StringLength(10)]
		public string Username { get; set; }
		[Required]
		[StringLength (100)]
		public string Name { get; set; }
		[Required,StringLength (10)]
		public string Type { get; set; }
		[Required]
		public string Password { get; set; }
		public virtual ICollection<Order> Orders { get; set; }
		public User() {
		    Orders = new List<Order>();
		}

	    }
	}


***Inside PMSContext class we create a DbSet which will create a table on our database . In here, inside Models we created a some model. To create table on those model on our database, we created DbSet of all Model inside PMSContext class. To reflect this code on databse, we need to do migration. Migration will convert this c# code into sql query and run those query in database. This way, we can create table based on our model in our database***

**To enable migration we have to use command line => tools => Nuget package manager => package manager console => Write on: PM> here**
	
![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/CodeFirst3.png)
	
* **to enable=> enable-migrations**
* **If we changed or modify any model or context we need to run => add-migration msg** 
	* **msg is like a github a commit message**
* **to update database=> update-database -Verbose**
	* **if we use -Verbose it will show us query, otherwise it will hide all those query**


**After run everything in our microsoft sql server a database named School will be created. On that database a Category table will be created, and other models table will also be created, beside that table another table named "dbo._MigrationHistory" will be created which is created by default to track all table creation, modification etc.**

**In model if we create a variable called id and type int, database will make this id as primary key, and auto increment. It is a default behaviour. otherwise we can set as [Key].**


**In model if there is a relation of one to one, one to many, vise versa, we may required to create a collection of other table/model, If we create collection then we need to create a constructor where we required to create an object of that collection table/model.**

**We can create random data on our database by writing code inside Seed() which is in Configuration.cs file, which is in Migrations Folder.**
**This Seed() method will run only one time, when we first run the project**

**Configuration.cs**

	namespace EFCodeFirst.Migrations
	{
	    using System;
	    using System.Data.Entity;
	    using System.Data.Entity.Migrations;
	    using System.Linq;

	    internal sealed class Configuration : DbMigrationsConfiguration<EFCodeFirst.EF.Models.PMSContext>
	    {
		public Configuration()
		{
		    AutomaticMigrationsEnabled = false;
		}

		protected override void Seed(EFCodeFirst.EF.Models.PMSContext context)
		{
		    //  This method will be called after migrating to the latest version.

		    //  You can use the DbSet<T>.AddOrUpdate() helper extension method
		    //  to avoid creating duplicate seed data.


		    for(int i = 0; i < 10; i++)
		    {
			context.Categories.AddOrUpdate(
			    new EF.Models.Category() { 
				Name=Guid.NewGuid().ToString().Substring(0,5), //6 string from 36 string
			    }
			    );
		    }
		    Random random = new Random();
		    for (int i = 0; i < 1000; i++) {
			context.Products.AddOrUpdate(

				new EF.Models.Product() { 
				    Name = Guid.NewGuid().ToString().Substring(0,17),
				    Price = random.Next(100,501),
				    Qty = random.Next(10,51),
				    CId = random.Next(1,21)
				}
			    );
		    }
		}
	    }
	}


**In here 10 category data will be created on our database. Next, 1000 Product will be created. If there is already created those data it won't gonna create again**



# Authentication

**Login Action**


	[HttpGet]
        public ActionResult Login() { 
            return View();  
        }
        [HttpPost]
        public ActionResult Login(LoginModel login) {
            if (ModelState.IsValid) {
                PMSContext db = new PMSContext();
                var user = (from u in db.Users
                            where u.Username.Equals(login.Username)
                            && u.Password.Equals(login.Password)
                            select u).SingleOrDefault();
                if (user != null)
                {
                    Session["user"] = user;
                    //var returnUrl = Request["ReturnUrl"];
                    //if(returnUrl != null)
                    //{
                      //  return Redirect(returnUrl);
                    //}
                    return RedirectToAction("Index", "Order");
                }
                TempData["Msg"] = "Username Password Invalid";
            }
            return View(login);
            
        }

**Login.cshtml**
       
       @{
           ViewBag.Title = "Login";
       }

       <h2>Log In</h2>
       <form method="post">
           <input name="name" type="text" placeholder="name" />
           <input name="password" type="text" placeholder="password" />
           <input name="submit" type="submit" value="Login"/>
       </form>


## Annotation

**We can create our own annotation maybe for authentication purpose**

**To create authentication annotation:**

**Inside our project we need to create a folder, for better known we may named that folder Auth.**
**For now we want to create two authentication annotation, one for Admin, another for Logged in user.**
**Inside Auth folder we created two file, first one is AdminAccess.cs, another one is Logged.cs**

**Project => Auth => AdminAccess.cs, Logged.cs**

**N:B: Folder name, file name could be anything**

**AdminAccess.cs**

	using EFCodeFirst.EF.Models;
	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Web;
	using System.Web.Mvc;

	namespace EFCodeFirst.Auth
	{
	    public class AdminAccess:AuthorizeAttribute
	    {
		protected override bool AuthorizeCore(HttpContextBase httpContext)
		{
		    var user = (User)httpContext.Session["user"];
		    if(user != null && user.Type.Equals("admin")) return true;
		    return false;
		}
	    }
	}


**Logged.cs**

	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Web;
	using System.Web.Mvc;

	namespace EFCodeFirst.Auth
	{
	    public class Logged : AuthorizeAttribute
	    {
		protected override bool AuthorizeCore(HttpContextBase httpContext)
		{
		    if (httpContext.Session["user"] != null) return true;
		    return false;
		}
	    }
	}

**To use these Annotation we can call them before any our controller Action**

**example**

	[AdminAccess]
        public ActionResult AllOrders() {
            var db = new PMSContext();
            return View(db.Orders.ToList());
        }

**Ony Admin can see the order list**





# API

**Application Programming Interface: Api is like a waiter where Customer is assuming Front End and Cheif is assuming Backend.**

**For creating API we need to do something extra stuff**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/1.png)

**Next**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/APi1.png)

**After starting the project, we can create database through Code First or Database First, any way we want.**

**Then we need to create controller:**

	Choose Controller folder -> right click -> Add -> Controller

**Next follow the screen shot given below:**


![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/APi2.png)


## Inside Controller File:

**First, Let's try to understand the Main thing**

	[HttpGet]
        [Route("api/students")]
        public HttpResponseMessage AllStudents()
        {
            EFSContext db = new EFSContext();
            var data = db.Students.ToList();
            return Request.CreateResponse(HttpStatusCode.OK, data);
        }
	
**Here in this code we created a Response Message,**

**[HttpGet] = Response when request is Get**

**[Route("api/students")] = After run the project we need to add this "api/students" url on that running url.(Example:https://localhost:44346/api/students)**

**After getting a request AllStudent() will return a response which contains data and a status code.**

## To get all the data from database:

	[HttpGet]
        [Route("api/students")]
        public HttpResponseMessage AllStudents()
        {
            EFSContext db = new EFSContext();
            var data = db.Students.ToList();
            return Request.CreateResponse(HttpStatusCode.OK, data);
        }

## To get individual data from database:

	[HttpGet]
        [Route("api/students/{id}")]
        public HttpResponseMessage GetStudents(int id)
        {
            EFSContext db = new EFSContext();
            var student = db.Students.Find(id);
            if (student != null)
            {
                return Request.CreateResponse(HttpStatusCode.OK, student);
            }
            return Request.CreateResponse(HttpStatusCode.NotFound);

        }

## To create data in database:

	[HttpPost]
        [Route("api/students/add")]
        public HttpResponseMessage AddStudents(Student st)
        {
            try
            {
                EFSContext db = new EFSContext();
                db.Students.Add(st);
                db.SaveChanges();
                return Request.CreateResponse(HttpStatusCode.OK);
            }
            catch(Exception ex)
            {
                return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ex.Message);
            }
        }

## To update data in database:

	[HttpPost]
        [Route("api/students/update")]
        public HttpResponseMessage UpdateStudents(Student st)
        {
            EFSContext db = new EFSContext();
            var student = db.Students.Find(st.Id);
            if (student != null)
            {
                db.Entry(student).CurrentValues.SetValues(st);
                try
                {
                    db.SaveChanges();
                    return Request.CreateResponse(HttpStatusCode.OK, student);
                }
                catch(Exception ex)
                {
                    return Request.CreateErrorResponse(HttpStatusCode.BadRequest,ex.Message);
                }
               
            }
            return Request.CreateResponse(HttpStatusCode.NotFound,"User Not Found");

        }

## To delete data from database

	[HttpDelete]
        [Route("api/studentdelete/{id}")]
        public HttpResponseMessage DeleteStudents(int id)
        {
            EFSContext db = new EFSContext();
            var student = db.Students.Find(id);
            if (student != null)
            {
                db.Students.Remove(student);
                db.SaveChanges();
                return Request.CreateResponse(HttpStatusCode.OK);
            }
            return Request.CreateResponse(HttpStatusCode.NotFound);

        }


## PostMan API

**To interact with database through api request: Need to install PostMan Api software**

**After Installation:**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/ApiSee1.png)

**Data creation is a little bit tricky**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/ApiSee2.png)






# N-tier Architecture as 3-tier Architecture:

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-1.png)

**N:B: When we create any model class, we make sure it is public just for now. Later we will make it internal**

**Application Layer:**
**In this layer user interact with the app. Application layer can be connected to anything. Example: Desktop app, android app.**

**Business Logic Layer:**
**In this layer decision making or logical operation are being implemented. Example: More than 20 students can't take Biology.**

**Data Access Layer:**
**In this layer we access data from database.**

## Step:

**Till now we created application Layer. Application layer can be connected with mobile app, etc. It could be anything.**

**So now we have to create DAL and BLL**
**To do these just follow the screenshot given below:**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-2.png)
![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-3.png)
![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-4.png)

**Same way we will create DAL**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-5.png)

**We peacefully created 3 layer**

**Now we have to connect Application Layer to Business Logic Layer , then Business Logic Layer to Data Access Layer. Connection process is Top Down approach**

**How? just Follow the ss given below**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-6.png)
![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-8.png)

**Now Application Layer and Business Logic Layer or BLL connected with each other**

**Next same way from BLL connect BLL with DAL**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-9.png)

**Now we have to install EntityFramework in DAL and Application Layer. In DAL we will create A folder Call Model. In this folder We will create table as a class like the older way.
And also don't forget to create a Context class inside DAL.
After this we need to create a < connectionStrings /> inside web.config which is in Application Layer.
That means database creation depends on both DAL and application Layer.**

**To run command we have to open package manager console same the older way.**

**But this time we have to change one thing which is given below:**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-10.png)

**In here we will run those command(enable-migrations, add-migraration etc) Like the older way.**

## DAL

**Next we have to create a folder called Interfaces. Inside Interfaces we have to create IRepo.cs. (What is Repo? Repo: Repo is a folder which contains the model class file, These file will comunicate with databases.)**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-13.png)

**IRepo.cs**

	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Text;
	using System.Threading.Tasks;

	namespace DAL.Interfaces
	{
	    public interface IRepo<TYPE,ID,RET>
	    {
		List<TYPE> Get();
		TYPE Get(ID id);
		RET Insert(TYPE obj);
		RET Update(TYPE obj);
		bool Delete(ID id);
	    }
	}

**IRepo.cs is an interface which contains the main structure of all of the repos**
**All the repos will inherit this IRepo if there function matched with IRepo. Otherwise for different repo with different function, we have to create different interfaces.**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-14.png)

**Next we have to create our desire Repo class inside a Repo folder. Repo class is created to interact our Model class with database.**
**To not create multiple time object of a database, we can create a class called Repo which contains the the creation of object of database, then all other repo will inherit this Repo class. So then we won't need to create object of database in every repo class.**

**Procedure is given below:**

**Repo.cs**

	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Text;
	using System.Threading.Tasks;

	namespace DAL.Repos
	{
	    internal class Repo
	    {
		internal LABContext db;
		internal Repo()
		{
		    db = new LABContext();
		}
	    }
	}


**MemberRepo.cs:**

	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Text;
	using System.Threading.Tasks;
	using DAL.Interfaces;
	using DAL.Models;

	namespace DAL.Repos
	{
	    internal class MemberRepo : Repo, IRepo<Member, int, bool>
	    {
		public bool Delete(int id)
		{
		    var data = db.Members.Find(id);
		    db.Members.Remove(data);
		    return db.SaveChanges() > 0;
		}

		public List<Member> Get()
		{
		    return db.Members.ToList();
		}

		public Member Get(int id)
		{
		    return db.Members.Find(id);
		}

		public bool Insert(Member obj)
		{
		    db.Members.Add(obj);
		    return db.SaveChanges() > 0;
		}

		public bool Update(Member obj)
		{
		    var data = db.Members.Find(obj.Id);
		    db.Entry(data).CurrentValues.SetValues(obj);
		    return db.SaveChanges()>0;
		}

	    }
	}



**In the same we can create as many repo as we want.**

**Next we have to create a DataAccessFactory class inside DAL(Not any other folder). So that BLL can communicate with DAL through this DataAccessFactory.cs**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-15.png)

**DataAccessFactory.cs**

	using DAL.Interfaces;
	using DAL.Models;
	using DAL.Repos;
	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Text;
	using System.Threading.Tasks;

	namespace DAL
	{
	    public class DataAccessFactory
	    {
		public static IRepo<Member, int, bool> MemberData()
		{
		    return new MemberRepo();
		}
		public static IRepo<Project, int, bool> ProjectData()
		{
		    return new ProjectRepo();
		}
	    }
	}




**In DAL our work has been done. Next we have to work on BLL.**

## BLL:

**Inside BLL we have to create 2 folder which are called:**

* 1. Services
* 2. DTOs

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-16.png)

**DTOs are as same as Model class. DTOs class are being created inside DTOs folder.**

**Inside DTOs CommentDTOs.cs**

	using DAL.Models;
	using System;
	using System.Collections.Generic;
	using System.ComponentModel.DataAnnotations;
	using System.ComponentModel.DataAnnotations.Schema;
	using System.Linq;
	using System.Text;
	using System.Threading.Tasks;

	namespace BLL.DTOs
	{
	    public class CommentDTO
	    {
		[Key]
		public int Id { get; set; }
		[Required]
		public string Text { get; set; }
		[Required]
		public DateTime Date { get; set; }

		public int UserId { get; set; }

		public int PostId { get; set; }


	    }
	}



**When we call a method from DAL our BLL couldn't able to recognise that method return type, which is a class. To solve this problem we create DTO's. When we call a method from DAL we got an object which can't be recognized by BLL. So we just convert that object into DTOs class(before we say that DTOs and Model class are same and DTOs are belongs to BLL and Model class are belongs to DAL). If we required to send a data to DAL we just convert that DTOs class object into Model class object.**

**To convert DTOs to model or model to DTOs there is a package called Automapper. We can download this Automapper(version: 10.0.0) package by the help of Nuget Manager. We have to download Automapper in BLL.**

**Services:**

**Insert data, get data etc are being done through Services. Services are like bridge between DAL and BLL.**


**Inside Services CommentServices.cs**


	using AutoMapper;
	using BLL.DTOs;
	using DAL;
	using DAL.Models;
	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Text;
	using System.Threading.Tasks;

	namespace BLL.Services
	{
	    public class CommentServices
	    {
		public static List<CommentDTO> Get()
		{
		    var data = DataAccessFactory.CommentData().Get();
		    var cfg = new MapperConfiguration(c=>
		    {
			c.CreateMap<Comment, CommentDTO>();
		    });
		    var mapper = new Mapper(cfg);
		    var mapped = mapper.Map<List<CommentDTO>>(data);

		    return mapped;
		    /*return Convert(data);*/
		}

		public static CommentDTO Get(int id)
		{
		    var data = DataAccessFactory.CommentData().Get(id);

		    var cfg = new MapperConfiguration(c =>
		    {
			c.CreateMap<Comment, CommentDTO>();
		    });
		    var mapper = new Mapper(cfg);
		    var mapped = mapper.Map<CommentDTO>(data);

		    return mapped; 


		}

		public static bool Create(CommentDTO member)
		{
		    var cfg = new MapperConfiguration(c =>
		    {
			c.CreateMap<CommentDTO, Comment>();
		    });
		    var mapper = new Mapper(cfg);
		    var mapped = mapper.Map<Comment>(member);

		    /*var data = Convert(member);*/
		    return DataAccessFactory.CommentData().Insert(mapped);
		}

		public static bool Update(CommentDTO member)
		{
		    var cfg = new MapperConfiguration(c =>
		    {
			c.CreateMap<CommentDTO, Comment>();
		    });
		    var mapper = new Mapper(cfg);
		    var mapped = mapper.Map<Comment>(member);
		    /*var data = Convert(member);*/
		    return DataAccessFactory.CommentData().Update(mapped);
		}

		public static bool Delete(int id)
		{
		    return DataAccessFactory.CommentData().Delete(id);
		}


	       /* static List<CommentDTO> Convert(List<Comment> comment)
		{
		    var data = new List<CommentDTO>();
		    foreach (var cm in comment)
		    {
			data.Add(new CommentDTO()
			{
			    Id = cm.Id,
			    Text = cm.Text,
			    Date = cm.Date,
			    UserId = (int)cm.UserId,
			    *//*Student=cm.Student,*/
			    /*TeacherId= (int)cm.TeacherId,*/
			    /* Teacher=cm.Teacher,*//*
			    PostId = (int)cm.PostId,
			    *//*Post=cm.Post*//*

			});
		    }

		    return data;
		}

		static CommentDTO Convert(Comment cm)
		{
		    return new CommentDTO()
		    {
			Id = cm.Id,
			Text = cm.Text,
			Date = cm.Date,
			UserId = (int)cm.UserId,
			*//*Student = cm.Student,*/
		       /* TeacherId = (int)cm.TeacherId,*/
		       /* Teacher = cm.Teacher,*//*
			PostId = (int)cm.PostId,
			*//*Post = cm.Post*//*
		    };
		}

		static Comment Convert(CommentDTO cm)
		{
		    return new Comment()
		    {
			Id = cm.Id,
			Text = cm.Text,
			Date = cm.Date,
			UserId = cm.UserId,
			*//*Student = cm.Student,*/
			/*TeacherId = cm.TeacherId,*/
			/*Teacher = cm.Teacher,*//*
			PostId = cm.PostId,
			*//*Post = cm.Post*//*
		    };
		}*/


	    }
	}





## Application Layer:

**We are assuming this layer as API.
Inside Controller we create CommentController as Controller.**

**CommentController.cs**

	using BLL.DTOs;
	using BLL.Services;
	using OnlineAcademy.Auth;
	using System;
	using System.Collections.Generic;
	using System.Linq;
	using System.Net;
	using System.Net.Http;
	using System.Web.Http;
	using System.Web.Http.Cors;

	namespace OnlineAcademy.Controllers
	{
	    [EnableCors("*","*","*")]  /* just enabling CORS */ 
	    [Logged]
	    public class CommentController : ApiController
	    {

		[HttpGet]
		[Route("api/comments")]
		public HttpResponseMessage Get()
		{
		    try
		    {
			var data = CommentServices.Get();
			return Request.CreateResponse(HttpStatusCode.OK, data);
		    }
		    catch (Exception ex)
		    {

			return Request.CreateResponse(HttpStatusCode.BadRequest, ex.Message);

		    }
		}

		[HttpGet]
		[Route("api/comments/{id:int}")]
		public HttpResponseMessage GetM(int id)
		{
		    try
		    {
			var data = CommentServices.Get(id);
			return Request.CreateResponse(HttpStatusCode.OK, data);
		    }
		    catch (Exception ex)
		    {

			return Request.CreateResponse(HttpStatusCode.BadRequest, ex.Message);

		    }
		}


		[HttpPost]
		[Route("api/comments/add")]
		public HttpResponseMessage AddMembers(CommentDTO comment)
		{
		    try
		    {
			var res = CommentServices.Create(comment);
			return Request.CreateResponse(HttpStatusCode.OK, res);
		    }
		    catch (Exception ex)
		    {
			Console.WriteLine(ex.InnerException.Message);
			return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ex.InnerException.InnerException.Message);

		    }
		}


		[HttpPost]
		[Route("api/comments/update")]
		public HttpResponseMessage UpdateMembers(CommentDTO comment)
		{
		    try
		    {
			var res = CommentServices.Update(comment);
			return Request.CreateResponse(HttpStatusCode.OK, res);
		    }
		    catch (Exception ex)
		    {
			return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ex.InnerException.InnerException.Message);
		    }
		}


		[HttpDelete]
		[Route("api/comments/delete/{id:int}")]
		public HttpResponseMessage DeleteMembers(int id)
		{
		    try
		    {
			var res = CommentServices.Delete(id);
			return Request.CreateResponse(HttpStatusCode.OK, res);
		    }
		    catch (Exception ex)
		    {
			return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ex.Message);
		    }

		}
	    }
	}

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/Layer-17.png)

**With this controller we communicate with BLL. Application layer dunno anything about DAL it's only know about BLL. BLL know DAL, and it catches data from DAL**

**We can set some authentication. Example: only logged in user can use this api or only admin can use this api etc.**

**Now simply run these on Postman Api or any way you want**


# SOLID architechture

<h4><a href="https://www.digitalocean.com/community/conceptual-articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design">Visit this link to know everything about SOLID architechture</a></h4>











 






