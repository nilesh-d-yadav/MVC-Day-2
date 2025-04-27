# MVC-Day-2

# ASP.NET MVC Razor Views: Theory & Code Examples

## 1. Razor View Engine in ASP.NET MVC

| **Feature**     | **Description**                                                             |
|-----------------|-----------------------------------------------------------------------------|
| **Razor View Engine** | To render dynamic HTML pages by mixing C# and HTML easily.            |
| **Purpose**     | To allow seamless mixing of C# code with HTML to generate dynamic content.  |
| **Syntax**      | Starts with `@`, which is used to transition between HTML and C# code.     |
| **Performance** | Fast rendering with minimal overhead.                                        |
| **File Type**   | `.cshtml`                                                                   |


The **Razor View Engine** is a markup syntax used for defining views in ASP.NET MVC. It combines HTML with C# code, allowing developers to dynamically generate web pages based on the data in the model.
Razor View Engine lets you embed C# logic into your HTML pages cleanly and efficiently in ASP.NET MVC.

### Syntax:
- `@` is used to switch from HTML to C#.
- C# code such as loops, conditions, and functions can be embedded using `@{ }`.
- Razor can handle **conditional statements**, **loops**, and **data binding** to display dynamic content.

---

## 2. Razor Syntax Example
### Wriitiung C# In HTML
```
<h1>Welcome to My Website</h1>
<p>Today's date is: @DateTime.Now.ToLongDateString()</p>
```
### If-Else in Razor
```
@{
    var isLoggedIn = true;
}

@if (isLoggedIn)
{
    <p>Hello, User!</p>
}
else
{
    <p>Please log in.</p>
}

```

### Loops in Razor
```
<ul>
@for (int i = 1; i <= 5; i++)
{
    <li>Item @i</li>
}
</ul>

```


### Displaying Dynamic Data:

```html
@{
    var name = "John Doe";
}
<p>Hello, @name!</p>

# 📄 ViewBag and ViewData in ASP.NET MVC 5

This mini project demonstrates how to use **ViewBag** and **ViewData** to pass data from a Controller to a View in an ASP.NET MVC 5 application.

## 🛠️ How it Works

### 🔹 Controller Code

```csharp
using System.Web.Mvc;

namespace ViewBagViewDataDemo.Controllers
{
    public class HomeController : Controller
    {
        [HttpGet]
        public ActionResult Index()
        {
            // Setting data using ViewBag
            ViewBag.Greeting = "Hello from ViewBag!";

            // Setting data using ViewData
            ViewData["Note"] = "This is a message from ViewData.";

            return View();
        }
    }
}
```
### Standard HTML Helpers
```
@using (Html.BeginForm())
{
    <div>
        @Html.Label("Name")
        <br />
        @Html.TextBox("Name")
    </div>

    <div>
        @Html.Label("Email")
        <br />
        @Html.TextBox("Email")
    </div>

    <div>
        @Html.Label("Password")
        <br />
        @Html.Password("Password")
    </div>

    <div>
        @Html.CheckBox("AgreeToTerms")
        @Html.Label("AgreeToTerms", "I agree to the terms and conditions")
    </div>

    <div>
        <input type="submit" value="Register"/>
    </div>
}


```

# Standard HTML Forms

## 📄 UserModel.cs

This file defines a **UserModel** class used for capturing user registration details with built-in validations using **Data Annotations** in ASP.NET MVC 5.

---



## 🛠️ Code

```csharp
using System.ComponentModel.DataAnnotations;

namespace _27April.Models
{
    public class UserModel
    {
        [Required(ErrorMessage = "Name Is required")]
        public string Name { get; set; }

        [Required(ErrorMessage = "Email Is required")]
        [EmailAddress(ErrorMessage = "Invalid Email Format")]
        public string Email { get; set; }

        [Required(ErrorMessage = "Password Is required")]
        [StringLength(100, MinimumLength = 6, ErrorMessage = "Password must have atleast 6 characters")]
        public string Password { get; set; }

        [Required(ErrorMessage = "You must agree to the terms")]
        public bool AgreeToTerms { get; set; }
    }
}
```
## 📄 UserController.cs

## 🛠️ Code

```csharp
using _27April.Models;
using Microsoft.AspNetCore.Mvc;

namespace _27April.Controllers
{
    public class UserController : Controller
    {
        // GET: Render Registration Form
        public IActionResult Register()
        {
            return View();
        }

        // POST: Handle Registration Form Submission
        [HttpPost]
        public IActionResult Register(UserModel user)  
        {
            if (ModelState.IsValid)
            {
                ViewBag.Message = "Registration Successful";
                return View("RegistrationDetails", user);
            }

            return View(user);
        }
    }
}
```
## 📄 Register.cshtml

It uses **Standard HTML Helpers** (`@Html.Label`, `@Html.TextBox`, `@Html.Password`, etc.) along with **Validation Messages** for server-side validation feedback.

## 🛠️ Code

```csharp
@*
    For more information on enabling MVC for empty projects, visit https://go.microsoft.com/fwlink/?LinkID=397860
*@
@{
    ViewBag.title = "User Registration";
}
<p>This is Registration Form!</p>

@using (Html.BeginForm())
{
    <div>
        @Html.Label("Name")
        <br />
        @Html.TextBox("Name")
        @Html.ValidationMessage("Name", "", new { @class = "text-danger" })
    </div>

    <div>
        @Html.Label("Email")
        <br />
        @Html.TextBox("Email")
        @Html.ValidationMessage("Email", "", new { @class = "text-danger" })
    </div>

    <div>
        @Html.Label("Password")
        <br />
        @Html.Password("Password")
        @Html.ValidationMessage("Password", "", new { @class = "text-danger" })
    </div>

    <div>
        @Html.CheckBox("AgreeToTerms")
        @Html.Label("AgreeToTerms", "I agree to the terms and conditions")
    </div>

    <div>
        <input type="submit" value="Register" />
    </div>

    @if (ViewBag.Message != null)
    {
        <p style="color: green;">@ViewBag.Message</p>
    }
}
```
## 📄 RegistrationDetails.cshtml

This view displays the **User Details** after a successful registration.  
It uses **Strongly Typed Model Binding** with Razor Syntax to show the user's data on the page.


## 🛠️ Code

```csharp
@model _27April.Models.UserModel
@*
    For more information on enabling MVC for empty projects, visit https://go.microsoft.com/fwlink/?LinkID=397860
*@
@{
}

<div>
    <h3>User Details</h3>
    <p><strong>Name:</strong> @Model.Name</p>
    <p><strong>Email:</strong> @Model.Email</p>
    <p><strong>Password:</strong> @Model.Password</p> 
</div>
```
# Strong HTML Forms

## 📄 Nilesh.cs

This file defines the **Nilesh** model for login purposes using basic properties and validation attributes.


## 🛠️ Code

```csharp
using System.ComponentModel.DataAnnotations;

namespace _27April.Models
{
    public class Nilesh
    {
        public string Name { get; set; }
        
        [EmailAddress]
        public string Email { get; set; }
        
        [StringLength(100, MinimumLength = 6, ErrorMessage = "Atleast 6 Letters")]
        public string Password { get; set; }
    }
}

```



## ✅ Second file – **NileshController.cs (Controller)**

```
# 📄 NileshController.cs

This controller handles the login process using the **Nilesh** model and provides validation before accepting user input.

## 🛠️ Code

```csharp
using _27April.Models;
using Microsoft.AspNetCore.Mvc;

namespace _27April.Controllers
{
    public class NileshController : Controller
    {
        public IActionResult Login()
        {
            return View();
        }

        [HttpPost]
        public IActionResult Login(Nilesh nile)
        {
            if (ModelState.IsValid)
            {
                ViewBag.Message = "Loggen In Beautifully!";
                return View();
            }
            else
            {
                return View(nile);
            }
        }
    }
}
```
## 📄 User Registration View (Login Form)

This view is responsible for rendering the **User Registration Form** where users can input their details such as name, email, and password. It uses **strongly-typed HTML helpers** and data validation features from the model.



## 🛠️ Code

```csharp
@model _27April.Models.Nilesh
@*
    For more information on enabling MVC for empty projects, visit https://go.microsoft.com/fwlink/?LinkID=397860
*@

<h2>User Registration</h2>

@using (Html.BeginForm())
{
    <div>
        @Html.LabelFor(x => x.Name)
        @Html.TextBoxFor(x => x.Name)
        @Html.ValidationMessageFor(x => x.Name)
    </div>

    <div>
        @Html.LabelFor(x => x.Email)
        @Html.TextBoxFor(x => x.Email)
        @Html.ValidationMessageFor(x => x.Email)
    </div>

    <div>
        @Html.LabelFor(x => x.Password)
        @Html.PasswordFor(x => x.Password)
        @Html.ValidationMessageFor(x => x.Password)
    </div>

    <div>
        <input type="submit" value="Register" />
    </div>

    @if (ViewBag.Message != null)
    {
        <p style="color:green;">@ViewBag.Message</p>
    }
}




