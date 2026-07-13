# Atividade: Classificar recursos em uma rede doméstica 🏠

## 📝 Descrição do projeto
O objetivo foi assumir o papel de dono de uma pequena empresa doméstica para estruturar um inventário de ativos de rede. Mapear as características e definir a sensibilidade de cada dispositivo é fundamental para aplicar regras de proteção proporcionais ao risco de cada um.


<details>
<summary>📸 links dos materiais de apoio</summary>

[Home asset inventory.xlsx](https://github.com/user-attachments/files/29948916/Home.asset.inventory.xlsx)

<img width="1600" height="900" alt="imagem" src="https://github.com/user-attachments/assets/cc249910-098a-42e4-a1d2-7a621e97b372" />

</details>

---

## 📂 Planilha de inventário de ativos

Abaixo está o inventário de ativos da rede doméstica:

| Asset | Network access | Owner | Location | Notes | Sensitivity |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Network router** *(Referência)* | Continuous | Internet service provider (ISP) | On-premises | Has a 2.4 GHz and 5 GHz connection. All devices on the home network connect to the 5 GHz frequency. | Confidential |
| **Desktop** *(Referência)* | Occasional | Homeowner | On-premises | Contains private information, like photos. | Restricted |
| **Guest smartphone** *(Referência)* | Occasional | Friend | On and Off-premises | Connects to my home network. | Internal-only |
| **Laptop** *(Novo)* | Daily | Homeowner | On-premises | Usado para gerenciar o negócio. Armazena contratos, dados financeiros da empresa e credenciais de login de clientes. | **Restricted** |
| **Storage Device (NAS/HD)** *(Novo)* | Continuous | Homeowner | On-premises | Dispositivo conectado que guarda os backups automáticos de todos os computadores e o histórico fiscal do negócio. | **Confidential** |
| **Smart Printer** *(Novo)* | Occasional | Homeowner | On-premises | Impressora inteligente conectada via Wi-Fi para impressão de notas e documentos. Pode ser um ponto de entrada se o firmware estiver desatualizado. | **Internal-only** |

---

## 📄 Análise de classificação e justificativa de sensibilidade

### 1. Laptop
*   **Acesso e características:** Conecta-se diariamente a rede sem fio criptografada pelo proprietário de dentro do escritório.
*   **Sensibilidade:** Classificado como **Restricted** porque armazena as informações mais sensíveis da operação comercial. O impacto de uma invasão aqui seria desastroso para a continuidade do negócio, exigindo a política de acesso estrito de necessidade de conhecimento.

### 2.Dispositivo de armazenamento / Backups
*   **Acesso e características:** Mantém conexão contínua via cabo diretamente ligada à rede local sob responsabilidade do proprietário.
*   **Sensibilidade:** Classificado como **Confidential** pois serve como o cofre de dados e repositório de segurança da empresa. O acesso a esse dispositivo deve ser limitado a usuários específicos para evitar que um eventual ataque de malware/ransomware consiga corromper ou apagar os backups de recuperação.

### 3.Impressora inteligente
*   **Acesso e características:** Conecta-se ocasionalmente via Wi-Fi quando há necessidade de emitir documentos fiscais dentro do escritório.
*   **Sensibilidade:** Classificada como **Internal-only** porque sua função é estritamente de uso local por pessoas autorizadas que estão presencialmente no ambiente. Não tem necessidade técnica de expor a impressora para a internet externa, reduzindo a superfície de ataque do escritório.
