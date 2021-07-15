---
title: Upgrading From IdentityServer 3 to IdentityServer 4
date: 2018-02-07T09:00:45+00:00
author: Thomas
layout: single
categories:
  - .NET Core
  - asp.net core
  - Identity Server
---
Upgrading from IdentityServer 3 to 4 isn't too tricky but there are some traps you can fall into if you are not careful.

# Type Changes

## Scopes are now API Resources

Scopes in IdentityServer 3 were used to define a resource and the secret required to get access to that resource. Now, this class has been updated to an [API Resource](http://docs.identityserver.io/en/release/reference/api_resource.html) as an example of how the new object might look like:

```json
{
  "Name": "MyApiRescource",
  "ApiSecrets": [
    {
      "Value": "MyAPIResouceSecret"
    }
  ],
  "Scopes": [
    {
      "Name": "MyScopeName",
      "DisplayName": "My Scope Display Name"
    }
  ]
}
```

As you can see above the Scopes are now handled as a property of an API Resource. Clients now request an API Resource and a valid associated scope. If you forget to add the Scopes as I did you will get invalid Scope errors when trying to request a authorisation token so be careful to include them!

# SDK Changes

## AddInMemoryScopes() Renamed to AddInMemoryApiResources()

Because _Scopes_ are now _ApiResources _the method to add in-memory versions of them has been renamed - but can be used with the same type as before.

## SetSigningCredential() Renamed to AddSigningCredential()

This is a minor change presumedly to make the intent of the method a little clearer and works the same way as before.

## SetTemporarySigningCredential() Renamed to AddDeveloperSigningCredential()

Again as above this is just a naming change.

# Summary

The above are the only changes I encountered when upgrading from version 3 to 4 and once I noticed the missing Scopes in the APIRescouce object the upgrade was pretty straightforward. There are probably other changes I didn't encounter but hopefully, they are similarly easy to transition to!