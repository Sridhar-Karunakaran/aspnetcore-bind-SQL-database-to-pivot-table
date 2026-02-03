# 📊 Bind SQL Database to a Syncfusion Pivot Table

> Quick-start samples demonstrating how to retrieve data from a SQL database via ASP.NET Web APIs and display it in a Syncfusion Pivot Table (PivotView).

---

## 📚 Table of Contents

- [🔍 Project Overview](#-project-overview)
- [🚀 Quick Start](#-quick-start)
- [✨ Key Features](#-key-features)
- [🛠️ Supported Platforms & Dependencies](#️-supported-platforms--dependencies)
- [🧭 Project Structure](#-project-structure)
- [🧩 Minimal Example (API + PivotView)](#-minimal-example-api--pivotview)
- [⚙️ Configuration & Environment](#️-configuration--environment)
- [🧪 Testing & CI](#-testing--ci)
- [🤝 Contributing](#-contributing)
- [📜 License & Support](#-license--support)

---

## 🔍 Project Overview

This repository provides quick-start server examples that expose SQL data via two API patterns:

- [ASP.NET Core API/](./ASP.NET%20Core%20API/) — modern ASP.NET Core Web API sample
- [ASP.NET Web API](./ASP.NET%20Web%20API/) — legacy ASP.NET Web API sample

Both controllers demonstrate fetching tabular data from a SQL database and returning JSON formatted rows suitable for binding to Syncfusion PivotView controls on the client.

Use cases:
- BI reporting dashboards
- Sales/financial data analysis
- Prototyping server-side data connectors for Syncfusion PivotView

---

## 🚀 Quick Start

Prerequisites
- .NET SDK (6.0+ recommended for ASP.NET Core sample)
- SQL Server (or compatible) instance with sample data
- Optional: Node.js + a front-end sample that consumes the API and renders PivotView

Run the ASP.NET Core API

```bash
cd "ASP.NET Core API"
dotnet restore
dotnet run
# Default URL and port shown in console (e.g. https://localhost:5001)
```

Run the classic ASP.NET Web API (Visual Studio recommended)

```powershell
# Open the solution in Visual Studio and run (IIS Express or project)
```

Run a front-end sample (choose one):

TypeScript
```bash
cd Typescript/pivot-table
npm install
npm start
```

Angular
```bash
cd Angular/pivot-table
npm install
npm start
```

React
```bash
cd React/pivot-table
npm install
npm start
```

Vue
```bash
cd VUE/pivot-table
npm install
npm run dev
```

First success: Use Swagger (if included) or browse to `https://localhost:<port>/api/pivot` (example) and confirm JSON rows are returned.

---

## ✨ Key Features

- Server examples for SQL → JSON API (ASP.NET Core and ASP.NET Web API)
- Clear pattern for binding backend query results to Syncfusion PivotView
- Minimal, copy-paste-ready controller code for common SQL queries
- Swagger/OpenAPI integration suggested for API discovery
- Cross-platform approach: front-end agnostic (works with Angular/React/Vue/Blazor)

Benefits:
- Faster prototyping of reporting features using existing SQL databases.
- Reusable API patterns that integrate with any Syncfusion PivotView client.

---

## 🛠️ Supported Platforms & Dependencies

- Primary languages: C# (API samples), JavaScript/HTML (client-side examples may be present)
- Typical server dependencies (check each project's .csproj): `Microsoft.AspNetCore.*`, `System.Data.SqlClient` or `Microsoft.Data.SqlClient`, `Swashbuckle.AspNetCore` (optional)
- System requirements: .NET SDK for server; SQL Server or compatible DB engine; browser for client.

---

## 🧭 Project Structure

- `ASP.NET Core API/` — .NET Core Web API sample, controller(s) to query SQL and return JSON
- `ASP.NET Web API/` — legacy Web API sample, controller(s) doing the same for older frameworks
- `.github/workflows/` — CI examples (if present)

Open entry points:
- API controllers located inside `ASP.NET Core API/Controllers/` or `ASP.NET Web API/Controllers/`

---

## 🧩 Minimal Example (API + PivotView)

Server: basic controller action (example)

```csharp
[HttpGet("api/pivotdata")]
public IActionResult Get()
{
		var rows = _dbContext.Database.SqlQuery("SELECT Country, Product, Amount FROM Sales");
		return Ok(rows);
}
```

Client: bind Syncfusion PivotView (vanilla JS example)

```html
<div id="PivotTable"></div>
<script>
fetch('/api/pivotdata')
	.then(res => res.json())
	.then(data => {
		var pivot = new ej.pivotview.PivotView({
			dataSourceSettings: { dataSource: data, rows:[{name:'Country'}], columns:[{name:'Product'}], values:[{name:'Amount'}] },
			height: 400
		});
		pivot.appendTo('#PivotTable');
	});
</script>
```

Note: adapt the API route and CORS policy as necessary when client and API run on different hosts.

---

## ⚙️ Configuration & Environment

- Connection string: set in `appsettings.json` or environment variable `ConnectionStrings__DefaultConnection`.

Example `appsettings.json` snippet:

```json
{
	"ConnectionStrings": {
		"DefaultConnection": "Server=localhost;Database=SampleDb;User Id=sa;Password=Your_password123;"
	}
}
```

- Enable CORS in `Program.cs` to allow front-end origins during development.

Troubleshooting
- Ensure SQL user has SELECT permissions on tables used by samples.
- If using `Microsoft.Data.SqlClient`, install the correct NuGet package and check platform compatibility.

---

## 🧪 Testing & CI

- Add GitHub Actions to build the .NET projects and run unit tests where applicable.
- Suggested CI workflow: `dotnet restore`, `dotnet build`, `dotnet test`, and (optional) deploy artifacts.

---

## 🤝 Contributing

Contributions welcome — please:

1. Fork and create a branch: `feature/<short-desc>`
2. Run the sample(s) locally and update docs
3. Open a PR and reference related issues

## 📜 License & Support

This is a **commercial product** subject to the Syncfusion End User License Agreement (EULA).

**Free Community License** is available for qualifying users/organizations:  
- Annual gross revenue < $1 million USD  
- 5 or fewer total developers  
- 10 or fewer total employees  

The community license allows free use in both internal and commercial applications under these conditions.  
No registration or approval is required — just comply with the terms.

**Paid Licenses** are required for:  
- Larger organizations  
- Teams exceeding the community license limits  
- Priority support, custom patches, or on-premise deployment options  

Purchase options and pricing: https://www.syncfusion.com/sales/products  
30-day free trial (full features, no credit card required): https://www.syncfusion.com/downloads/essential-js2  
Community License details & FAQ: https://www.syncfusion.com/products/communitylicense  
Full EULA: https://www.syncfusion.com/eula/es/

© 2026 Syncfusion, Inc. All Rights Reserved.