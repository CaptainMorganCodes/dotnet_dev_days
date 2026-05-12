# Copilot Workspace Instructions

## ? MANDATORY PRE-COMMIT CHECKLIST

- [ ] dotnet build SocOps/SocOps.csproj passes
- [ ] Code follows C# conventions (PascalCase public, _camelCase private)
- [ ] Razor components use proper event binding (@onclick, @onchange)
- [ ] No unused imports or variables
- [ ] CSS utilities from app.css (no inline styles)

## Project Overview

**SocOps** — Social Bingo game built with Blazor WebAssembly (.NET 10). Players match questions to mark bingo squares and achieve 5-in-a-row to win.

## Architecture at a Glance

- **Components/** — Reusable UI (BingoBoard, BingoSquare, GameScreen, StartScreen)
- **Models/** — BingoSquareData, GameState, BingoLine
- **Services/** — BingoGameService (state + events), BingoLogicService (win logic)
- **Data/** — Questions.cs (game content)
- **wwwroot/css/app.css** — Custom utility classes (no framework)

## Key Commands

`ash
dotnet build SocOps/SocOps.csproj              # Build
dotnet run --project SocOps                    # Dev server (localhost:5166)
dotnet clean SocOps/SocOps.csproj              # Clean
`

## C# Conventions

| Category | Style | Example |
|----------|-------|---------|
| Classes/Methods | PascalCase | BingoGameService |
| Private fields | _camelCase | _gameService |
| Public properties | PascalCase | GameState |
| Components | :ComponentBase | public class BingoBoard : ComponentBase |

## Styling

- Use utility classes from pp.css (layout, spacing, colors, typography)
- Scoped styles in .razor.css files alongside components
- CSS variables for theme colors

## State Management

- BingoGameService manages GameState and fires OnStateChanged event
- Components subscribe for reactivity
- State persisted to localStorage via JSInterop

## Component Patterns

`csharp
// Parameters
[Parameter] public string PlayerName { get; set; }

// Event handling
@onclick="() => ToggleSquare(index)"
@bind="playerName" @onchange="HandleChange"

// Reactive subscriptions
protected override async Task OnInitializedAsync()
{
    _gameService.OnStateChanged += StateHasChanged;
}
`

## Common Tasks

- **Add Question** ? Edit Data/Questions.cs
- **Style Component** ? Create ComponentName.razor.css
- **Game Logic** ? Edit Services/BingoLogicService.cs
- **State Changes** ? Use BingoGameService methods

## Testing

1. Run dotnet run --project SocOps
2. Navigate to http://localhost:5166
3. Browser console (F12) shows errors
4. Dev server auto-recompiles on file changes

## Resources

- [Blazor Docs](https://learn.microsoft.com/blazor)
- [ASP.NET Core](https://learn.microsoft.com/aspnet/core)
- [.NET 10](https://learn.microsoft.com/dotnet/core/whats-new/dotnet-10)
- Workshop guides in workshop/ (EN, ES, PT-BR)
