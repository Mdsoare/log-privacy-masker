# 🧹 Log-Privacy-masker — PowerShell Log Anonymization & PII Masking

![PowerShell](https://img.shields.io/badge/powershell-5.1%2B%20%7C%207%2B-blue.svg)
![License MIT](https://img.shields.io/badge/license-MIT-green.svg)
![Compliance](https://img.shields.io/badge/compliance-LGPD%20%7C%20GDPR-purple.svg)

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

### 1. Processamento Lote / Recursivo (Recomendado) - `anonimiza.ps1`

Processa todos os arquivos de log de um diretório e seus subdiretórios:

```powershell
# Processa o diretório atual em arquivos .log
.\anonimiza.ps1 -Diretorio . -Extensao "*.log"

# Processa um diretório específico com logs rotacionados
.\anonimiza.ps1 -Diretorio "C:\Logs\Sistema" -Extensao "*.log.*"
```

### 2. Processamento de Arquivo Único - `sanitizar.ps1`

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

### Entrada Exemplo:
```text
2026-03-26 22:00:38 INFO AuthController - User login:[antony.santiago] authenticated with pass:[Secret123!]
2026-03-26 22:00:39 WARN Service - Event triggered by name:[John Doe] token:[abc123xyz]
```

### Saída Gerada:
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