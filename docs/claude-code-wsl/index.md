---
layout: default
title: Claude Code no WSL
parent: Guias de Desenvolvimento
nav_order: 1
---

# Claude Code no WSL com Plugin IntelliJ

**Tags:** #wsl #claude #ai #plugin #intellij
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

Conteúdo do script:
```bash
#!/bin/bash
source ~/.bashrc
/home/valdemar/.nvm/versions/node/v22.14.0/bin/node /home/valdemar/.nvm/versions/node/v22.14.0/bin/claude "$@"
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
- **Não suporta Windows nativamente**
- Requer macOS ou Linux
- Mensagem de erro: "Claude Code is not supported on Windows"

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
- **Não usa API key**
- Autenticação via browser (OAuth)
- Token armazenado localmente no WSL
- Plugin usa mesma autenticação

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
/help          # Lista comandos
/init          # Cria CLAUDE.md no projeto
/status        # Status da autenticação
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
