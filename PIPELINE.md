# 📊 Monitoramento do Pipeline GitHub Actions

## Acessar o Pipeline

1. Navegue para o repositório no GitHub
2. Clique na aba **"Actions"** no menu superior
3. Você verá todos os workflows executados

## Visualizar Detalhes de uma Execução

1. Clique no workflow "Code Validation"
2. Selecione a execução desejada (por branch ou data)
3. Você verá:
   - ✅ Status geral (Success/Failed)
   - 📈 Tempo de execução
   - 🐍 Versões Python testadas

## Artefatos Gerados

Após cada execução bem-sucedida, os relatórios estão disponíveis para download:

- `bandit-report.json`: Relatório detalhado de segurança
- `safety-report.json`: Relatório de vulnerabilidades de dependências

Para acessar:
1. Abra a execução do workflow
2. Role para baixo até **"Artifacts"**
3. Clique no artefato para baixar

## Badges de Status

Adicione a ação de badge ao seu README:

```markdown
[![Code Validation](https://github.com/SEU_USUARIO/SEU_REPO/actions/workflows/validate.yml/badge.svg)](https://github.com/SEU_USUARIO/SEU_REPO/actions/workflows/validate.yml)
```

## Integrando com Proteções de Branch

Para forçar que o pipeline passou antes de fazer merge:

1. Vá em **Settings** → **Branches**
2. Configure **Branch protection rules** para `main`
3. Ative "Require status checks to pass before merging"
4. Selecione "Code Validation" como check obrigatório

## Dicas de Troubleshooting

| Problema | Solução |
|----------|---------|
| Erro "Module not found" | Verifique se as dependências estão no pyproject.toml |
| Ruff falha em formatação | Execute `poetry run ruff format` localmente |
| Bandit reporta problema segurança | Configure exceções em `.bandit` se necessário |
| Safety encontra vulnerabilidades | Atualize as dependências: `poetry update` |

## Links Úteis

- [GitHub Actions Workflow Syntax](https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions)
- [Bandit Documentation](https://bandit.readthedocs.io/)
- [Safety Documentation](https://safetycli.com/)
- [Ruff Documentation](https://docs.astral.sh/ruff/)
