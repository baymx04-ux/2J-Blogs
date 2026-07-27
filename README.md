# 2J-Blogs

A full-featured blog publishing platform built with **Blazor Server** and **.NET 7.0**, connected to a **SQL Server** database. Users can register, log in, create and manage blog posts, leave comments, and submit contact messages.

## Features

- **User Registration & Authentication** -- Sign up with username, email, and password; log in to access the dashboard.
- **Blog Management** -- Create, view, and delete blog posts from a personal dashboard.
- **My Blogs** -- View a filtered list of all blogs authored by the current user.
- **Blog Detail View** -- Read full blog content with author information.
- **Comments** -- Submit and read comments on individual blog posts.
- **Contact Form** -- Send messages (name, email, message) stored in the database.
- **About Page** -- Static informational page about the project and its creators.

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Blazor Server (.NET 7.0) |
| Language | C# |
| Database | SQL Server (SQL Express) |
| Data Access | Raw ADO.NET (`SqlConnection` / `SqlCommand`) |
| UI Styling | Bootstrap 5, Bootstrap Icons, AOS (Animate On Scroll), Swiper, GLightbox |
| Template Base | [ZenBlog](https://bootstrapmade.com/) BootstrapMade template |

## Project Structure

```
BlogSite/
├── Pages/
│   ├── Signin.razor          # Login page (landing page)
│   ├── SignUp.razor          # User registration
│   ├── Index.razor           # Authenticated home / blog listing
│   ├── Blogs.razor           # Single blog detail + comments
│   ├── MyBlogs.razor         # Current user's blog list
│   ├── About.razor           # About page
│   ├── Contact.razor         # Contact form
│   ├── SubmitForm.razor      # Blog creation dashboard
│   ├── RemoveBlog.razor      # Blog deletion dashboard
│   ├── Home.razor            # Legacy/unused static home prototype
│   └── Error.razor           # Error / unauthorized page
├── Shared/
│   ├── MainLayout.razor      # Default layout with background image + footer
│   ├── NoMenuLayout.razor    # Minimal layout for auth/dashboard pages
│   ├── Header.razor          # Empty (navbar duplicated per page)
│   └── Footer.razor          # Footer with author credits
├── Models/
│   ├── UserModel.cs          # User entity (UserId, Username, Email, Password)
│   ├── BlogModel.cs          # Blog entity (BlogId, Title, Content, UserId, SubmittedBy)
│   ├── CommentModel.cs       # Comment entity (CommentId, BlogId, UserId, CommentContent, Author)
│   └── ContactMessageModel.cs # Contact message entity
├── Data/
│   ├── UserService.cs        # User registration, authentication, and lookup
│   ├── BlogService.cs        # Blog CRUD operations
│   ├── CommentService.cs     # Comment submission and retrieval
│   ├── ContactMessageService.cs # Contact message submission
│   └── UserState.cs          # Simple authentication state holder
├── wwwroot/
│   ├── css/                  # Site-wide CSS
│   ├── images/               # Background and card images
│   └── assets/               # Vendor libraries (Bootstrap, Swiper, AOS, etc.)
├── Program.cs                # Application entry point and service registration
├── appsettings.json          # SQL Server connection string configuration
└── BlogSite.csproj           # Project file targeting net7.0
```

## Database Schema

The application uses four tables in a SQL Server database named `BlogSite`:

| Table | Columns |
|---|---|
| **Users** | UserId (PK), Username, Email, Password |
| **Blogs** | BlogId (PK), Title, Content, UserId (FK), SubmittedBy |
| **Comments** | CommentId (PK), BlogId (FK), UserId (FK), CommentContent, Author |
| **ContactMessages** | ContactMessageId (PK), Name, Email, Message, CreatedAt |

## Getting Started

### Prerequisites

- [.NET 7.0 SDK](https://dotnet.microsoft.com/download/dotnet/7.0)
- [SQL Server](https://www.microsoft.com/en-us/sql-server) or SQL Server Express
- An IDE such as Visual Studio 2022 or VS Code

### Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/baymx04-ux/2J-Blogs.git
   cd 2J-Blogs/BlogSite_Blazor-master/BlogSite
   ```

2. **Create the database:**
   Open SQL Server Management Studio and create a database named `BlogSite`. Create the four tables (`Users`, `Blogs`, `Comments`, `ContactMessages`) matching the schema described above.

3. **Update the connection string:**
   Edit `appsettings.json` and update the `DefaultConnection` string to point to your SQL Server instance:
   ```json
   "ConnectionStrings": {
     "DefaultConnection": "Data Source=YOUR_SERVER;Initial Catalog=BlogSite;Integrated Security=True"
   }
   ```

4. **Run the application:**
   ```bash
   dotnet run
   ```
   The application will start and be available at `https://localhost:5001` or `http://localhost:5000`.

## Pages

| Page | Route | Description |
|---|---|---|
| Login | `/` | Email and password authentication form |
| Sign Up | `/signup` | New user registration form |
| Home | `/Home/{username}` | Blog listing dashboard with all posts |
| Blog Detail | `/blog/{blogId}/{username}` | Full blog view with comments |
| My Blogs | `/myblogs/{username}` | List of the current user's blogs |
| Dashboard | `/dashboard/{username}` | Create new blog posts |
| Remove Blogs | `/removeblogs/{username}` | Delete existing blog posts |
| About | `/about/{username}` | Information about the project |
| Contact | `/contact/{username}` | Contact form submission |
| Error | `/error` | Unauthorized / error page |

## Authors

- **Kanwar Junaid Islam**
- **Muhammad Jasim Ibrahim Malik**

Built as a project at Air University.

## License

This project is for educational purposes.
