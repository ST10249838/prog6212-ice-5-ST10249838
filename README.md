# BasicMovie 🎬

A cinema management web application built with **ASP.NET Core MVC** and **.NET 8**. Manage movies, showtimes, and ticket bookings through an intuitive Bootstrap-powered interface.

## Table of Contents

- [Overview](#overview)
- [Tech Stack](#tech-stack)
- [Features](#features)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Running the Application](#running-the-application)
- [Routes & Pages](#routes--pages)
- [Data Models](#data-models)
- [Configuration](#configuration)

## Overview

BasicMovie is a lightweight cinema-style web application that allows users to manage a catalog of movies, schedule showtimes with seat availability, and handle ticket bookings. All data is stored in-memory, making it ideal for demonstration and educational purposes without requiring any database setup.

## Tech Stack

| Layer         | Technology                                                     |
| ------------- | -------------------------------------------------------------- |
| **Runtime**   | [.NET 8](https://dotnet.microsoft.com/) (C#)                   |
| **Framework** | ASP.NET Core MVC                                               |
| **Views**     | Razor (`.cshtml`)                                              |
| **CSS**       | [Bootstrap](https://getbootstrap.com/)                         |
| **JS**        | [jQuery](https://jquery.com/), jQuery Validation (unobtrusive) |
| **Storage**   | In-memory (static lists — no database required)                |

## Features

- **Movie Management:** Create, view, edit, and delete movies with title, genre, and duration.
- **Showtime Scheduling:** Define showtimes linked to movies, including date/time and available seat count.
- **Ticket CRUD:** Standard create, read, update, and delete operations for tickets.
- **Seat-Aware Booking:** A dedicated booking flow that validates seat availability and decrements available seats on confirmation.
- **Client-Side Validation:** Model-driven validation with jQuery unobtrusive validation for immediate user feedback.
- **Responsive UI:** Bootstrap-based layout that works across desktop and mobile browsers.

## Project Structure

```text
BasicMovie/
├── prog6212-ice-5-ST10249838/
│   ├── Controllers/
│   │   ├── HomeController.cs        # Home, Privacy, Error pages
│   │   ├── MovieController.cs       # Movie CRUD operations
│   │   ├── ShowtimeController.cs    # Showtime CRUD operations
│   │   └── TicketController.cs      # Ticket CRUD + booking flow
│   ├── Models/
│   │   ├── MovieModel.cs            # Title, Genre, Duration
│   │   ├── ShowtimeModel.cs         # MovieId, Showtime, AvailableSeats
│   │   ├── TicketModel.cs           # ShowtimeId, CustomerName, NumberOfTickets
│   │   └── ErrorViewModel.cs
│   ├── Views/
│   │   ├── Home/                    # Index, Privacy
│   │   ├── Movie/                   # Index, Create, Edit, Delete
│   │   ├── Showtime/                # Index, Create, Edit, Delete
│   │   ├── Ticket/                  # Index, Create, Edit, Delete, Book, Confirmation
│   │   └── Shared/                  # _Layout, Error, validation partials
│   ├── wwwroot/
│   │   ├── css/site.css
│   │   ├── js/site.js
│   │   └── lib/                     # Bootstrap, jQuery, jQuery Validation
│   ├── Properties/
│   │   └── launchSettings.json
│   ├── Program.cs                   # App entry point & middleware pipeline
│   ├── appsettings.json
│   ├── appsettings.Development.json
│   └── prog6212-ice-5-ST10249838.sln
├── .gitignore
├── .gitattributes
└── README.md
```

## Getting Started

### Prerequisites

- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0) (or later)

### Running the Application

1. **Clone the repository**

   ```bash
   git clone https://github.com/<your-username>/BasicMovie.git
   cd BasicMovie/prog6212-ice-5-ST10249838
   ```

2. **Build the project**

   ```bash
   dotnet build
   ```

3. **Run the application**

   ```bash
   dotnet run
   ```

4. **Open in your browser**

   | Profile | URL                      |
   | ------- | ------------------------ |
   | HTTP    | <http://localhost:5062>  |
   | HTTPS   | <https://localhost:7267> |

> **Tip:** You can also open the `.sln` file in Visual Studio and press **F5** to launch with IIS Express.

## Routes & Pages

The app uses ASP.NET Core conventional routing (`{controller=Home}/{action=Index}/{id?}`).

| Controller   | Action       | Method   | URL Example              | Description                 |
| ------------ | ------------ | -------- | ------------------------ | --------------------------- |
| **Home**     | Index        | GET      | `/`                      | Landing page                |
| **Home**     | Privacy      | GET      | `/Home/Privacy`          | Privacy policy              |
| **Movie**    | Index        | GET      | `/Movie`                 | List all movies             |
| **Movie**    | Create       | GET/POST | `/Movie/Create`          | Add a new movie             |
| **Movie**    | Edit         | GET/POST | `/Movie/Edit/12345`      | Edit an existing movie      |
| **Movie**    | Delete       | GET/POST | `/Movie/Delete/12345`    | Delete a movie              |
| **Showtime** | Index        | GET      | `/Showtime`              | List all showtimes          |
| **Showtime** | Create       | GET/POST | `/Showtime/Create`       | Add a new showtime          |
| **Showtime** | Edit         | GET/POST | `/Showtime/Edit/12345`   | Edit an existing showtime   |
| **Showtime** | Delete       | GET/POST | `/Showtime/Delete/12345` | Delete a showtime           |
| **Ticket**   | Index        | GET      | `/Ticket`                | List all tickets            |
| **Ticket**   | Create       | GET/POST | `/Ticket/Create`         | Create a ticket manually    |
| **Ticket**   | Edit         | GET/POST | `/Ticket/Edit/12345`     | Edit an existing ticket     |
| **Ticket**   | Delete       | GET/POST | `/Ticket/Delete/12345`   | Delete a ticket             |
| **Ticket**   | Book         | GET/POST | `/Ticket/Book`           | Book tickets for a showtime |
| **Ticket**   | Confirmation | GET      | `/Ticket/Confirmation`   | Booking confirmation page   |

## Data Models

### MovieModel

| Property   | Type     | Validation              |
| ---------- | -------- | ----------------------- |
| `Id`       | `int`    | Auto-generated          |
| `Title`    | `string` | Required, max 100 chars |
| `Genre`    | `string` | —                       |
| `Duration` | `int`    | Range: 30–300 minutes   |

### ShowtimeModel

| Property         | Type       | Validation     |
| ---------------- | ---------- | -------------- |
| `Id`             | `int`      | Auto-generated |
| `MovieId`        | `int`      | Required       |
| `Showtime`       | `DateTime` | —              |
| `AvailableSeats` | `int`      | Range: 1–100   |

### TicketModel

| Property          | Type     | Validation     |
| ----------------- | -------- | -------------- |
| `Id`              | `int`    | Auto-generated |
| `ShowtimeId`      | `int`    | —              |
| `CustomerName`    | `string` | —              |
| `NumberOfTickets` | `int`    | Range: 1–10    |

> **Note:** All data is stored in-memory using static lists on each controller. Data resets when the application restarts.

## Configuration

Configuration files live in the project root:

- **`appsettings.json`:** Base logging levels and allowed hosts.
- **`appsettings.Development.json`:** Development-specific logging overrides.
- **`Properties/launchSettings.json`:** Launch profiles, URLs, and environment variables.

The only environment variable used is `ASPNETCORE_ENVIRONMENT` (set to `Development` by default in launch profiles). No connection strings or secrets are required.
