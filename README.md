ONce upon a time in Mumbai
	Create a project with 5 controller
1.	Home
2.	About
3.	Contact
4.	Gallery
5.	Services
	Create a project with one controller (index) and show calculator result on web browser
	A=10000, b=50;
	Create a project with one master  and one child
Design header and footer in master and display “I am the child”
With header footer

1.	Create sign in page
With user name and password: if usernamr=”Techpile” , password=”Techpile123”
Open new page = “welcome to the techpile”, Data receive to the parameter of action method
2. Create regstration page
Name, fathername, dob, gender, qualification(ddl)
Show all data of from to the next greeting page

05-01-2022
Task 1:
Create a registeration page with 
Name
 gender
 fathers name
Qualification
Hobbies
Address
Course
Branch
Mobnmber
Email
Password
Confirm password
Submit
Anu field should not be null and password and confirm password – redirect to signin

Signin : 
Emailid
Password
Login Button- on click of login redirect to profile page page if email and password matches to registtation data
1.registration -> login -> profile (show all data in p tag)



06-01-2022
In different project
Registration: Namr, FatherName, Contact Number, dob, email, password
Product : Product Name, quantity, color, size, brand, add date

-	Store data in db and show successful message


7-1-2022

Registration : 
Name 
Contact number
Email id
Password
Address
Pincode
Picture




2 form: college
Addemployee : name, qualification, mobno, email, post, picture
Addcourse : course name, seates, course pic, 
Submit

using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
using System.Data;
using System.Data.SqlClient;
using System.Configuration;

namespace Projrct_1.Controllers
{
    public class HomeController : Controller
    {
        public ActionResult Index()
        {
            return View();
        }

        [HttpPost]
        public ActionResult Index(string name,string number, string email,string password, string address,int pin,HttpPostedFileBase pic)
        {
            string picname = "";
            if(pic!=null)
            {
                picname = pic.FileName;
                pic.SaveAs(Server.MapPath("/content/File/")+picname);
            }             

            string con = ConfigurationManager.ConnectionStrings["MyReg"].ToString();
            SqlConnection connection = new SqlConnection(con);
            
            if(connection.State==System.Data.ConnectionState.Closed)
                connection.Open();

            SqlCommand command = new SqlCommand("sp_registration", connection);
            command.CommandType = CommandType.StoredProcedure;

            command.Parameters.Add("@name", name);
            command.Parameters.Add("@number", number);
            command.Parameters.Add("@email", email);
            command.Parameters.Add("@password", password);
            command.Parameters.Add("@address", address);
            command.Parameters.Add("@pin", pin);
            command.Parameters.Add("@pic", picname);

            int num= command.ExecuteNonQuery();
            connection.Close();
            if(num>0)
            {
                ViewBag.msg = "Record Addes Successfully";
            }
            else
            {
                ViewBag.msg = "Record not Added, Please try again";
            }
            return View();
        }
    }
}


Index




Write a program to print table of a number
Wap a to make a list of a fruits and print all element in h1 tag
Wap to make a list of student details like name father name , date of birth, contacr number email id and priint student detail in a table row
Wap to store 3 integer number and print greatest number using else-if ladder
Wap to return student details by controller in list store in tempdata and print list element in a view.

Wap to upload file by registration page and print file name on signin view by tempdata;
Wap to input first name and last name and print full name on view by using tempdata.


Controller 

using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
using System.IO;

namespace Projrct.Controllers
{
    public class HomeController : Controller
    {
        public ActionResult Index()
        {
            return View();
        }
        [HttpPost]
        public ActionResult Index(HttpPostedFileBase profile,HttpPostedFileBase resume)
        {
            if (profile != null && resume!=null)
            {
                string path=Path.Combine(Server.MapPath("/content/profile"),profile.FileName);
                profile.SaveAs(path);
                //resume.SaveAs(Server.MapPath("/content/resume/"));
                string resumepath = Path.Combine(Server.MapPath("/content/resume"), resume.FileName);
                resume.SaveAs(resumepath);
            }
            return RedirectToAction("about");
        }
        public ActionResult About()
        {
            ViewBag.msg = "About Page";
            ViewData["data"] = "Data from view data ";
            return View();
        }
        public ActionResult Register()
        {
            return View();
        }
        [HttpPost]
        public ActionResult Register(string name,string email, string pass)
        {
            //TempData["name"] = name;
            //TempData["email"] = email;
            //TempData["pass"] = pass;

            List<string> student = new List<string> { name,email,pass};
            TempData["Data"] = student;
            return RedirectToAction("SignIn");
        }

        public ActionResult SignIn()
        {
            
            return View();
        }
    }
}


Register


@{
    ViewBag.Title = "Register";
    Layout = "~/Views/Shared/_Layout.cshtml";
}

<h2>Register</h2>
<form action="" method="post">
    <input type="text" name="name" placeholder="Enter Your Name"/> <br />
    <input type="email" name="email" placeholder="Enter Your Email"/><br />
    <input type="password" name="password" placeholder="Enter Your password"/><br />
    <input type="submit" value="Register"/>

</form>



Signin


@{
    ViewBag.Title = "SignIn";
    Layout = "~/Views/Shared/_Layout.cshtml";
}

<h2>SignIn</h2>
@{List<string> data = TempData["Data"] as List<string>;}
@if(TempData["Data"] != null)
{
    foreach (string val in data)
    {
     @val
     <br />
    }
}

@(5 * 2)
@{int a = 30; int b = 60; }
@(70*40) 
@if (a > b) { 
<p>@a is greater than @b </p>
}
else{
    <p>@b is greater than @a </p>
}




If you could successfully sign then print all data in welcome page and print in text









Create new data base with new table
1.	Create reg page for student
Name
Mobile Number,
Email primary key
Password
Dob
Address
Picture

2.	Create a search student page with a text box :
Enter emal id of student if :
If email if not present in db then print record not found
Otherwise display the record of student in a ta
3.	Display all records on get method


Click on delete buttun all tr changed in input type text




Create a page show all data desc of regdate with action
//on click of delete, remove record from database

19-01-2021

1.	Add all Departments of a college in db:
Department Name
Department Seat
Department Head
2.	Register a employee in database with following records
Name
Gender
Contact Number
Email
Password
Highest Qualification
Department : bind all department list from database
Picture
3.	Show all employee records with department name


20-01-2021

Category :  in db-id ,name ,picture
	Category Name
	Category Picture

Add Product
	Category -> dropdownlist
	Product Title
	Product MRP(int)
	Sale Rate(int)
	Brand Name
	Description	
	Picture

	In db- id, add date, In stock(bit)

Show : 
1.	Show Category :
Picture, Name 

2.	Product : 
Picture, Brand, Mrp, Sale Rate, Discount, Title, Description,


21/01/2022
1.	Add Product		
2.	Display All Product
3.	Delete Product
4.	Show List of Product in Div
Title,Brand, MRP, Sale Rate, Description, Picture
5.	Update Category Name and Picture



Neosoftech








Create new project
Create a ADO Connection  class
1.	ExecuInsertUpdateDelete
2.	ExecuteDatable

Registration Form :
	Name
	Dob
	Email
	Password
	Picture
(Save into Database, Show all data of student on Index page)




Name,Dob, Email,Password,Contact Number, Profile Picture, Gender , Status

DB-Student Id, Name,Dob, Email,Password,Contact Number, Profile Picture, Gender , Status

29/01/2022

Read Garbej Collection, Heap
