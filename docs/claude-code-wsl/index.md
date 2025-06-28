---
layout: default
title: Claude Code no WSL
parent: Guias de Desenvolvimento
nav_order: 1
description: "Guia completo para configurar Claude Code no WSL com integração IntelliJ"
tags: [wsl, claude, ai, intellij, windows, linux, desenvolvimento, plugin, anthropic, nodejs, npm, nvm, shell, bash, ssh, authentication, wrapper-script, troubleshooting]
keywords: "Claude Code, WSL, Windows Subsystem Linux, IntelliJ, AI, plugin, desenvolvimento"
canonical_url: "https://varantes.github.io/dev-guides/docs/claude-code-wsl/"
author: "Valdemar Arantes Neto"
date: 2025-06-28
last_modified_at: 2025-06-28
---

# Claude Code no WSL com Plugin IntelliJ

![WSL](https://img.shields.io/badge/WSL-0078D7?style=flat&logo=windows&logoColor=white)
![Claude](https://img.shields.io/badge/Claude-FF6B35?style=flat&logo=anthropic&logoColor=white)
![AI](https://img.shields.io/badge/AI-4285F4?style=flat&logo=google&logoColor=white)
![IntelliJ](https://img.shields.io/badge/IntelliJ-000000?style=flat&logo=intellijidea&logoColor=white)

> **Resumo**: Este guia resolve o problema de integrar Claude Code (ferramenta AI da Anthropic) com IntelliJ IDEA no Windows usando WSL (Windows Subsystem for Linux). Claude Code não roda nativamente no Windows, então usamos WSL + script wrapper para fazer a integração funcionar.

## Passos Rápidos

### 1. Instalar Claude Code no WSL
```bash
# No terminal WSL
npm install -g @anthropic-ai/claude-code
```

### 2. Autenticar
```bash
# No WSL
claude
# Seguir login no browser
```

### 3. Criar Script Wrapper
```bash
# No WSL
nano ~/claude-wrapper.sh
```

Conteúdo do script (ajuste os caminhos para seu ambiente):
```bash
#!/bin/bash
source ~/.bashrc
# Ajuste o caminho para sua versão do Node.js
/home/$(whoami)/.nvm/versions/node/v22.14.0/bin/node /home/$(whoami)/.nvm/versions/node/v22.14.0/bin/claude "$@"
```

**Alternativa genérica (recomendada):**
```bash
#!/bin/bash
source ~/.bashrc
# Usa a versão atual do NVM
claude "$@"
```

```bash
chmod +x ~/claude-wrapper.sh
```

### 4. Configurar Plugin IntelliJ
- Settings → Tools → Claude Code
- Executable Path: `wsl ~/claude-wrapper.sh`
- Clicar no ícone Claude Code na barra superior

## Detalhes Técnicos

### Limitações do Claude Code
- **Não suporta Windows nativamente**: Requer ambiente Unix-like
- **Sistemas suportados**: macOS, Linux, WSL
- **Erro comum**: "Claude Code is not supported on Windows"
- **Dependências**: Node.js 18+ e npm/yarn

### Problema com WSL e PATH
O comando `claude` funciona em shell interativo do WSL, mas não via `wsl comando`:

```bash
# ❌ Não funciona
wsl claude --version
# Erro: command not found

# ✅ Funciona
wsl
claude --version
```

**Causa:** Shells não-interativos não carregam `.bashrc` automaticamente.

### Problema com NVM
O Claude Code foi instalado via npm/nvm, criando dependências:

```bash
# Localização do executável
/home/valdemar/.nvm/versions/node/v22.14.0/bin/claude

# ❌ Não funciona - Node não encontrado
wsl /caminho/completo/claude

# ✅ Funciona - Usando node explicitamente
wsl bash -c "source ~/.bashrc && /caminho/node /caminho/claude"
```

### Diferença entre Shells Interativos e Não-Interativos

**Shell Interativo (WSL direto):**
- Carrega `.bashrc`
- Inicializa nvm
- PATH completo disponível

**Shell Não-Interativo (via `wsl comando`):**
- Não carrega `.bashrc`
- NVM não inicializado
- PATH limitado

### Soluções Testadas

#### 1. Comando Completo (Funciona)
```bash
wsl bash -c "source ~/.bashrc && /home/valdemar/.nvm/versions/node/v22.14.0/bin/node /home/valdemar/.nvm/versions/node/v22.14.0/bin/claude"
```

#### 2. Script Wrapper (Recomendado)
Encapsula a complexidade em um script simples:
```bash
wsl ~/claude-wrapper.sh
```

#### 3. Alternativas Não Implementadas
- Instalar Node.js via `apt` (mais simples, mas altera ambiente)
- Mover configuração nvm para `.profile`

### Autenticação Claude Code
- **Autenticação OAuth**: Login via browser com conta Anthropic
- **Não requer API key**: Token gerado automaticamente
- **Token local**: Armazenado no WSL (~/.config/claude)
- **Compartilhamento**: Plugin IntelliJ usa mesmo token do CLI
- **Renovação automática**: Token renovado quando necessário

### Verificações Úteis

```bash
# Verificar localização do claude
which claude

# Testar autenticação
claude /status

# Verificar configuração nvm
cat ~/.bashrc | grep nvm

# Testar script wrapper
wsl ~/claude-wrapper.sh --version
```

### Comandos Úteis Claude Code
```bash
/help          # Lista todos os comandos disponíveis
/init          # Cria CLAUDE.md no projeto atual
/status        # Mostra status da autenticação
/clear         # Limpa histórico da conversa
/reset         # Reinicia sessão
```

## Troubleshooting

### Plugin não encontra executável
- Verificar caminho: `wsl ~/claude-wrapper.sh`
- Testar manualmente no PowerShell

### Erro de autenticação
```bash
# Reautenticar no WSL
wsl
claude
```

### Script wrapper não executa
```bash
# Verificar permissões
ls -la ~/claude-wrapper.sh
chmod +x ~/claude-wrapper.sh
```

### Node not found
- Verificar se nvm está no `.bashrc`
- Ajustar caminho no script wrapper para sua versão do Node

---

## Referências e Links Úteis

- [**Claude Code Oficial**](https://docs.anthropic.com/en/docs/claude-code) - Documentação completa da ferramenta
- [**Claude Code NPM**](https://www.npmjs.com/package/@anthropic-ai/claude-code) - Pacote oficial no registro NPM
- [**Anthropic Claude**](https://www.anthropic.com/claude) - Site oficial do Claude AI
- [**WSL Documentation**](https://learn.microsoft.com/en-us/windows/wsl/) - Guia oficial do Windows Subsystem for Linux
- [**WSL Troubleshooting**](https://learn.microsoft.com/en-us/windows/wsl/troubleshooting) - Solução de problemas do WSL
- [**IntelliJ IDEA**](https://www.jetbrains.com/idea/) - IDE oficial da JetBrains
- [**Node.js & NVM**](https://github.com/nvm-sh/nvm) - Node Version Manager no GitHub
- [**Bash Manual - Interactive Shells**](https://www.gnu.org/software/bash/manual/html_node/Interactive-Shells.html) - Diferenças entre shells interativos e não-interativos

## Palavras-chave para Busca

Claude Code, Anthropic AI, Windows Subsystem for Linux, WSL, IntelliJ IDEA, plugin integration, shell scripting, Node.js, npm, nvm, wrapper script, Windows development, Linux tools, AI coding assistant, development environment setup, troubleshooting guide.

**Problema comum**: "Claude Code not supported on Windows" → **Solução**: WSL + wrapper script
**Erro típico**: "command not found" quando executando via `wsl comando` → **Causa**: shell não-interativo não carrega .bashrc
