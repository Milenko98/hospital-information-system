# Hospital Information System – Databases (Bachelor thesis)

Bachelor thesis project at the **Faculty of Technical Sciences, Novi Sad** (Applied Software Engineering), 2021.
A relational database for managing a hospital – patients, staff, examinations, diagnoses, therapies and prescriptions – together with a desktop application built on top of it.

![ER diagram](Documents/Bolnica_ER_Dijagram.png)

## Highlights

- **Database design** – ER model with 22 tables, including an inheritance hierarchy for people
  (`Person` → `Doctor`, `Patient`, `Receptionist`, `Worker`, `Security`) mapped with table-per-type.
- **Model-first Entity Framework** – the schema is generated from the EDMX model
  ([`Model1.edmx.sql`](Bolnica/Servis/Baza/Model1.edmx.sql)).
- **T-SQL programmability**
  - stored procedure with a cursor that looks up a patient's medical record by ID and place of residence ([`Procedura.txt`](Procedura.txt))
  - scalar function returning the doctor who performed an examination ([`Funkcija.txt`](Funkcija.txt))
  - `AFTER INSERT` triggers on hospitals and places ([`InsertBolnicaTriger.txt`](InsertBolnicaTriger.txt), [`InsertMesto.txt`](InsertMesto.txt))
- **Desktop application (WPF, MVVM)** – forms for adding every entity and a screen for executing the stored procedure.
- **Layered architecture** – a service layer (interfaces + implementations per entity) separates the UI from data access.

Full specification (in Serbian): [`Documents/Specifikacija Baze podata2 .pdf`](Documents/).

## Tech stack

C# · .NET Framework 4.6.1 · WPF (MVVM) · Entity Framework 6 · Microsoft SQL Server · T-SQL

## Project structure

```
Bolnica/
├── Servis/              # data layer: EF model (EDMX), entity classes, service interfaces & implementations
└── UI/                  # WPF application: Views (XAML) + ViewModels
Documents/               # ER diagram and project specification
*.txt                    # T-SQL procedure, function and triggers
```

## Running locally

1. Open `Bolnica/Bolnica.sln` in Visual Studio.
2. Create the database by running `Bolnica/Servis/Baza/Model1.edmx.sql` on a SQL Server (Express) instance.
3. Update the `Model1Container` connection string in `App.config` (both projects) to point to your server.
4. Restore NuGet packages, set **UI** as the startup project and run.
