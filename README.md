# 🛡️ parent_control

Sistema de **controle parental inteligente** para redes domésticas, que permite aplicar regras de bloqueio e liberação de conteúdo para cada dispositivo conectado à rede, com base no endereço MAC. Este repositório é o **esqueleto (scaffold)** inicial do projeto e segue a **arquitetura de diplomatas**.

---

## 📚 Objetivo do Projeto

Este projeto busca resolver um problema comum em residências: **como controlar o acesso à internet de forma personalizada por dispositivo**, de maneira automática e segura.

A aplicação permite:

- Bloquear redes sociais para dispositivos de crianças
- Restringir YouTube após determinado horário
- Liberar sites específicos para certos dispositivos
- Aplicar regras de tempo de uso por dispositivo

As regras são aplicadas em um servidor **Pi-hole** ou equivalente (como um wrapper Python: **pyhole**).

---

## 🧱 Sobre a Arquitetura de Diplomatas

Este projeto segue a arquitetura de diplomatas, que organiza o código em camadas bem definidas para facilitar leitura, manutenção, testes e extensão.

Cada componente tem uma responsabilidade específica:

`diplomat`\
Responsável pela comunicação com o mundo externo. Pode incluir entrada (como handlers HTTP) e saída (como chamadas para APIs externas, bancos de dados, etc.). É o "embaixador" da aplicação para o exterior.

`wire/in` e `wire/out`\
Define os contratos de entrada e saída da aplicação. Tudo que entra via Diplomat é validado e convertido com base nos schemas de wire/in. Tudo que sai da aplicação é formatado usando os schemas de wire/out.

`adapters`\
Realizam a transformação dos dados entre os formatos externos (wire) e os modelos internos (models/). Também podem aplicar validações ou mapeamentos específicos.

`models`\
Contém os modelos de dados internos que trafegam entre as camadas da aplicação. Representam a forma canônica dos dados usados na lógica de negócio.

`controllers`\
Responsáveis pela orquestração da lógica de negócio. Recebem dados processados pelos adapters, tomam decisões e, quando necessário, acionam os diplomatas para interagir com sistemas externos.

### Code Structure

```
.
├── parent_control
│   ├── README.md
│   └── src
│       ├── adapters
│       │   └── mac_rule_adapter.py
│       ├── controllers
│       │   └── apply_rule_controller.py
│       ├── diplomat
│       │   ├── http
│       │   │   └── flask_handler.py
│       │   └── client
│       │       └── pyhole_client.py
│       ├── models
│       │   ├── mac_rule.py
│       │   ├── rule_status.py
│       │   ├── request_context.py
│       │   └── pyhole_response.py
│       ├── wire
│       │   ├── in
│       │   │   └── apply_mac_rule_request.py
│       │   └── out
│       │       └── apply_mac_rule_response.py
│       └── main.py
```



---

## 🚀 Como rodar localmente

### ✅ Pré-requisitos

- Python 3.10 ou superior
- Git
- pip (ou virtualenv)

### 📦 Instalação

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/parent_control.git
cd parent_control

# Crie e ative o ambiente virtual
python3 -m venv venv
source venv/bin/activate

# Instale as dependências
pip install fastapi uvicorn pydantic
