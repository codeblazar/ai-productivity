---
marp: true
theme: default
size: 16:9
paginate: true
author: Peter Kenny
header: Ai for Boosting Productivity
footer: Copyright © 2024 Republic Polytechnic. All rights reserved. 
style: |

    @import url('https://unpkg.com/tailwindcss@^2/dist/utilities.min.css');

    section {
      color: #246;
      font-size: 30px;
      }

    section.lead h1 {
        font-size: 2.5em;
        text-align: center;
    }

    section.lead h2 {
        font-size: 1.25em;
        text-align: center;
    }

    section.lead img {
        display: block;
        margin-left: auto;
        margin-right: auto;
    }

    /* Reduce size of header, footer & page numbers */
    header, footer, section::after {
        font-size: 0.4em;
        position: absolute;
        right: 0;
        text-align: right;
        width: 95%;
        padding-right: 0em; /* Adjust padding as necessary */
    }

    img[alt~="center"] {
      display: block;
      margin: 0 auto;
    }
  
---

<!-- 
_class: lead
_paginate: false
-->

![width:250px](https://raw.githubusercontent.com/codeblazar/FileImageShare/db12f70db388a660aa1a01373a8cf975bc07d2c5/Branding/RPnoTag.png)
<br/>

# AI for Boosting Productivity

## Presentation by: **School of Infocomm**

---
# Overview

<div class="grid grid-cols-10 gap-10">
<div class="col-span-5">
<br/>

- AI Landscape
- Tools
- Automation
- Creation
- Trends
  
</div>
<div class="col-span-5">

![](/images/AiBoostProductivity.jpeg)

</div>

---

# Layout **justifications**

- Shared elements within a web app are frequently used by many pages with an app.
    - Scripts
    - Stylesheets
- These shared elements may be defined in a layout `.cshtml` file. 
- The name usually starts with an underscore. E.g.,
    - `_Layout.cshtml`
    - `_Travel.cshtml`
    - `_Candidate.cshtml`
    - `_Organic.cshtml`
- Layouts reduce duplicate code in views.
- A layout can be referenced by any view used within the app. 

---

# **Using** a layout

## Specify a Layout in individual views

```cs
@{
    // Inside each .cshtml view file
    Layout = "_Candidate";
}
```

<div class="columns-right">

## Specify a layout for all views
Use the `Views/_ViewStart.cshtml` file

```cs
@{
    // Inside _ViewStart.cshtml file    
    Layout = "_Travel";
}
```

---    

# Including scripts and stylesheets in a layout (e.g., `_Candidate.cshtml)`

<div class="grid grid-cols-3 gap-6">
<div class="col-span-2">

<br/>

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <link href="~/lib/bootstrap/css/bootstrap.min.css" rel="stylesheet" />
    <script src="~/lib/bootstrap/umd/popper.js"></script>
    <script src="~/lib/bootstrap/js/bootstrap.min.js"></script>
    <link href="~/lib/bootstrap/font/bootstrap-icons.min.css" rel="stylesheet" />
    <title>Candidate</title>
</head>
<body>
    <div class="container border-bottom">
        <nav class="navbar navbar-expand-md">
            <div class="container-fluid">

                <a class="navbar-brand" asp-controller="Candidate" asp-action="Index">
                    <img src="~/images/applicant.svg" height="72" />
                    Candidates
                </a>
```                

</div>
<div>

## Note: 
The order of the inclusions in the `head` element is important. Include the `bootstrap.min.css`, `popper.js`, `bootstrap.min.js` and `bootstrap-icons.min.css` in the order shown for predictable results.

</div>
</div>

---  

# Including a `navbar` in a layout (e.g., `_Candidate.cshtml`)

<div class="grid grid-cols-3 gap-6">
<div class="col-span-2">

<br/>

```html
    <div class="container border-bottom">
        <nav class="navbar navbar-expand-md">
            <div class="container-fluid">

                <a class="navbar-brand" asp-controller="Candidate" asp-action="Index">
                    <img src="~/images/applicant.svg" height="72" />
                    Candidates
                </a>

                @*Button below (hamburger menu) appears when viewport too small.*@
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                        data-bs-target="#navbarSupportedContent">
                    <span class="navbar-toggler-icon"></span>
                </button>

                <ul class="navbar-nav mr-auto">
                    <li class="nav-item">
                        <a class="nav-link"
                           asp-controller="Candidate"
                           asp-action="Create">New Candidate</a>
                    </li>
                </ul>

                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                </div>
            </div>
        </nav>
    </div>>
```

</div>
<div>

## Note: 
When included in a layout, the `navbar` is only specified once, then used throughout the application.

</div>

---

# Including a `RenderBody()` in a layouts (e.g., `_Candidate.cshtml`)

<div class="grid grid-cols-3 gap-6">
<div class="col-span-2">

<br/> 

```html
    <div class="container m-3">
        @RenderBody()
    </div>

</body>
</html>
```

</div>
<div>

## Note:
The code from a view using a layout is inserted at the position of `@RenderBody()`. Therefore the view using the layout is only required to render the specifics of that view. 

</div>

---

# Referencing the layout in a view

<div class="grid grid-cols-3 gap-6">
<div class="col-span-2">

<br/> 

```html
@{
   Layout = "_Candidate";
}

@model Candidate
<h1>@Model.CName</h1>
<img src="~/candidates/@Model.PicFile">

<dl class="dl-horizontal">
   <dt>RegNo : </dt>
   <dd>@Model.RegNo</dd>
   <dt>Gender : </dt>
   <dd>@Model.Gender</dd>
   <dt>Height : </dt>
   <dd>@Model.Height </dd>
   <dt>Birthdate : </dt>
   <dd>@string.Format("{0:yyyy-MM-dd}", Model.BirthDate)</dd>
   <dt>Race : </dt>
   <dd>@Model.Race </dd> 
   <dt>Clearance : </dt>
   <dd>@Model.Clearance </dd>
</dl>
```

</div>
<div>

## Notes: 
- The **Razor Layout Directive** is specified in the top of the view.

- The code below is replaces the call to the **Razor RenderBody Method** `@RenderBody()` in the layout.

- The layout enables the removal of "boiler plate" text (e.g., `<html>`, `<head>`, `<body>`, navigation bar and scripts) from the view. (i.e., DRY - Don't Repeat Yourself)

</div>

---

<!-- _class: lead -->
# `_ViewImports.cshtml`& Tag helpers 

---

# `_ViewImports.cshtml`

<div class="grid grid-cols-3 gap-6">
<div class="col-span-2">

The `_ViewImports file` supports the following Razor directives:
- `@using` :pushpin:
- `@addTagHelper` :pushpin:
- `@removeTagHelper`
- `@tagHelperPrefix`
- `@model` 
- `@inherits`
- `@inject`

The following code is used in `_ViewImports.cshtml` to simplify the code for Lesson 08.

```
@using System.Data
@using Lesson08.Models

@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers
```

</div>
<div>

## Advantages:

- Eliminates `@using Lesson08.Models` in all views that use a Model.
- Eliminates `@using System.Data` in all views that use a `DataRowCollection`.
- `@addTagHelper` **enables** common tag helpers.

</div>

---

# Tag helpers

- Tag helpers 
  - Enable server-side code to easily create and render HTML elements in `.cshtml` files.
  - Look similar to standard HTML **elements** and **attributes**.
  - Target HTML elements based on **element name**, **attribute name**, or **parent tag**. 
- Tag helpers used in today's Lesson
    - `asp-for`
    - `asp-controller`
    - `asp-action`
    - `asp-route-id`
    - `asp-validation-for`
    - `asp-validation-summary`
- Tag Helpers may be **enabled** in `_ViewImports.cshtml` :pushpin:

For a more details and additional help please reference [Tag Helpers in MVC](https://learn.microsoft.com/en-us/aspnet/core/mvc/views/working-with-forms?view=aspnetcore-7.0)

---

# Tag helpers enable code **simplification**

<div class="grid grid-cols-2 gap-6">
<div class="col-span-1">

## Before

```html
<!DOCTYPE html>
<head>...</head>
<body>
   @if (User.Identity.IsAuthenticated)
   {
        @*For authenticated users*@
        @await Html.PartialAsync("TravelUser")>
   }
   else
   {
        @*For unauthenticated (guest) users*@
        @await Html.PartialAsync("TravelGuest")
    }

   <div class="container mt-10">
      @RenderBody()
   </div>
```
</div>

<div>
<div class="col-span-1">

## After

```html
<!DOCTYPE html>
<head>...</head>
<body>
   @if (User.Identity.IsAuthenticated)
   {
        @*For authenticated users*@
        <partial name="TravelUser">
   }
   else
   {
        @*For unauthenticated (guest) users*@
        <partial name="TravelGuest">
   }

   <div class="container mt-10">
      @RenderBody()
   </div>
```

</div>

---

# Tag helpers enable code **clarity**

<div class="grid grid-cols-2 gap-6">
<div class="col-span-1">

## Before

```html
@foreach (Candidate cdd in Model)
{
  <div class="col">
    <div class="card align-items-center">
      <img src="~/candidates/@cdd.PicFile" 
           width="100" class="mx-3 mt-3">
      <div class="card-body">
        <div class="card-title">
          <a href="~/Candidate/Display/@cdd.RegNo">
            @cdd.CName
          </a>
        </div>
      </div>
    </div>
  </div>
}
```
</div>

<div>
<div class="col-span-1">

## After

```html
@foreach (Candidate cdd in Model)
{
  <div class="col">
    <div class="card align-items-center">
      <img src="~/candidates/@cdd.PicFile" 
           width="100" class="mx-3 mt-3">
      <div class="card-body">
        <div class="card-title">
          <a asp-controller="Candidate"
            asp-action="Display"
            asp-route-id="@cdd.RegNo">
            @cdd.CName
          </a>
        </div>
      </div>
    </div>
  </div>
}
```

</div>

---

# Tag helpers enable code **generation**

<div class="grid grid-cols-2 gap-6">
<div class="col-span-1">

## You write

```html
<div class="col-md-3 mb-3 form-floating">
  <input type="number" 
         min="0" 
         class="form-control" 
         asp-for="RegNo"
         placeholder="RegNo" 
         required />
  <label asp-for="RegNo">Reg#</label>
</div>
```
</div>

<div>
<div class="col-span-1">

## Framework creates

```html
<div class="col-md-3 mb-3 form-floating">
  <input type="number" 
         min="0" 
         class="form-control" 
         placeholder="RegNo" 
         required data-val="true" 
         data-val-required="The RegNo field is required." 
         id="RegNo" 
         name="RegNo" 
         value="" />
  <label for="RegNo">Reg#</label>
</div>
```

</div>

---
# Tag helpers enable a **validation summary** 

- The validation summary tag helper is used to show a list of form **validation errors**.
- The validation summary tag helper is usually at the **top of the form**. 
- Simple validation errors are derived from the **column names**.
- A sample from the `Create.cshtml` view is shown below:

```html
<div asp-validation-summary="All" class="text-danger"></div>
```

Sample output is:
![center width:450px](https://raw.githubusercontent.com/codeblazar/FileImageShare/main/PET/C236/lesson-08/pi-0803-2022.png)

---
<!-- _class: lead -->
# Model Binding &  C# Attributes

---

# Introduction to **model binding**

Model binding in ASP.NET Core maps data from **HTTP requests** to **action method parameters**. 
- Parameters may be simple types such as `string`, `int`, or `float`, or they may be complex types. 
- Model binding creates enormous productivity gains by simplifying
  - Data Conversion
  - Data Validation

---

# Before and after **model binding**

<div class="grid grid-cols-2 gap-6">
<div class="col-span-1">

## Before

```cs
public IActionResult AddPost(IFormFile photo)
  {
    IFormCollection form = HttpContext.Request.Form;
    string title    = form["Title"].ToString().Trim();
    string city     = form["City"].ToString().Trim();
    string story    = form["Story"].ToString().Trim();
    string tripDate = form["TripDate"].ToString().Trim();
    string duration = form["Duration"].ToString().Trim();
    string spending = form["Cost"].ToString().Trim();
    ...

```
</div>

<div>
<div class="col-span-1">

## After

```cs
public IActionResult Create(Trip trip, IFormFile photo)
  {
  ...  
```
## Note: 
Model binding is achieved by the addition of a parameter `trip` of type `Trip` in the action.
</div>

---

# **C\#** Attributes

- Attributes are used in C# to convey **declarative information** or **metadata** about various code elements such as **methods**, **assemblies**, **properties**, **types** and other elements.
- Attributes convey information on the **behaviour** of the element to which they are attached.
- A declarative tag is depicted by square brackets placed **above** the method or class for which behaviour is to be **modified**.
## Examples:

<div class="grid grid-cols-2 gap-6">
<div class="col-span-1">

```cs
[HttpPost]
public IActionResult Create(Candidate cdd, IFormFile photo)
{ ...
```
```cs
[AllowAnonymous]
[HttpPost]
public IActionResult Login(UserLogin user)
{...
```    
</div>

<div>
<div">

```cs
public class Candidate
{
    [Required]
    public string CName { get; set; } = null!;
    ...
    [Required]
    public string Race { get; set; } = null!;
    ...
```
</div>

---
# **Controller** attributes

<div class="grid grid-cols-2 gap-6">
<div class="col-span-1">

## `[HttpGet]`

- Return a view (form) to the user for input.
- The view can be empty or pre-populated with data for editing.
- A model is be used to pass data to the form for editing.

```cs
[HttpGet]
public IActionResult Create()
{
  return View();
}
```

</div>
<div>

## `[HttpPost]`

- Receive user entered data from a view (form).
- Input data is passed from view to controller using a model.
- Data is used by the action method.

```cs
[HttpPost]
public IActionResult Create(Candidate cdd, IFormFile photo)
  {
  if (!ModelState.IsValid)
    {..
```

</div>

---

# **Model** attributes

- `string` properties that are required have the `[Required]` attribute attached. **Recall**: Nullability and the null forgiving operator are applied in this model for `CName and `Gender`.
- `int` can never be null, only zero, so the `[Required]` attribute is not necessary.
- Similarly, `double` and `DateTime` can never be null, so the `[Required]` attribute is not necessary.
```cs
public class Candidate
{
    public int RegNo { get; set; }
    [Required]
    public string CName { get; set; } = null!;
    [Required]
    public string Gender { get; set; } = null!;
    public double Height { get; set; }
    public DateTime BirthDate { get; set; }
    ...
    // bool's Default is [False]
    public bool Clearance { get; set; }
    ...
```  
---

# **DataType** attribute: 
Attributes other than `[Required]` can be added to the model.
- In the `Trip` class, the datatype `DateTime` matches the database.
- However, the system only requires the **date** component. The **time** component is of no interest.
- Bootstrap 5 will add **both** date and time pickers to the form.
- An additional `[DataType(DataType.Date)]` attribute placed on `TripDate` helps resolve this matter and ensures Bootstrap will only create a picker for the date component.

```cs
public class Trip
{
    ...
    [Required]
    [DataType(DataType.Date)]
    public DateTime TripDate { get; set; }
    ...
}
```

---

# Validation using a **model**
- There is no longer any requirement to check for null attributes, because that is now completed by the model.
- In place, simply check the `ModelState`. If the state is invalid return the model to the view.
- The view can show a validation summary using the tag helper `asp-validation-summary`.
- If validation is successful, the model properties can be used directly in an **SQL** statement

<div class="grid grid-cols-2 gap-6">
<div class="col-span-1">

## **Successful** validation defined by `ModelState`

The model (`ccd`) is returned to the view.
```cs
[HttpPost]
public IActionResult Create(Candidate cdd, IFormFile photo)
{
  if (!ModelState.IsValid)
    {
      ViewData["Message"] = "Invalid Input";
      ViewData["MsgType"] = "warning";
      return View(cdd);
    }
else ...
```
</div>
<div>

## **Unsuccessful** validation 
A validation summary (`asp-validation-summary`) is shown to the user. This validation summary contains all errors that were found when validating the user input against the model.

```html
<div class="form-group row">
  <div class="offset-sm-2 col-sm-4">
    <div asp-validation-summary="All" class="text-danger">
    </div>
  </div>
</div>

```
---

# Turning **off** validation in a controller

- Occasionally it is useful/necessary to **override** the default validation on a property given by the model. This requirement may occur when
  - Checking validation prior to retrieving additional information (e.g., the username from the claim) to populate the property
  - Updating a record where the property is not changed
  - Updating/inserting a record where the property can be derived from another property.
- In this case use `ModelState.Remove` as demonstrated in the **Travel/Create** [POST] action, a portion of which appears below.

```cs
...
ModelState.Remove("Picture");     // No Need to Validate "Picture" - Derived from "Photo".
ModelState.Remove("SubmittedBy"); // Ignore "SubmittedBy". See claim below.
if (!ModelState.IsValid)
{
    return View("Create");
}
else
{ ...
```

---

<!-- _class: lead -->
# Passwords & Authentication

---
# **Storing** passwords

- A **hash** function is used to **encrypt** passwords before they are stored in a database.
- Encrypting passwords ensures that, even if the database is breached, an individual's passwords remain private.
- The function used is **one-way**, meaning passwords **cannot be decrypted**.

```sql
CREATE TABLE TravelUser (
  UserId    VARCHAR(10) PRIMARY KEY,
  UserPw    VARBINARY(50) NOT NULL,
  FullName  VARCHAR(50) NOT NULL
);

INSERT INTO TravelUser (UserId, UserPw, FullName) VALUES 
('john',    HASHBYTES('SHA1', 'password1'), 'John Lim'),
('pauline', HASHBYTES('SHA1', 'password3'), 'Peter Chan');
```
| UserId  | UserPw                                     | FullName     |
| ------- | ------------------------------------------ | ------------ |
| john    | 0xE38AD214943DAAD1D64C102FAEC29DE4AFE9DA3D | John Lim     |
| pauline | 0x1119CFD37EE247357E034A08D844EEA25F6FD20F | Pauline Chan |

---

# Authentication **user**

- The same function that was used to encrypt the password originally is used to encrypt the value the user enters.
- The two encrypted values, one entered by the user and the other in the database, are compared.
- If the two encrypted values (hashes) match, then the user is authenticated.

```cs
private static bool AuthenticateUser(string uid, string pw,
                              out ClaimsPrincipal principal)
{
    principal = null!;
    string sql = @"SELECT * FROM TravelUser 
                   WHERE UserId = '{0}' AND UserPw = HASHBYTES('SHA1', '{1}')";
    string select = string.Format(sql, uid, pw);
    DataTable ds = DBUtl.GetTable(select);
    if (ds.Rows.Count == 1)
    {
        principal =
           new ClaimsPrincipal(
              new ClaimsIdentity(
                 new Claim[] {
                  new Claim(ClaimTypes.Name, ds.Rows[0]["FullName"].ToString()!)
                 },
                 CookieAuthenticationDefaults.AuthenticationScheme));
        return true;
    }
    return false;
}
```

---
# Authentication **implementation**

To fully implement authentication, the following files need to be modified. The code for the implementation is not included in this slide deck. **Please refer to Lesson 08 code for details**.

<div class="grid grid-cols-2 gap-6">
<div class="col-span-1">

- Code entry point (`Program.cs`)
  - `builder.Services.AddAuthentication(...)`
  - `app.UseAuthentication();`
  - `app.UseAuthorization();`

- Controllers (`AccountController.cs`)
  - `AccountController.cs`
    - `Login [HttpGet],[AllowAnonymous]`
    - `Login [HttpPost],[AllowAnonymous]`
    - `Logoff [Authorize]`

</div>
<div>

- Models (`UserLogin.cs`)
  - `UserID [Required]`
  - `Password [Required]`

- Views (`Login.cshtml`)
  - `UserId`
  - `Password`

</div>

---

# Authentication check in a **view**

The authentication check for Lesson 08 is placed in the shared layout called `_Travel.cshtml` By placing the authentication check in this file, the code is able to render the correct view.
<br/>

<div class="grid grid-cols-3 gap-6">
<div class="col-span-2">

```html
<!DOCTYPE html>
<html>
<head> .... </head>
<body>
    @if (User.Identity!.IsAuthenticated)
    @*For authenticated users*@
    {
        <partial name="TravelUserNav" />
    }
    else
    @*For unauthenticated (guest) users*@
    {
        <partial name="TravelGuestNav" />
    }

    <div class="container mt-10">
        @RenderBody()
    </div>

</body>
</html>
```

</div>
<div>

## Note:

- If the username and password are validated, then the navigation for an authenticated user is displayed.
- If the username and password are **not** validated, then the navigation for a guest user is displayed.

</div>

---
# Authentication check in a **controller**

- The authorization check in a controller is performed by using an annotation. 
- Note: The `userid` is retrieved from the **claim**.

```cs
[Authorize]
public IActionResult MyTrips()
{
  string userid = User.FindFirst(ClaimTypes.NameIdentifier)!.Value;
  string select = string.Format(@"SELECT * FROM TravelHighlight 
                                  WHERE UserId = '{0}'", userid);
  List<Trip> list = DBUtl.GetList<Trip>(select);
  return View("MyTrips", list);
}
 ```
---

<!-- _class: lead -->
# `DBUtl.cs` additional functionality

---

# `DBUtl.GetList<ModelClass>`

- New function returns a `List<ModelClass>` based on the **SQL**.
- **Important**: The property names in the model class **must match** the column names in the database table. These names are **case sensitive**.
- Mismatches between database and model are not tolerated by the framework.
<br/>
<div class="grid grid-cols-2 gap-6">
<div class="col-span-1">

```cs
public class Candidate
{
   public int RegNo { get; set; }
   public string CName { get; set; }
   public string Gender { get; set; }
   public double Height { get; set; 
   public DateTime BirthDate { get; set; } 
   public string Race { get; set; }
   public bool Clearance { get; set; } 
   public string PicFile { get; set; }
}
```

</div>
<div>

```sql

CREATE TABLE Candidate (
   RegNo      INT PRIMARY KEY,
   CName      VARCHAR(50) NOT NULL,
   Gender     CHAR        NOT NULL,
   Height     FLOAT       NOT NULL,
   BirthDate  DATE        NOT NULL,
   Race       VARCHAR(5)  NOT NULL,
   Clearance  BIT         NOT NULL,
   PicFile    VARCHAR(30) NOT NULL 
);
```
</div>

**:warning: Note:** After you have created the class, you must consider **nullability**, and modify the class accordingly.
E.g., `public string CName { get; set; } = null!;`

---
# **Calling** `DBUtl.GetList<ModelClass>`

```cs
public IActionResult Index()
{
  List<Candidate> lstCandidate =
    DBUtl.GetList<Candidate>("SELECT * FROM Candidate ORDER BY CName");
  return View(lstCandidate);
}
```    
![center width:450px ](https://raw.githubusercontent.com/codeblazar/FileImageShare/main/PET/C236/lesson-08/pi_0802-2022.png)

---

# Display models with **multiple rows**
- Use the correct razor model directive `@model List<Candidate>`.
- Loop through using a `foreach` statement.
```html
...
@model List<Candidate>
<h1>All Candidates</h1>
...
<div class="row row-cols-sm-4 g-3">
  @foreach (Candidate cdd in Model)
  {
    <div class="col">
      <div class="card align-items-center">
        <img src="~/candidates/@cdd.PicFile" width="100" class="mx-3 mt-3">
        <div class="card-body">
          <div class="card-title">
            <a asp-controller="Candidate"
               asp-action="Display"
               asp-route-id="@cdd.RegNo">
               @cdd.CName
            </a>
          </div>
        </div>
      </div>
    </div>
  }
</div>
```

---

# Retrieve a **single value**

- Example can be found in the **Candidate** controller, **Display** action.
- Select the record based on **id**.
- Take the **first** record returned, which will always be record `[0]`.

```cs
public IActionResult Display(int id)
{
   string sql = String.Format(@"SELECT * FROM Candidate 
                                 WHERE RegNo = {0}", id);
   List<Candidate> lstCandidate = DBUtl_orig.GetList<Candidate>(sql);
   if (lstCandidate.Count == 0)
   {
      TempData["Message"] = $"Candidate #{id} not found";
      TempData["MsgType"] = "warning";
      return RedirectToAction("Index");
   }
   else
   {
      // Get the FIRST element of the List
      Candidate cdd = lstCandidate[0];
      return View(cdd);
   }
}
```
---

# Solving the problem

- Layouts are to be used in the solution to Lesson 08.
- Lesson 08 moves from HTML attributes to ASP.NET **tag helpers**. Because of this change, HTML tags such as `min`, `step` and `required` have been removed.
- The use of **attributes** will be extended in Lesson 09, so it is important to understand their use in models and controllers.
- Please use the **tag helpers** methods in  your code. You can use the **Candidates** system for reference.

---

# Special Note for 2022 Classes:

## Full solutions to problems will no longer be released.
Please use your time in class to complete the problem to the best of your ability. 

---

<!-- _class: lead -->

# End of Lesson 08

