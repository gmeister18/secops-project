# SecOps Project

Projeto de operações de segurança com validações automáticas via GitHub Actions.

## 📋 Visão Geral

Este projeto implementa um pipeline de CI/CD com GitHub Actions para automação de validações de código incluindo:

- **Bandit**: Análise de segurança Python
- **Safety**: Verificação de dependências com vulnerabilidades conhecidas
- **Ruff**: Linting e formatação de código

## 🚀 Como Usar

### Pré-requisitos

- Python >= 3.10
- Poetry

### Instalação Local

```bash
# Instalar dependências
poetry install --with dev

# Executar todas as validações
poetry run bandit -r src/ main.py
poetry run safety check
poetry run ruff check src/ main.py tests/
poetry run ruff format src/ main.py tests/
```

## 🔒 GitHub Actions Pipeline

O pipeline é acionado automaticamente em:
- Push para `main` ou `develop`
- Pull Requests para `main` ou `develop`

### Ferramentas de Validação

#### Bandit (Segurança)
Realiza auditoria de segurança estática no código Python.

```bash
poetry run bandit -r src/ main.py
```

#### Safety (Dependências)
Verifica vulnerabilidades conhecidas em dependências.

```bash
poetry run safety check
```

#### Ruff (Linting & Formatação)
Valida qualidade do código e conformidade com padrões.

```bash
# Verificar
poetry run ruff check src/ main.py tests/

# Formatar automaticamente
poetry run ruff format src/ main.py tests/
```

## 📊 Relatórios

Os relatórios de validação são salvos como artefatos no GitHub Actions:
- `bandit-report.json`: Relatório de segurança em JSON
- `safety-report.json`: Relatório de dependências em JSON

## ✅ Status do Pipeline

O badge abaixo mostra o status atual:

[![Code Validation](https://github.com/[USERNAME]/[REPO]/actions/workflows/validate.yml/badge.svg)](https://github.com/[USERNAME]/[REPO]/actions/workflows/validate.yml)

## 🔧 Configuração

- **ruff.toml**: Configurações do Ruff
- **.bandit**: Configurações do Bandit
- **pyproject.toml**: Configurações gerais e dependências

## 📝 Boas Práticas

1. Sempre executar validações localmente antes de fazer push
2. Manter as dependências atualizadas
3. Responder a alertas de segurança prontamente
4. Formatar o código antes de commitar: `poetry run ruff format`

## 📞 Contato

- Desenvolvimento: [gmeister18](https://github.com/gmeister18)
