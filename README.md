# 🚗💨 Locadora de Veículos VL:  Sistema de Gestão de Locações

[![Status do Projeto](https://img.shields.io/badge/Status-Em%20Desenvolvimento-yellow)](https://shields.io/)

## 🌟 Equipe de Desenvolvimento

Uma equipe dedicada a transformar o controle de locações da VL!

*   **Bruno Basso** ➔ 22.123.067-5
*   **Gabriel Balbine** ➔ 22.222.001-4
*   **Gabriela Ciocci** ➔ 22.222.032-9
*   **Guilherme Albuquerque** ➔ 22.224.024-4

---

## 📖 Sobre o Projeto

A Locadora de Veículos VL, uma empresa regional em crescimento, nos contratou para modernizar sua gestão!  Atualmente, a VL opera com processos manuais e registros em fichas.  Nosso desafio é criar um sistema que automatize e otimize todas as etapas da locação de veículos.

## 🎯 Objetivo

Desenvolver um sistema completo para a Locadora VL, abrangendo:

*   ✅ **Modelagem de Software:**  Utilizando as melhores práticas para criar uma base sólida.
*   🗺️ **Diagrama de Caso de Uso:**  Visualizando as interações entre usuários e o sistema.
*   ⚙️ **Requisitos Funcionais e Não Funcionais:**  Garantindo que o sistema atenda a todas as necessidades da VL.
*   👥 **Atores:**  Identificando quem interage com o sistema (clientes, funcionários, etc.).

## 🚀 Diagrama de Casos de Uso

Este diagrama mostra as principais funcionalidades do sistema e como os diferentes atores interagem com ele:

<img src="UseCasesVL.drawio.png" alt="Diagrama de Casos de Uso" width="600">

## 📝 Casos de Uso Detalhados

Abaixo, detalhamos cada caso de uso, mostrando o fluxo principal, fluxos alternativos, pré-condições e pós-condições.

### UC_01 - Solicitação de um Veículo

<details>
<summary>Clique para expandir</summary>
<img src="uc_01.png" alt="UC_01 - Solicitação de um Veículo">
</details>

### UC_02 - Controlar as Locações

<details>
<summary>Clique para expandir</summary>
<img src="uc_02.png" alt="UC_02 - Controlar as Locações">
</details>

### UC_03 - Buscar Multas

<details>
<summary>Clique para expandir</summary>
<img src="uc_03.png" alt="UC_03 - Buscar Multas">
</details>

### UC_04 - Verificar Locações Pendentes

<details>
<summary>Clique para expandir</summary>
<img src="uc_04.png" alt="UC_04 - Verificar Locações Pendentes">
</details>

### UC_05 - Consolidar os Pagamentos

<details>
<summary>Clique para expandir</summary>
<img src="uc_05.png" alt="UC_05 - Consolidar os Pagamentos">
</details>

---

## 🧮 Diagrama de Classes

```mermaid

classDiagram

    Pessoa <|-- Cliente : é
    Pessoa <|-- Operador : é
    Pessoa <|-- Atendente : é
    Operador <|-- TimePatio : é

    Empresa "1" -- "1" Operador : possui
    Empresa "1" -- "1..*" Veiculo : possui
    Operador "1..*" -- "*..*" Locacao : efetua
    Locacao "1" -- "1..*" Veiculo : faz parte
    Cliente "1" -- "1..*" SistemaPagamento : efetua
    Atendente "1..*" -- "1..*" Cliente : recebe
    Veiculo "1..*" -- "1" DETRAN : cadastrado
    Cliente "1" -- "1..*" Locacao : tem

    class Pessoa{
        string nome
        long CPF
        data nascimento
        int idade
        VerificarCPF()
        RecusaCPF()
    }

    class Cliente{
        int ID
        string e-mail
        string senha
        boolean premium
        LoginUsuario()
        Cadastro()
        EscolherCategoriaEVeiculo()
        SolicitarLocacao()
        ConsultarPagamento()
        EfetuarPagamento()
        RetirarVeiculo()
        DevolverVeículo()
    }

    class Operador{
        int ID
        string e-mail
        string senha
        VerificarLocacao()
        RecusaLocacao()
    }

    class Atendente{
        int ID
        string e-mail
        string senha
        VerificaCadastro()
        RecusarLocação()
    }

    class Empresa{
        long CNPJ
        string nome
        string endereco
        InicializarSistema()
        LogarNoServidor()
    }

    class Locacao{
        int ID
        Veiculo veiculo
        data duracao
        string categoria
        VerificarUpgrade()
    }

    class Veiculo{
        string marca
        string modelo
        int ano
        int portas
        boolean ar-condicionado
        string placa
        int categoria
        ExibirInfosCategoriaVeiculo()
        VerificarEstado()
    }

    class TimePatio{
        Operador funcionario
        RecebeLocacao()
        ValidaDocumentos()
        LiberaVeiculo()
    }

    class SistemaPagamento{
        int ID
        string tipoPagamento
        CriaExtrato()
        PagamentoCheck()
        CancelaPagamento()
        GerarEstorno()
    }

    class DETRAN{
        Veiculo veiculo
        BuscarMulta()
        EnviarMulta()
    }

```

---

## 📌 Diagrama de Sequência

1. Solicitação de um Veículo
2. Controle das Locações
3. Buscar Multas
4. Consolidar Pagamentos
5. Consolidar Pagamentos


### 1️⃣ Solicitação de um Veículo
Este diagrama ilustra o processo de login, escolha de veículo, solicitação de locação, pagamento e retirada do veículo pelo cliente.

```mermaid
%%{title: "Solicitar Locação de um veículo"}%%
sequenceDiagram
    actor Cliente
    participant C as Cliente
    actor Atendente
    participant A as Atendente
    participant V as Veiculo
    participant L as Locacao
    actor Operador
    participant O as Operador
    actor SistemaPagamento
    participant SP as SistemaPagamento
    actor TimePatio
    participant TP as TimePatio
    
    %% Login 
    Cliente->>C: LoginUsuario()

    %% Fluxo secundario LOGIN NAO EXISTE
    alt FALHA NO LOGN
        C->>Atendente: LoginUsuario()
        Atendente->>A: VerificarCadastro()
        activate A
    else USUÁRIO NÃO EXISTE
        A-->>Cliente: - Necessita de cadastro
        deactivate A
        Cliente->>C: Cadastro()
        activate C 
        C-->>Cliente: - Cadastro Concluido
        deactivate C
        Cliente->>C: LoginUsuario()
    end
    %% Segue
    activate C
    C-->>Cliente: - Login feito
    deactivate C


    %% Escolher categoria e veiculo

    Cliente->>C: EscolherCategoriaVeiculo()
    activate C
    C->>V:  EscolherCategoriaVeiculo()
    deactivate C
    activate V
    activate V
    V-->>V: ExibirInfosCategoriaVeiculo()
    deactivate V

    %% Fluxo secundario CATEGORIA ESGOTADA
    alt CATEGORIA ESGOTADA
        V->>L: CategoriaDisponivel()
        activate L
        L->>L: VerificarUpgrade()
        deactivate L
        L-->>V: - Upgrade de Categoria
    end

    %% Segue
    V-->>Cliente: - Retorna categoria e veiculo
    deactivate V


    %% Solicitar veiculo

    Cliente->>C: SolicitaLocacao()
    activate C
    C->>Operador: SolicitarLocacao()
    deactivate C
    Operador->>O: VerificarLocacao()
    %% Fluxo secundario LOCACAO NEGADA
    activate O
    alt LOCACAO NEGADA
        O-->>A: - Existe locação pendente
        A-->>C: RecusarLocacao() 
    end
    O-->>Cliente: - Locacao OK
    deactivate O
    

    %% Extrato

    Cliente->>C: ConsultarPagamento()
    activate C
    C->>SistemaPagamento: ConsultarPagamento()
    deactivate C
    SistemaPagamento->>SP: CriarExtrato()
    activate SP
    SP-->>Cliente: - Extrato OK
    deactivate SP
    
    
    %% Pagamento

    Cliente->>C: EfetuarPagamento()
    activate C
    C->>SistemaPagamento: EfetuarPagamento()
    %% Fluxo secundario PAGAMENTO NEGADO
    alt PAGAMENTO NEGADO
        SistemaPagamento->>SistemaPagamento: - KILL
    end
    deactivate C
    SistemaPagamento->>SP: PagamentoCheck()
    activate SP
    SP-->>Cliente: - Pagamento OK
    deactivate SP
    

    %% Retirar Veiculo

    Cliente->>C: RetirarVeiculo()
    activate C 
    C->>TimePatio: RetirarVeiculo()
    deactivate C
    activate TimePatio
    TimePatio->>TP: LiberarVeiculo()
    activate TP
    TP-->>Cliente: - Veiculo Liberado
    deactivate TP
```


### 2️⃣ Controle das Locações
Este diagrama ilustra o fluxo de liberação e devolução de um veículo alugado.

```mermaid
%%{title: "Controlar as locações"}%%
sequenceDiagram
    actor Cliente
    participant C as Cliente
    actor TimePatio
    participant TP as TimePatio
    
    Cliente->>C: SoliticarLocação()
    activate C
    C->>TimePatio: SolicitarLocação()
    deactivate C
    TimePatio->>TP: LiberarLocação()
    activate TP
    TP-->>Cliente: - Veículo liberado
    deactivate TP
    activate Cliente
    Cliente->>Cliente: RetirarVeiculo()
    deactivate Cliente
    Cliente->>C: DevolverVeículo()
    activate C
    C->>TimePatio: DevolverVeículo()
    deactivate C
    TimePatio->>TP: ReceberLocação()
    activate TP
    TP-->Cliente: - Veículo devolvido
    deactivate TP

```


### 3️⃣ Buscar Multas
O diagrama abaixo representa o processo de busca de multas associadas ao veículo alugado.

``` mermaid
%%{title: "Buscar multas"}%%
sequenceDiagram
    actor Detran
    participant DT as Detran
    actor Cliente

    DT->>Detran: BuscarMulta()
    activate DT
    activate Detran
    Detran->>Detran: BuscarMulta()
    
    Detran-->>DT: - retornar multa
    
    alt Se existir multa
    DT->>Cliente: EnviarMulta()
    end
    deactivate DT
```
### 4️⃣ Verificar Locações Pendentes
O diagrama detalha a parte de verificação de uma locação do cliente.

```mermaid

%%{title: "Verificar Locações Pendentes"}%%
sequenceDiagram
    actor Operador
    participant O as Operador

    Operador->>O: VerificarLocação()
    activate O
    alt Cliente tem uma locação pendente
        O->>O: - KILL()
    end
    O-->>Operador: - Locação OK
    deactivate O

```

### 5️⃣ Consolidar Pagamentos
Este diagrama detalha como os pagamentos são processados e confirmados para o cliente.

```mermaid
%%{title: "Consolidar os pagamentos"}%%
sequenceDiagram
    actor Cliente
    participant C as Cliente
    actor SistemaDePagamento
    participant SP as SistemaDePagamento
    
    Cliente->>C: ConsultarPagamento()
    activate C
    C->>SistemaDePagamento: ConsultarPagamento()
    deactivate C
    SistemaDePagamento->>SP: CriarExtrato()
    activate SP
    SP-->>Cliente: - Extrato gerado ao cliente
    deactivate SP
    Cliente->>C: EfetuarPagamento()
    activate C 
    C->>SistemaDePagamento: EfetuarPagamento()
    deactivate C
    SistemaDePagamento->>SP: PagamentoCheck()
    activate SP
    SP-->>Cliente: - Pagamento Efetuado
    deactivate SP
    
```

---
## 📈 Diagrama de Sequência

### 1️⃣ Cliente
```mermaid
stateDiagram
    [*] --> LogandoUsuario
    LogandoUsuario --> CadastrandoUsuario : [conta não existente]

    LogandoUsuario --> EscolhendoVeiculo : [logado na conta]
    CadastrandoUsuario --> EscolhendoVeiculo : [cadastro efetuado]

    EscolhendoVeiculo --> SolicitandoLocacao : [categoria disponível]
    EscolhendoVeiculo --> SolicitandoLocacao : [categoria esgotada, recebe upgrade]

    SolicitandoLocacao --> SolicitandoPagamento : [locação efetuada]
    SolicitandoLocacao --> [*] : [existe locação pendente]

    SolicitandoPagamento --> [*] : [pagamento negado]
    SolicitandoPagamento --> RetirandoVeiculo : [pagamento efetuado]

    RetirandoVeiculo --> DevolvendoVeiculo : [após o tempo de locação]
    DevolvendoVeiculo --> [*] : [processo encerrado]
```
### 2️⃣ Detran

```mermaid
stateDiagram
  direction TB
  [*] --> BuscarMulta
  BuscarMulta --> EnviarMulta : [achou uma multa]
  BuscarMulta --> [*] : [não achou uma multa]
  EnviarMulta --> [*]
```
### 3️⃣ SistemaPagamento

```mermaid
stateDiagram
  direction TB
  [*] --> CheckPagamento():[Locação foi feita]
  CheckPagamento() --> CriaExtrato():[Pagamento realizado]
  CheckPagamento() --> CancelaPagamento():[Pagamento não efetuado]
  CriaExtrato() --> GerarEstorno():[Se falhar]
  CriaExtrato() --> [*]
```

### 4️⃣ Veículo

```mermaid

stateDiagram
  direction TB
  [*] --> ExibirInfosCategoriaVeiculo():[Ao realizar pesquisa]
  ExibirInfosCategoriaVeiculo() --> VerificarEstado():[Veículo escolhido]
  VerificarEstado() --> ReijeitaVeiculo(): [Se estiver em estado ruim]
  VerificarEstado() --> [*]
```


### 5️⃣ Pessoa

```mermaid

stateDiagram
  direction TB
  [*] --> VerificaCPF()
  VerificaCPF() --> RecusaCPF():[CPF irregular]
  VerificaCPF() --> [*]
```
### 6️⃣ Operador

```mermaid

stateDiagram
  direction TB
  [*] --> VerificaLocacao():[Após solicitação]
  VerificaLocacao() --> [*] : [Caso não possua locações pendentes]  

```

### 7️⃣ TimePatio

```mermaid
stateDiagram
  direction TB
  [*] --> RecebeLocacao() : [Se o atendente liberar a locação]
  RecebeLocacao() --> ValidaDocumentos()
  ValidaDocumentos() --> LiberaVeiculo() : [Se os documentos estiverem validados]
  ValidaDocumentos() --> CancelaLiberacao() : [Se os documentos estiverem inválidos]
  LiberaVeiculo() --> [*]  
```


---

## 🛠️ Tecnologias

*   **Diagramas:** ![Draw.io](https://img.shields.io/badge/draw.io-diagrams.net-orange?logo=drawio&logoColor=white)
*   **Diagramas de Caso de Uso:** ![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?logo=microsoft-excel&logoColor=white)
*   **Diagramas de Classes:** ![Mermaid](https://img.shields.io/badge/Mermaid-Diagram-blue?logo=mermaid&logoColor=white)
*   **Diagrama de Sequência:** ![Mermaid](https://img.shields.io/badge/Mermaid-Diagram-blue?logo=mermaid&logoColor=white)

---

## 🤝 Contribuições
Contribuições para aprimorar este projeto são muito bem-vindas, forke o projeto e contribua!

## ✉️ Contato
Qualquer dúvida sobre o projeto entrar em contato, será um prazer!
