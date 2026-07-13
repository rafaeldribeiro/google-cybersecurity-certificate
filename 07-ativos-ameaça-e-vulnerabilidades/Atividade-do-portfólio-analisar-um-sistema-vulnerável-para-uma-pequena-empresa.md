# Atividade: Relatório de avaliação de vulnerabilidade de segurança

## 📝 Descrição do Projeto
Realizei uma auditoria interna focada nos controles de acesso e na exposição do servidor de banco de dados remoto da organização. 

O objetivo principal foi mapear os riscos de manter nossa base de dados MySQL aberta ao público e estruturar um plano de remediação baseado nas diretrizes de risco do padrão **NIST SP 800-30 Rev. 1**.


<details>
<summary>📸 link do material de apoio</summary>

[NIST SP 800-30 Rev. 1.pdf](https://github.com/user-attachments/files/29986522/NIST.SP.800-30.Rev.1.pdf)

[Vulnerability assessment report.pdf](https://github.com/user-attachments/files/29986519/Vulnerability.assessment.report.pdf)

</details>

---

## 📂 Visão geral da infraestrutura do sistema

*   **Componentes do servidor:** Processador de alta performance, 128 GB de memória RAM, sistema operacional Linux atualizado e sistema de gerenciamento de banco de dados MySQL.
*   **Conectividade:** Conexão de rede estável utilizando endereços IPv4 e comunicação criptografada ativa via SSL/TLS.
*   **Escopo da avaliação:** O foco desta análise limita aos controles de acesso lógicos, integridade, disponibilidade e confidencialidade dos dados armazenados no servidor durante o período de três meses (de junho a agosto), desconsiderando a segurança física do hardware.

---

## 📄 Relatório de Avaliação de Vulnerabilidades

### 🎯 Objetivo
O objetivo desse relatório é avaliar os riscos de segurança do nosso servidor de banco de dados MySQL, que está exposto diretamente à internet pública desde o lançamento da empresa, há três anos. Esse servidor é vital para o e-commerce, pois armazena todos os cadastros e informações que nossa equipe remota utiliza globalmente para encontrar novos clientes.

---

### 📊 Avaliação de vulnerabilidades
A tabela abaixo quantifica os riscos associados ao servidor com base no cálculo padrão de matriz de risco do NIST.

| Fonte | Evento de Ameaça | Probabilidade | Gravidade | Risco |
| :--- | :--- | :---: | :---: | :---: |
| **Hacker** | Conseguir informações confidenciais por meio de vazamento de dados dos clientes. | 3 | 3 | **9** |
| **Funcionário** | Alterar ou deletar informações críticas das operações diárias por acidente ou erro de permissão. | 2 | 3 | **6** |
| **Hacker** | Realizar ataques de Negação de Serviço DoS para derrubar e sobrecarregar o banco de dados. | 2 | 2 | **4** |

---

### 🛠️ Abordagem
Escolhi essas três fontes de ameaça e seus respectivos eventos porque eles atacam diretamente o nosso maior ponto fraco: o banco de dados estar 100% visível na internet. Um hacker externo tem facilidade máxima para tentar roubar dados dos clientes ou derrubar o sistema por DoS, já que não existem barreiras de rede impedindo o acesso inicial ao servidor.

---

### 🛡️ Estratégia de remediação
Para corrigir e mitigar essas vulnerabilidades, a primeira medida urgente é configurar o firewall para implementar uma lista de permissões de IP, garantindo que apenas os escritórios corporativos e conexões autorizadas da equipe remota consigam acessar o banco. Também se deve adotar o framework AAA (Autenticação, Autorização e Contabilização) com controle baseado em funções (RBAC), removendo o privilégio de administrador de funcionários que só precisam fazer consultas de rotina.
