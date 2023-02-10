# Asp.Net-Note

**Asp.Net is a tool to create website which is design based on MVC(Model View Controller)**

# To Start

**To create website with asp.net we need to choose the option on picture given below.**

![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/1.png)

# Structure of Asp.Net
|  Image      | Description |
| ----------- | ----------- |
| ![](https://github.com/Ridowan-sajid/Asp.Net-Note/blob/main/images/2.png) | * In **App Start** We have **RouterConfig.cs** where we set the router means after starting the app from where it will start. * In **Content** devs put all the bootstrap required to run bootstrap * In **Controllers** we create controller for our web page * In **fonts** devs put all the fonts. * In **Models** we can create model to create object based on that model. * In **Scripts** devs put all the javascript file which is required. * After creating controller we need to create view based on that controller in **Views** folder.   |

# How Asp web app work?

**Everytime App will start from controller. First we need to create our controller(name extension: nameController). Inside controller we need to create action which is ultimately a function.**
**Suppose our controller Name is HomeController.cs**

## Action

**HomeController.cs**

       public ActionResult Index()
        {
            return View();
        }
        
**Action will return a View. In views we need to create our own cshtml(html like) webpage. Every Action has their own view. That means When an action being called it will return an web page through view() from Views.**

## Views

**Views->Home(which is a controller name)->index.cshtml**
    
    @{
        ViewBag.Title = "Index";
    }

    <h2>Login</h2>

    <form method="post">
        <input type="text" class="form-control" name="Uname" placeholder="Username" />
        <input type="password" class="form-control" name="Pass" placeholder="Password" />
        <input type="submit" value="Login" class="btn btn-danger" />
    </form>


**We can create views in short cut way through action:**

**In Action right click on view() function -> Add view -> MVC 5 View -> 
It will generate a box where** 

* View name: we have to give name of this view -> 
* Template: For now don't need to hyped with Template ->
* Options: In option there is a check box named **Use a layout page** where we can set our own layout page. otherwise it will choose the default one. If we don't want any layout just unchecked the check box.

**Note: To create or see layout there is a folder called Shared which has all the layout. We can also create layout here.** 

**Some answers:**

* View Engine: It helps to run multiple language inside html(example: cshtml file)
* View Engine Razor: It helps to run c# syntax in html (vise versa). **To write c# we have to add an @ sign before c# syntax. Example(@if(){})**
* Layout: Common page for all web page. (example: Navbar)
* To redirect from one : **return RedirectToAction("Index","Home");** "Index": Action name, "Home": Controller name







