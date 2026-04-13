***

# ⚙️ Lab Setup — HelpDesk Agent AI

## 📋 Pré-requisitos

***

### 🗂️ Criar SharePoint Site

Crie um novo SharePoint Site com as seguintes configurações:

| Propriedade     | Valor                |
| --------------- | -------------------- |
| **Nome**        | Contoso IT Help Desk |
| **Escopo**      | Team Scope           |
| **Privacidade** | Private              |

***

## 🧱 Criar Solution (Power Platform)

No ambiente do **Copilot Studio**, crie uma nova Solution:

| Propriedade      | Valor                             |
| ---------------- | --------------------------------- |
| **Display Name** | Contoso Solutions IT              |
| **Name**         | ContosoSolutionsIT                |
| **Publisher**    | CDS Default Publisher (Cr894ce)   |
| **Description**  | Copilot Studio Learning Champions |

> 💡 As Solutions funcionam como pacotes para gerenciamento de ciclo de vida (ALM) dos seus agentes e componentes.

***

## 🤖 Criar Agente

Crie um novo agente utilizando:

    Advanced Mode

<img width="354" height="152" alt="image" src="https://github.com/user-attachments/assets/2242c1df-5562-4e18-8cd6-e11051acfb25" />


| Propriedade      | Valor                                                              |
| ---------------- | ------------------------------------------------------------------ |
| **Name**         | HelpDesk Agent AI                                                  |
| **Instructions** | Utilizar conteúdo do bloco de notas "Instrução do agente Helpdesk" |

***

# 📚 Configuração de Knowledge

***

## 1️⃣ Public Websites

Adicione as seguintes fontes de conhecimento:

*   [Microsoft Support](https://support.microsoft.com/)
*   [Microsoft Troubleshoot Docs](https://learn.microsoft.com/pt-br/troubleshoot/)

| Configuração | Valor   |
| ------------ | ------- |
| Web Search   | Disable |

📌 Durante o teste, utilize o **Activity** para apresentar o raciocínio do agente.

***

### ✅ Teste do Agente

**Prompt:**

    Como posso verificar o status da garantia do meu Surface?

***

## 2️⃣ SharePoint Knowledge Source

Adicione como fonte:

*   Contoso IT Helpdesk SharePoint Site: Site do sharepoint com template padrao do helpdesk

| Configuração | Valor   |
| ------------ | ------- |
| Web Search   | Disable |

📌 Utilize o **Activity Panel** para demonstrar como o agente utiliza a fonte organizacional.

***

## 3️⃣ Upload de Arquivos

Faça upload do documento:

    Contoso Guest Wi-Fi Connection Guide

Adicione como fonte de conhecimento:

| Configuração | Valor               |
| ------------ | ------------------- |
| Fonte        | Contoso IT Helpdesk |
| Web Search   | Disable             |

***


### ✅ Teste do Agente (Múltiplas Fontes)

**Prompt:**

    Como posso acessar a VPN Contoso da nossa empresa pelo meu dispositivo?

✔️ Validar:

*   Uso da fonte do SharePoint
*   Uso do documento carregado
*   Resposta consolidada pelo agente

***

# 🏁 Fim do Setup

***
