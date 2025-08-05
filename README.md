# 🛡️ parent_control

Sistema de **controle parental inteligente** para redes domésticas, que permite aplicar regras de bloqueio e liberação de conteúdo para cada dispositivo conectado à rede, com base no endereço MAC. Este repositório é o **esqueleto (scaffold)** inicial do projeto e segue a **arquitetura de diplomatas**.

> ✅ Ideal para ser usado como base em projetos de TCC. Este repositório foi criado para ser **forkado**, estudado e estendido.

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

## 🧱 Arquitetura: Diplomatas

A arquitetura utilizada neste projeto é chamada de **diplomatas**. Nela, a aplicação é dividida em camadas bem definidas que se comunicam entre si via modelos de dados. Isso favorece testes, manutenção e clareza de propósito.


### Code Structure

```
├── parent_control
│ ├── adapters
│ │ └── mac_rule_adapter.py
│ ├── controllers
│ │ └── apply_rule_controller.py
│ ├── diplomat
│ │ ├── http
│ │ │ └── flask_handler.py
│ │ └── client
│ │ └── pyhole_client.py
│ ├── models
│ │ ├── mac_rule.py
│ │ ├── rule_status.py
│ │ ├── request_context.py
│ │ └── pyhole_response.py
│ ├── wire
│ │ ├── in
│ │ │ └── apply_mac_rule_request.py
│ │ └── out
│ │ └── apply_mac_rule_response.py
│ └── main.py
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
