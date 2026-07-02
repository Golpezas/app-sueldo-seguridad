# AppSueldo — AGENTS.md

## App

Single-file Flet web app (`main.py`, 281 LOC). Argentine salary calculator based on UPSRA CCT 507/07 collective bargaining agreement (Vigilador General category, Jan–Jun 2026 scales).

- **Run**: `venv\Scripts\Activate.ps1` then `python main.py` — open browser at `http://localhost:8000`
- **Entrypoint**: `main.py` -> `ft.run(main=main, view=ft.AppView.WEB_BROWSER, port=..., host="0.0.0.0")`
- **PORT**: overridable via env var `PORT` (default 8000)
- **host**: `0.0.0.0` required for Render port detection; access locally via `localhost`, NOT `0.0.0.0` in the browser

## Architecture

Three layers in one file — no packages, no modules:

| Layer | Class / Location | Purpose |
|---|---|---|
| Data (`main.py:11-21`) | `ConfiguracionMes`, `EscalaSalarial` | Pydantic models |
| Business (`main.py:26-127`) | `MotorJornadaAutomatica` | Engine: scales, holidays (Argentina), seniority, pay calculation |
| UI (`main.py:132-277`) | Flet UI | Dark-mode form, dropdowns, auto-fill hours, results panel |

## Salaries

Scales are **hardcoded** in `MotorJornadaAutomatica.historico_escalas` (Jan–Jun 2026). Adding months requires editing that dict. Reference scales are in `txt/UPSRA Convenio de salarios.txt`.

## Dependencies

- `venv/` is gitignored; first-time setup: `python -m venv venv` then `pip install -r requirements.txt` (uses only pip)
- Key deps: `flet==0.84.0`, `pydantic==2.13.3`, `holidays==0.95`

## Tests / Lint / CI

None. No test framework, no linter config, no CI workflows. If introducing tests, no conventions to follow — start fresh.

## Conventions

- Spanish identifiers and comments throughout
- A backup copy of `main.py` lives at `txt/main.py.txt` — edit `main.py`, not the backup
