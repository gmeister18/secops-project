# 🛠️ Guia de Comandos - Validações de Código

## Instalação

```bash
# Instalar todas as dependências (incluindo dev)
poetry install --with dev
```

## Execução Individual

### 1. Bandit (Análise de Segurança)
```bash
# Executar auditoria de segurança
poetry run bandit -r src/ main.py

# Gerar relatório JSON
poetry run bandit -r src/ main.py -f json -o bandit-report.json

# Com nível de severidade
poetry run bandit -r src/ main.py -ll
```

### 2. Safety (Verificação de Dependências)
```bash
# Verificar vulnerabilidades
poetry run safety check

# Gerar relatório JSON
poetry run safety check --json --output safety-report.json

# Modo vulnerabilidades críticas
poetry run safety check --continue-on-error
```

### 3. Ruff (Linting & Formatação)
```bash
# Verificar estilo de código
poetry run ruff check src/ main.py tests/

# Formatar código automaticamente
poetry run ruff format src/ main.py tests/

# Verificar formatação sem formatar
poetry run ruff format --check src/ main.py tests/
```

## Scripts Úteis

### Executar Todas as Validações
```bash
#!/bin/bash
echo "🔐 Executando Bandit..."
poetry run bandit -r src/ main.py

echo "⚠️ Executando Safety..."
poetry run safety check

echo "📝 Validando com Ruff..."
poetry run ruff check src/ main.py tests/

echo "✨ Formatando com Ruff..."
poetry run ruff format src/ main.py tests/

echo "✅ Todas as validações completadas!"
```

### Windows (PowerShell)
```powershell
Write-Host "🔐 Executando Bandit..." -ForegroundColor Blue
poetry run bandit -r src/ main.py

Write-Host "⚠️ Executando Safety..." -ForegroundColor Yellow
poetry run safety check

Write-Host "📝 Validando com Ruff..." -ForegroundColor Green
poetry run ruff check src/ main.py tests/

Write-Host "✨ Formatando com Ruff..." -ForegroundColor Cyan
poetry run ruff format src/ main.py tests/

Write-Host "✅ Todas as validações completadas!" -ForegroundColor Green
```

## Pré-commit Hook (Opcional)

Crie `.git/hooks/pre-commit`:

```bash
#!/bin/bash
poetry run ruff format src/ main.py tests/
poetry run ruff check src/ main.py tests/
poetry run bandit -r src/ main.py
```

Para ativar:
```bash
chmod +x .git/hooks/pre-commit
```

## Configurações Base

| Ferramenta | Arquivo | Configuração |
|-----------|---------|--------------|
| Bandit | `.bandit` | Diretórios e testes |
| Ruff | `ruff.toml` | Regras e linha de código |
| Safety | `pyproject.toml` | Dependências a ignorar |

## Troubleshooting

### Ruff recusa formatar?
```bash
poetry run ruff check --fix src/ main.py tests/
```

### Bandit muito restritivo?
Adicione exceções em `.bandit`:
```json
{
  "exclude": [".git", ".venv"],
  "tests": false,
  "skips": ["B101"]
}
```

### Safety com erro de conectividade?
```bash
poetry run safety check --offline
```

## CI/CD Automatizado

O GitHub Actions executa automaticamente:
- Em todo push para `main` ou `develop`
- Em todo pull request para `main` ou `develop`
- Em 3 versões Python (3.10, 3.11, 3.12)
- Gera artefatos com relatórios

Acesse: `https://github.com/[USERNAME]/[REPO]/actions`
