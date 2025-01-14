# EntityFrameworkCore.EncryptColumn
Hello, you can store your data in encrypted form in your database with this package. 

## How to use?
Install "[EntityFrameworkCore.EncryptColumn](https://www.nuget.org/packages/EntityFrameworkCore.EncryptColumn)" package to your project. 

Specify your encryption key in the constructor method of your DbContext class and create a instance from the encryption provider.  Yout encryption key must be 128 bit!

```csharp
private readonly IEncryptionProvider _provider;
public ExampleDbContext()
{
    this._provider = new GenerateEncryptionProvider("example_encrypt_key");
}
```
Then specify that you will use an encryption provider in the "OnModelCreating" method. 

```csharp
modelBuilder.UseEncryption(this._provider);
```

That's it! Now you can encrypt the parameters in the class you want by adding the "EncryptColumn" attribute. 

```csharp
public class User
{
    public Guid ID { get; set; }
    public string Firstname { get; set; }
    public string Lastname { get; set; }
    [EncryptColumn]
    public string EmailAddress { get; set; }
    [EncryptColumn]
    public string IdentityNumber { get; set; }
}
```

