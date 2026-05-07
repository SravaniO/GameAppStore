# GameStore

An ASP.NET Core web application for browsing and managing a game catalog, deployed to Azure App Service via GitHub Actions CI/CD.

## Tech Stack

- **Framework:** ASP.NET Core (targeting .NET 8.0)
- **Pattern:** MVC (Model-View-Controller)
- **Hosting:** Azure App Service (`GameStore20250410103506`)

## Project Structure

```
GameStore/
├── Controllers/
│   ├── GameController.cs     # Handles /Games routes; lists all games
│   └── HomeController.cs     # Handles home and contact pages
├── Models/                   # Data models (e.g. ErrorViewModel)
├── Services/
│   └── GameService.cs        # Business logic for retrieving game data
├── Views/                    # Razor view templates
└── GameStore.csproj          # Project file targeting net8.0
```

## Getting Started

### Prerequisites

- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)

### Run locally

```bash
git clone <your-repo-url>
cd GameStore
dotnet run
```

The app will be available at `https://localhost:5001` by default.

### Build for production

```bash
dotnet publish -c Release -o ./publish
```

## Deployment

The project uses **GitHub Actions** for automated CI/CD. On every push to `main`:

1. The app is built with `dotnet build` on Windows.
2. Published artifacts are uploaded.
3. The artifact is deployed to the Azure Web App using a publish profile stored as a GitHub secret (`AZUREAPPSERVICE_PUBLISHPROFILE_...`).

The workflow file is located at `.github/workflows/`.

## Environment & Secrets

| Secret | Description |
|---|---|
| `AZUREAPPSERVICE_PUBLISHPROFILE_D49E2C2321E942DD91426BFAAEDA612A` | Azure publish profile for the Production slot |

Store secrets in **GitHub → Settings → Secrets and variables → Actions**. Never commit them to the repository.

## Contributing

1. Fork the repository and create a feature branch.
2. Make your changes and ensure `dotnet build` passes.
3. Open a pull request targeting `main`.
