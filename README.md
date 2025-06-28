# Dev Guides

Uma coleção de guias de desenvolvimento e documentação técnica para desenvolvedores.

## 📚 Sobre o Projeto

Este repositório contém guias práticos e documentação técnica sobre ferramentas e tecnologias de desenvolvimento. O objetivo é centralizar conhecimento útil e criar recursos de referência rápida para desenvolvedores.

## 🚀 Guias Disponíveis

### Claude Code
- **[Claude Code no WSL](docs/claude-code-wsl/)** - Guia completo para configurar e usar o Claude Code no Windows Subsystem for Linux

### Em Desenvolvimento
- Docker e Containers
- Git Workflows Avançados
- VS Code Extensions
- Configuração de Ambientes de Desenvolvimento

## 🌐 Site GitHub Pages

Este projeto está configurado para usar GitHub Pages com Jekyll. Acesse o site em:
`https://varantes.github.io/dev-guides`

### Estrutura do Site

```
dev-guides/
├── docs/                    # Guias organizados por categoria
│   ├── claude-code-wsl/    # Guia do Claude Code WSL
│   └── ...                 # Outros guias
├── _config.yml             # Configuração Jekyll
├── index.md               # Página inicial
└── README.md              # Este arquivo
```

## 🛠️ Como Contribuir

1. Fork este repositório
2. Crie uma branch para sua feature (`git checkout -b feature/novo-guia`)
3. Adicione seu guia na pasta `docs/`
4. Commit suas mudanças (`git commit -am 'Adiciona guia X'`)
5. Push para a branch (`git push origin feature/novo-guia`)
6. Abra um Pull Request

### Estrutura de um Guia

Cada guia deve seguir esta estrutura:

```markdown
---
layout: default
title: Título do Guia
parent: Guias de Desenvolvimento
nav_order: X
---

# Título do Guia

Descrição breve do que o guia aborda.

## Pré-requisitos
## Instalação
## Configuração
## Uso Básico
## Dicas e Truques
## Solução de Problemas
## Recursos Adicionais
```

## 📝 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 📧 Contato

- GitHub: [@varantes](https://github.com/varantes)
- Email: varantes@exemplo.com

---

⭐ Se este projeto foi útil para você, considere dar uma estrela no repositório!