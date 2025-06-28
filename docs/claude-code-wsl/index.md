---
layout: default
title: Claude Code no WSL
parent: Guias de Desenvolvimento
nav_order: 1
---

# Claude Code no WSL

Este guia aborda como configurar e usar o Claude Code no Windows Subsystem for Linux (WSL).

## Pré-requisitos

- Windows 10/11 com WSL2 instalado
- Distribuição Linux no WSL (Ubuntu recomendado)
- Node.js instalado no WSL

## Instalação

### 1. Configurar o WSL

```bash
# Verificar versão do WSL
wsl --version

# Listar distribuições instaladas
wsl -l -v
```

### 2. Instalar Claude Code

```bash
# Instalar via npm
npm install -g @anthropic/claude-code

# Verificar instalação
claude-code --version
```

## Configuração

### Autenticação

```bash
# Configurar API key
claude-code auth login
```

### Configuração do ambiente

```bash
# Configurar editor padrão
export EDITOR=nano

# Configurar diretório de projetos
cd ~/projetos
```

## Uso Básico

### Comandos essenciais

```bash
# Iniciar sessão interativa
claude-code

# Executar comando específico
claude-code "criar um arquivo README.md"

# Usar com arquivo específico
claude-code --file src/app.js "adicionar comentários JSDoc"
```

## Dicas e Truques

### Integração com VS Code

- Usar extensões do WSL
- Configurar terminal integrado
- Sincronização de configurações

### Performance

- Usar arquivos no sistema de arquivos do WSL
- Evitar cross-filesystem operations
- Configurar Git no WSL

## Solução de Problemas

### Problemas comuns

1. **Erro de permissão**: `chmod +x script.sh`
2. **Node.js não encontrado**: Reinstalar Node.js via nvm
3. **Conexão de rede**: Verificar configurações de proxy

### Logs e debug

```bash
# Verificar logs
claude-code --debug

# Limpar cache
claude-code cache clear
```

## Recursos Adicionais

- [Documentação oficial do Claude Code](https://docs.anthropic.com/claude-code)
- [Guia do WSL](https://docs.microsoft.com/en-us/windows/wsl/)
- [Configuração do Node.js no WSL](https://docs.microsoft.com/en-us/windows/dev-environment/javascript/nodejs-on-wsl)