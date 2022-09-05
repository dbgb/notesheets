# Working with ASP.NET: Notesheet

## Create .NET gitignore file

```dotnet-cli
dotnet new gitignore
```

## `ASP.NET`

### User registration

```http-POST
{
  "Email": "username@email.test",
  "Password": "Password123@",
  "ConfirmPassword": "Password123@"
}

POST https://localhost:<PORT>/api/account/register
```

### Get bearer token with user credentials

```http-GET
# URL encoded form
> grant_type password
> username <USERNAME>
> password <PASSWORD>

GET https://localhost:<PORT>/token

# Copy "access_token" from response
```

### Perform authorized operation

```http-GET
# Enter bearer token

GET https://localhost:<PORT>/api/values

# Receive response
```
