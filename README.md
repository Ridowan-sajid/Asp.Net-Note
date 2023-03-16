# Asp.Net-Note

**Asp.Net is a tool to create website which is design based on MVC(Model View Controller)**

# To Start

**To create website with asp.net we need to choose the option on picture given below.**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/1.png)

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








