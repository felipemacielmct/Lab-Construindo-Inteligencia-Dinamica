***

# 🧪 Lab: Construindo Inteligência Dinâmica no Copilot Studio

## 🎯 Objetivo

O objetivo deste laboratório é reforçar os conceitos de:

*   ✅ Variáveis
*   ✅ Adaptive Cards
*   ✅ Tópicos no Copilot Studio
*   ✅ Uso de Power Fx para lógica dinâmica

Ao final deste lab você será capaz de:

*   Entender como os **tópicos** estruturam a conversa do agente
*   Compreender a anatomia de um tópico (gatilhos e nós)
*   Explorar diferentes tipos de nós de conversa
*   Utilizar **Power Fx** para criação de lógica dinâmica
*   Criar um **tópico customizado** para execução de tarefas
*   Integrar o agente com dados do **SharePoint**
*   Construir formulários dinâmicos com **Adaptive Cards**

***

## 🧩 Conceito: Tópicos

### 🔹 Qual a principal função de um tópico?

Um **tópico** é a estrutura de conversa que permite ao seu agente:

*   Responder perguntas
*   Executar tarefas
*   Guiar o usuário em um fluxo conversacional

Pense em um tópico como uma **mini aplicação conversacional**.

Os tópicos ajudam a:

*   Organizar o conhecimento do agente
*   Tornar a conversa mais natural
*   Resolver problemas de forma efetiva

***

### 🔹 Tipos de Tópicos

| Tipo              | Descrição                                     |
| ----------------- | --------------------------------------------- |
| **System Topics** | Tópicos padrão do sistema                     |
| **Custom Topics** | Criados manualmente para cenários específicos |

***

### 🔹 Componentes de um Tópico

*   **Trigger Phrases** → Palavras ou frases que iniciam o tópico
*   **Conversation Nodes** → Blocos que controlam o fluxo da conversa
*   **Topic Management** → Controle de navegação entre tópicos

***

## ⚙️ Uso do Power Fx

O **Power Fx** é a linguagem low-code utilizada para adicionar:

*   Lógica dinâmica
*   Manipulação de dados
*   Controle de variáveis

> É a mesma linguagem utilizada no Power Apps (similar ao Excel).

### 📌 Exemplos

#### Definir variável

```PowerFx
Set(userName, "Felipe Maciel")
```

#### Criar condição

```PowerFx
If(score > 80, "Pass", "Fail")
```

#### Formatar data

```PowerFx
Text(DateValue, "dd/mm/aaaa")
```

***

# 🚀 Início do Laboratório

***

## 1️⃣ Criar um Novo Tópico

    Add a topic → From Blank

**Nome:**

    Dispositivos disponíveis

**Trigger Description:**

> Este tópico ajuda os usuários a encontrar dispositivos disponíveis em nossa lista do SharePoint. O usuário poderá visualizar itens prontos para uso como laptops, smartphones e acessórios.

***

## 2️⃣ Definir Trigger Inputs

Acesse:

    (...)
    → Details
    → Topic Details
    → Input

<img width="1283" height="675" alt="image" src="https://github.com/user-attachments/assets/7473f629-b5f7-4701-90b3-c9dc9066ea7c" />


Crie uma nova variável:

| Propriedade | Valor                       |
| ----------- | --------------------------- |
| Name        | VarTipoDispositivo          |
| Data Type   | String                      |
| Identify As | Users entire response       |
| Description | Laptop, Desktop, Smartphone |

<img width="509" height="1080" alt="image" src="https://github.com/user-attachments/assets/eef6cdb1-a100-40ee-bee2-4c236bc5c0d3" />


***

## 3️⃣ Definir Trigger Outputs

Crie uma nova variável:

| Propriedade | Valor                             |
| ----------- | --------------------------------- |
| Name        | VarDispositivosDisponiveis        |
| Data Type   | Table                             |
| Description | Lista de dispositivos disponíveis |

<img width="510" height="1080" alt="image" src="https://github.com/user-attachments/assets/88e13317-6718-4be4-bd3f-b0402c1aa742" />


***

## 4️⃣ Adicionar Conector do SharePoint

Adicione um novo nó:

    + → Add a Tool → SharePoint - Get Items

Configure:

*   Site: **Contoso IT Helpdesk**
*   Lista: **Dispositivos**

<img width="675" height="1080" alt="image" src="https://github.com/user-attachments/assets/0a055152-9beb-4ab4-95cf-367662373a62" />


***

### 📌 Filter Query (Power Fx)



```PowerFx
Concatenate(
    "Status eq 'Disponível' and AssetType eq '",
    Topic.VarDeviceType,
    "'"
)
```

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/024418ec-308d-4a3c-a269-5585f05de23a" />


*   Limit Columns by View → **All Items**
*   Output → **VarDispositivos**
*   Defina como variável **Global**

<img width="672" height="1075" alt="image" src="https://github.com/user-attachments/assets/22d6407e-500f-4875-abc1-2b422daba26e" />


***

## 5️⃣ Salvar Dispositivos em Variável Global

Adicione um novo nó:

    Variable Management → Set a variable value

| Campo    | Valor                        |
| -------- | ---------------------------- |
| Variable | VarDispositivos              |
| Value    | Global.VarDispositivos.value |

<img width="720" height="963" alt="image" src="https://github.com/user-attachments/assets/413cbc17-cf14-41c8-8e68-ab32d6333794" />



***

## 6️⃣ Atualizar Instruções do Agente

Adicione:

```markdown
# Dispositivos

Ajude a encontrar dispositivos disponíveis usando o tópico 
[Dispositivos disponíveis].

Sempre extraia o VarDeviceType da entrada do usuário.

Após fornecer os detalhes, pergunte se o usuário deseja solicitar um dispositivo disponível.

Referencie:
"/Dispositivos disponíveis"
```

<img width="833" height="396" alt="image" src="https://github.com/user-attachments/assets/d98066ce-3516-4768-acf5-f66e2c1a7e51" />


***

## 7️⃣ Testar

### 💬 Prompt

    Eu preciso de um laptop

***

# 📝 Solicitação com Adaptive Card

***

## 8️⃣ Criar Novo Tópico

    Add a topic → From Blank

**Nome:**

    Solicitar Dispositivo

***

## 9️⃣ Adicionar "Ask with Adaptive Card"

Edite o Card e substitua todo o JSON pelo seguinte:

<a link="https://github.com/felipemacielmct/Lab-Construindo-Inteligencia-Dinamica/blob/main/adaptivecard.json">Adaptive Card Simple lab</a>

<img width="1280" height="1080" alt="image" src="https://github.com/user-attachments/assets/a4f03219-634f-4dae-a84c-87b9f0da3499" />


***

## 🔗 Referência

Para testar outros modelos de cartão:

👉 [Adaptive Cards Designer](https://adaptivecards.microsoft.com/designer)

***

## 🔟 Atualizar Instruções do Agente

Adicione:

```markdown
Se o usuário responder "sim" à pergunta de solicitação,
ative o tópico:

[Solicitar dispositivo]

Caso responda "não",
ative:

[Despedida]
```

<img width="821" height="559" alt="image" src="https://github.com/user-attachments/assets/a1ed932a-4af2-4dfb-a52b-f30024d65288" />


***

## ✅ Teste Final

### 💬 Fluxo esperado

    Usuário: Eu preciso de um laptop
    Agente: (lista dispositivos)
    Agente: Deseja solicitar um dispositivo?

    Usuário: Sim
    Agente: (Adaptive Card exibido)

***

# 🏁 Fim do Lab

***

Se quiser, eu posso te gerar também uma versão com **badges + arquitetura do fluxo em Mermaid** pra deixar o README mais "client-ready" para demo.
