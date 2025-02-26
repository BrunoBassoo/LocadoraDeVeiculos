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

## <> Diagrama de Classes

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
    }

    class Cliente{
        int ID
        string e-mail
        string senha
        boolean premium
        LoginUsuario()
        Cadastro()
        SolicitarLocacao()
        EfetuaPagamento()
    }

    class Operador{
        int ID
        string e-mail
        string senha
        VerificarLocacao()
    }

    class Atendente{
        int ID
        string e-mail
        string senha
        ReceberCliente()
        VerificaCadastro()
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
    }

    class TimePatio{
        Operador funcionario
        LiberaLocacao()
        RecebeLocacao()
    }

    class SistemaPagamento{
        int ID
        string tipoPagamento
        CriaExtrato()
    }

    class DETRAN{
        Veiculo veiculo
        BuscarMulta()
    }

```

---

## 🛠️ Tecnologias

*   **Diagramas:** [draw.io](http://draw.io)
*   **Diagramas de Caso de Uso:** ![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?logo=microsoft-excel&logoColor=white)
*   **Diagramas de Classes:** [mermaid.live](https://mermaid.live/)

## 🤝 Contribuições
Contribuições para aprimorar este projeto são muito bem-vindas, forke o projeto e contribua!

## ✉️ Contato
Qualquer dúvida sobre o projeto entrar em contato, será um prazer!
