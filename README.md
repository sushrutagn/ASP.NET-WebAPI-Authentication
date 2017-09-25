# ASP.NET-WebAPI-Authentication

This is an example of Basic and Bearer Token authentication in ASP.NET WebAPI 2.0. It also includes the code for Google and Faceook Log-In. UI is developed using HTML, Bootstrap and jQuery. 

Execution: LogIn page is loaded when the application starts. A user may log in using Facebook/Google credentials. Alternatively, a user may register in to the local DB using Register page and use these credentials for logging in. After the successful log in, the user is routed to a protected page which lists employees.

Steps:

1. Run the DB script EmployeeDB.sql to generate required tables along with seed data
2. Create Google and Facebook apps for Social Log-In and copy the Client/App Id and Client/App Secret to the respective fields in App-Start/StartUp.Auth.cs
3. Change the port number from 53907 to the port number on which your application is configured to run in the following files

   a. In LogIn.html,
   
            // Google Sign-In
            $('#btnGoogleLogin').click(function () {
                window.location.href = "/api/Account/ExternalLogin?provider=Google&response_type=token&client_id=self&redirect_uri=http%3A%2F%2Flocalhost%3A53907%2FTemplates%2FLogIn.html&state=GerGr5JlYx4t_KpsK57GFSxVueteyBunu02xJTak5m01";
            });

            // Facebook Sign-In
            $('#btnFacebookLogin').click(function () {
                window.location.href = "/api/Account/ExternalLogin?provider=Facebook&response_type=token&client_id=self&redirect_uri=http%3A%2F%2Flocalhost%3A53907%2FTemplates%2FLogIn.html&state=GerGr5JlYx4t_KpsK57GFSxVueteyBunu02xJTak5m01";
            });
            
      
    b. In GoogleAuthentication.js,
    
          function signupExternalUser(accessToken, provider) {
        $.ajax({
        url: '/api/Account/RegisterExternal',
        method: 'POST',
        headers: {
            'content-type': 'application/json',
            'Authorization': 'Bearer ' + accessToken
        },
        success: function () {
            window.location.href = "/api/Account/ExternalLogin?provider="+provider+"&response_type=token&client_id=self&redirect_uri=http%3A%2F%2Flocalhost%3A53907%2FTemplates%2FLogIn.html&state=GerGr5JlYx4t_KpsK57GFSxVueteyBunu02xJTak5m01";
        },
        error: function (jqXHR) {
            // alert(jqXHR.responseText);
            $('#divErrorText').text(JSON.stringify(jqXHR.responseJSON.ModelState.err[1]));
            $('#divError').show('fade');
        }    
        }); 
        }
   
       
       
       
       
NOTE: This application was configured to run in http://localhost:53907
      
Kindly refer http://csharp-video-tutorials.blogspot.in/2016/09/aspnet-web-api-tutorial-for-beginners.html for ASP.NET WebAPI tutorials. 
This example is based on a similar example illustrated in the above link.
Videos from 18 to 29 explain authentication in WebAPI. Kindly refer videos 18 and 19 for setting up your Google and Facebook Log-In apps.


Kindly re-install the nuGet packages if prompted.
