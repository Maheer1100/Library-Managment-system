# Library Management System (ASP.NET Core MVC)

Manage books and members, issue and return books, and track overdue books with an automatic late fine.

## Run it

1. Install the .NET SDK, then run `dotnet --version`.
2. If it does not start with 10, open `LibraryManagement.csproj` and change the two lines at the top:
   `net10.0` to `net8.0` (or `net9.0`) and `10.0.*` to `8.0.*` (or `9.0.*`).
3. In this folder, run:

```
dotnet restore
dotnet run
```

4. The browser opens at `http://localhost:5080` (the link is also shown in the terminal).

The first run creates `library.db` (SQLite) with all tables and a few sample books and members.
To start fresh, stop the app and delete `library.db`.

## What it does

- **Books:** add, edit, delete, search by title/author/ISBN, filter by category and status.
- **Members:** add, edit, delete, search. Emails must be unique.
- **Issues:** issue a book for 1 to 60 days, one member can hold up to 3 books, return a book, filter by currently issued / overdue / returned.
- **Late fine:** Rs 10 per day after the due date (change `FinePerDay` in `Models/IssueRecord.cs`).
- **Dashboard:** totals, overdue warning, recent activity.
- Books and members with issue history can't be deleted.

## Folder guide

| Folder | What is inside |
|---|---|
| `Models` | `Book`, `Member`, `IssueRecord` (these become the database tables) |
| `Data` | `LibraryContext` (EF Core database access) and `SeedData` (sample data) |
| `Controllers` | One controller per page group: Home, Books, Members, Issues |
| `Views` | Razor pages (`.cshtml`) for each controller, plus `Shared/_Layout` |
| `ViewModels` | Small classes that carry data to a page (dashboard, issue form) |
| `Program.cs` | App startup: services, database setup, routing |

## Ideas to extend it

- Login with ASP.NET Core Identity (librarian-only access)
- Switch to SQL Server: replace the Sqlite package and `UseSqlite` with `UseSqlServer`
- EF Core migrations instead of `EnsureCreated`
- Book copies count instead of a single available/issued flag
- Unit tests for the fine calculation
