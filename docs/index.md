#Cake.CakeMail Documentation

Cake.CakeMail is an Addin for [Cake](http://cakebuild.net/) which allows the sending of email using [CakeMail](https://cakemail.com).

```csharp
#addin Cake.CakeMail

var apiKey = EnvironmentVariable("CAKEMAIL_API_KEY");
var userName = EnvironmentVariable("CAKEMAIL_USERNAME");
var password = EnvironmentVariable("CAKEMAIL_PASSWORD");

Task("SendEmail")
    .Does(() =>
{
    try
    {
        var result = CakeMail.SendEmail(
                senderName: "Bob Smith", 
                senderAddress: "bob@example.com",
                recipientAddress: "jane@example.com",
                subject: "This is a test",
                htmlContent: "<html><body>This is a test</body></html>",
                textContent: "This is a test",
                settings: new CakeMailEmailSettings
                {
                    ApiKey = apiKey,
                    UserName = userName,
                    Password = password
                }
        );

        if (result.Ok)
        {
            Information("Email succcessfully sent");
        }
        else
        {
            Error("Failed to send email: {0}", result.Error);
        }
    }
    catch(Exception ex)
    {
        Error("{0}", ex);
    }
});
```