#[Q]Asp.net normal html input runat=“server” return non-updated value in code-behind
It's because everytime you load the page you override the value of the input the stuff in Page_Load().
And based on the ASP.NET Pipeline Lifecycle, Page_Load is executed first and then controls' event handlers. To avoid that you will need to run the above mentioned line of code only when the page first load...on a GET request and not on a POST request. You can change the Page_Load event handler like this...
```
protected void Page_Load(object sender, EventArgs e)
{
        //code to retrieve data from database and store in server instance
        if(!IsPostBack)
        {//put the initial code here.}   
 }
```