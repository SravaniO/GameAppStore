# GameStore

An ASP.NET Core web application for browsing and managing a game catalog, deployed to Azure App Service via GitHub Actions CI/CD.

## Tech Stack

- **Framework:** ASP.NET Core (.NET 8.0)
- **Pattern:** MVC (Model-View-Controller)
- **Hosting:** Azure App Service (`GameStore20250410103506`, Sweden Central)
- **Auth for deployment:** Azure Managed Identity (OIDC) via GitHub Actions

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
git clone https://github.com/SravaniO/GameAppStore.git
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
2. Artifacts are published and uploaded.
3. The workflow authenticates to Azure using **OIDC (OpenID Connect)** via a User-assigned Managed Identity.
4. The artifact is deployed to the Azure Web App.

The workflow file is located at `.github/workflows/main_gamestore20250410103506.yml`.

## Azure Setup

| Resource | Name |
|---|---|
| App Service | `GameStore20250410103506` |
| Resource Group | `GameStore20250410103506_group` |
| Region | Sweden Central |
| Managed Identity | `oidc-msi-8619` |

The Managed Identity has a **federated credential** configured for:
- **Entity type:** Environment
- **Environment name:** `Production`
- **Repository:** `SravaniO/GameAppStore`

## GitHub Secrets

These secrets must be set under **Settings → Secrets and variables → Actions**:

| Secret | Description |
|---|---|
| `AZUREAPPSERVICE_CLIENTID` | Client ID of the `oidc-msi-8619` Managed Identity |
| `AZUREAPPSERVICE_TENANTID` | Tenant ID from Microsoft Entra ID |
| `AZUREAPPSERVICE_SUBSCRIPTIONID` | Azure Subscription ID |

Never commit secret values to the repository.

## Contributing

1. Fork the repository and create a feature branch.
2. Make your changes and ensure `dotnet build` passes.
3. Open a pull request targeting `main`.
