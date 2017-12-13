
Two-way data binding

```
Create Form
    |
    |
Abstract Form
    |
    |
NamedAccount Model
```

```
-------------------------------------------------
|               Data Access Layer               |
-------------------------------------------------
Model     |    Object
Store     |    Access
```

We have model and store for the named account. When we changed data in the store, the framework will automatically send an ajax call 'update' to the backend and update the data. It's like two-way data binding.

Access file: `/apps/search/lib/data/NamedAccountAccess.php`
