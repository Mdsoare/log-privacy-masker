# 🧹 Log-Privacy-masker — PowerShell Log Anonymization & PII Masking

<!-- Badges do Topo -->
![Security Compliance](https://img.shields.io/badge/Security-Local%20Only%20%2F%20Zero%20Trust-green.svg)
![CI Pipeline](https://github.com/Mdsoare/log-privacy-masker/actions/workflows/security-scan.yml/badge.svg)
![Security Rating](https://img.shields.io/badge/Security-DevSecOps%20Hardened-green?style=flat&logo=github)
![Code Style: PSScriptAnalyzer](https://img.shields.io/badge/code%20style-PSScriptAnalyzer-5391FE.svg?logo=powershell)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)

<!-- Tech Stack & DevSecOps Ecosystem -->
![PowerShell](https://img.shields.io/badge/PowerShell-7.0%2B-5391FE?style=for-the-badge&logo=powershell&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)
![Dependabot](https://img.shields.io/badge/Dependabot-025E8C?style=for-the-badge&logo=dependabot&logoColor=white)
![SAST & SCA](https://img.shields.io/badge/DevSecOps-SAST%20%26%20SCA-red?style=for-the-badge&logo=github-actions&logoColor=white)

---

Ferramenta em PowerShell para localização e mascaramento de dados sensíveis (PII, credenciais, nomes e tokens) em arquivos de log, garantindo conformidade com regras de proteção de dados (**LGPD**) e boas práticas de segurança da informação.

---

## 🚀 Funcionalidades

- **Sanitização por Expressão Regular (Regex):** Substitui o valor dos campos sensíveis por `*****`, preservando os rótulos e delimitadores para auditoria.

- **Campos Cobertos:** `name`, `nome`, `login`, `pass`, `passwd`, `password`, `senha`, `token`.

- **Modo Recursivo:** Processa subdiretórios inteiros com filtros customizados de extensão.

- **Suporte Nativo a UTF-8:** Evita corrupção de caracteres acentuados durante a leitura/escrita.

- **Visualização de Progresso:** Feedback visual interativo via terminal durante o processamento em lote.

---

## 📋 Pré-requisitos

- **PowerShell 5.1** ou superior (Compatível com PowerShell Core / Cross-platform).

- Permissão de leitura no diretório/arquivo de origem e escrita no diretório de destino.

---

## 💻 Como Usar

### 1. Processamento Lote / Recursivo (Recomendado)

- `anonimiza.ps1`

Processa todos os arquivos de log de um diretório e seus subdiretórios:

```powershell
# Processa o diretório atual em arquivos .log
.\anonimiza.ps1 -Diretorio . -Extensao "*.log"

# Processa um diretório específico com logs rotacionados
.\anonimiza.ps1 -Diretorio "C:\Logs\Sistema" -Extensao "*.log.*"
```

### 2. Processamento de Arquivo Único

- `sanitizar.ps1`

Ideal para execuções pontuais via linha de comando ou pipelines:

```powershell
# Define arquivo de saída padrão (new_<nome_original>)
.\sanitizar.ps1 -ArquivoEntrada "C:\logs\producao.log"

# Define um caminho de saída customizado
.\sanitizar.ps1 -ArquivoEntrada "C:\logs\producao.log" -ArquivoSaida "C:\logs\sanitizado.log"
```

---

## 🛠️ Padrão de Sanitização

O script localiza padrões chave/valor delimitados por parênteses colchetes `[ ]` e substitui o valor por asteriscos:

### Entrada Exemplo

```text
2026-03-26 22:00:38 INFO AuthController - User login:[antony.santiago] authenticated with pass:[Secret123!]
2026-03-26 22:00:39 WARN Service - Event triggered by name:[John Doe] token:[abc123xyz]
```

### Saída Gerada

```text
2026-03-26 22:00:38 INFO AuthController - User login:[*****] authenticated with pass:[*****]
2026-03-26 22:00:39 WARN Service - Event triggered by name:[*****] token:[*****]
```

---

## 📄 Estrutura do Repositório

```text
.
├── .gitignore
├── LICENSE
├── README.md
└── scripts/
    ├── .gitignore
    ├── anonimiza.ps1    # Script Principal (Em Lote / Recursivo)
    └── sanitizar.ps1        # Script Auxiliar (Arquivo Único)
```

---

## 🛡️ Segurança & LGPD

Esta ferramenta foi desenvolvida para auxiliar equipes de Segurança da Informação, DevOps e Suporte a higienizarem evidências e logs de auditoria antes do compartilhamento com terceiros ou armazenamento em repositórios externos.

---

*Desenvolvido por **Marcelo Soares** | Especialista em Segurança da Informação e Computação Forense.*