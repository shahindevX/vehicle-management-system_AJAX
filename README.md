# Vehicle Management System

A **vehicle management web app** built with **ASP.NET MVC 5 (.NET Framework 4.8)** and **Entity Framework 6 (Code First)**. It keeps a register of vehicles with their type, owner contact, purchase date, photo and service history. Vehicles are created and edited in modal dialogs that save over AJAX, so the list never needs a full page reload.

## Features

- **Vehicle register** – name, registration number, purchase date, owner mobile number and active status
- **Vehicle types** – full CRUD (Sedan, SUV, Truck and Motorcycle are seeded automatically)
- **Service records** – attach any number of service entries (service name and cost) to a vehicle, and add or remove them while editing
- **Photo upload** – each vehicle can have a picture (saved with a unique GUID name, with `novehicle.png` as the default)
- **AJAX modals** – create, edit and delete vehicles through jQuery and Bootstrap modals
- **Validation** – data annotations on a dedicated `VehicleViewModel`, plus anti-forgery tokens on create and edit
- **Auto-created database** – the schema and seed data are created on first run through `MigrateDatabaseToLatestVersion`

## Tech Stack

| Layer | Technology |
| --- | --- |
| Framework | ASP.NET MVC 5.2, .NET Framework 4.8 |
| Language | C# |
| ORM | Entity Framework 6.4 (Code First) |
| Database | SQL Server LocalDB |
| Front end | Razor views, Bootstrap 5.3, jQuery 3.7 |

## Data Model

```
VehicleType 1 ──< Vehicle 1 ──< ServiceRecord
```

| Entity | Main fields |
| --- | --- |
| `VehicleType` | `VehicleTypeId`, `TypeName` |
| `Vehicle` | `VehicleId`, `VehicleName`, `RegistrationNumber`, `PurchaseDate`, `OwnerMobileNo`, `IsActive`, `ImageUrl`, `VehicleTypeId` (FK) |
| `ServiceRecord` | `ServiceRecordId`, `ServiceName`, `Cost`, `VehicleId` (FK) |

## Project Structure

```
VehicleManagementSystem/
├── Controllers/      # Home, Vehicles, VehicleTypes
├── Models/           # Vehicle, VehicleType, ServiceRecord
├── ViewModels/       # VehicleViewModel (form binding and validation)
├── DAL/              # AppDbContext
├── Migrations/       # Configuration with seed data
├── Views/            # Razor views and shared partials (create / edit modals)
├── Content/ Scripts/ # Bootstrap and jQuery
└── images/           # Uploaded vehicle photos and the default image
```

## Getting Started

### Prerequisites

- Windows with **Visual Studio 2019 / 2022** (ASP.NET and web development workload)
- **.NET Framework 4.8** developer pack
- **SQL Server LocalDB** (installed with Visual Studio)

### Run locally

1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/<your-repo>.git
   ```
2. Open `VehicleManagementSystem.sln` in Visual Studio.
3. Build the solution. NuGet packages are restored automatically from `packages.config`.
4. Press **F5**. On first start, the `VehicleManagementDB` database is created and the vehicle types are seeded, so no manual migration step is needed.

### Database connection

The connection string is in `Web.config` and points to LocalDB:

```xml
<add name="AppDbContext"
     connectionString="server=(LocalDB)\MSSQLLocalDB; database=VehicleManagementDB; Trusted_Connection=true"
     providerName="System.Data.SqlClient" />
```

Change the server name if you use a full SQL Server instance.

## Routes

| Route | Description |
| --- | --- |
| `/` | Home page |
| `/Vehicles` | Vehicle list with modal create, edit and delete |
| `/VehicleTypes` | Manage vehicle types (list, details, create, edit, delete) |

## Possible Improvements

- Add authentication and roles
- Search, filter and paging on the vehicle list
- Show the total service cost per vehicle
- Validate uploaded file type and size
- Replace automatic migrations with explicit, versioned migrations
- Migrate to ASP.NET Core

## License

Add a license of your choice (for example MIT), or remove this section.
