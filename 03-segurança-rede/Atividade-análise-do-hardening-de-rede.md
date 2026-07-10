# Atividade: Análise do hardening de rede 🛡️

## 📝 Apresentação da atividade
Este projeto corresponde à quarta atividade prática do Curso 3 (**Conectar e Proteger: Redes e Segurança de Redes**) do curso Cybersecurity do Google. Analisei o caso de uma organização de mídia social que sofreu uma grande violação de dados devido a falhas críticas de configuração e hábitos dos usuários.

Minha meta foi inspecionar as vulnerabilidades relatadas, mapear as melhores ferramentas de **Network Hardening** (Fortalecimento de Rede) e propor uma avaliação de risco de segurança estruturada para evitar novos vazamentos de dados de clientes.

<details>
<summary>📸 PDFs dos materiais de apoio</summary>

[Network hardening tools.xlsx](https://github.com/user-attachments/files/29909729/Network.hardening.tools.xlsx)

[Security risk assessment report.pdf](https://github.com/user-attachments/files/29909727/Security.risk.assessment.report.pdf)

</details>

---

## 📂 O Cenário e as Vulnerabilidades Encontradas
*Clique na caixa abaixo para entender os pontos fracos.*

<details>
<summary>🔍 Visualizar as vulnerabilidades</summary>

Após a investigação da rede da organização, foram mapeados 4 problemas graves:
1. **Compartilhamento de credenciais:** Os funcionários compartilham senhas entre si diariamente.
2. **Senha padrão de fábrica:** A credencial de administrador do banco de dados principal nunca foi alterada.
3. **Firewalls sem regras de filtragem:** Os firewalls estão ativos, mas não possuem regras configuradas para barrar tráfego malicioso de entrada ou saída.
4. **Ausência de MFA:** Não há autenticação multifator ativa para proteger os acessos.
</details>

---

## 📄 Relatório de avaliação de risco de segurança

### 📊 Part 1: Três ferramentas e métodos para implementar.

Com base no catálogo de ferramentas de hardening de rede, selecionei os três métodos mais urgentes e eficazes para os riscos da organização.

| Hardening task selecionada | Vulnerabilidade alvo | Objetivo principal baseado nas diretrizes |
| :--- | :---: | :--- |
| **Autenticação multifator (MFA)** | Funcionários compartilhando senhas e ausência de MFA corporativo. | Exigir duas ou mais formas de verificação de identidade (como senhas, PINs ou tokens temporários) antes de liberar o acesso aos sistemas. |
| **Filtragem de portas / manutenção de firewall** | Firewalls ativos, mas sem regras de filtragem de tráfego implementadas. | Configurar regras estritas para bloquear ou permitir portas específicas e impedir que tráfego indesejado ou malicioso passe pela rede privada. |
| **Políticas de senha** | Senha de administrador definida como padrão e compartilhamento de credenciais. | Estabelecer novos critérios de criação de credenciais complexas (uso de hashes e salts) para evitar ataques de força bruta ou adivinhações simples. |

---

### 💡 Parte 2: Recomendações

Recomendações que devem ser implementadas imediatamente pela organização.

#### 📝 Recomendação 1: Implementação de autenticação multifator (MFA)
*   **Por que essa técnica é eficaz?** 
  O maior problema atual da empresa é a fragilidade das credenciais de acesso. O MFA é extremamente eficaz porque invalida o poder da posse simples da senha.
*   **Com que frequência precisa ser implementada?** 
  É  um controle que se configura **uma vez e permanece ativo continuamente** protegendo os sistemas. No entanto, revisões operacionais e de manutenção devem ser feitas periodicamente (por exemplo, a cada dois meses) para garantir que novos funcionários entrem na política e que colaboradores desligados tenham seus tokens revogados imediatamente.

#### 📝 Recomendação 2: Configuração de filtros de porta e manutenção do firewall
*   **Por que essa técnica é eficaz?** 
  Um firewall sem regras de filtragem é como ter uma barreira física com a cancela sempre aberta. A filtragem de portas é eficaz porque limita a comunicação apenas ao estritamente necessário para o negócio.
*   **Com que frequência precisa ser implementada?** 
  A  manutenção das regras de firewall e a verificação de portas devem ocorrer de forma **frequente e preventiva**
