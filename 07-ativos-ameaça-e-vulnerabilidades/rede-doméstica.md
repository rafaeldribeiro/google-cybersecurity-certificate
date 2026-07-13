# Atividade: Classificar recursos em uma rede doméstica 🏠

## 📝 Descrição do projeto
O objetivo foi assumir o papel de dono de uma pequena empresa doméstica para estruturar um inventário de ativos de rede.

---

## 📂 Planilha de inventário de ativos

Abaixo está o inventário de ativos da rede doméstica estruturado com as três referências básicas e os três novos dispositivos identificados no cenário.

| Ativo | Acesso a rede | Proprietário | Localização | Observações | Sensibilidade |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Roteador de rede** *(Referência)* | Contínuo | Provedor de serviços de Internet (ISP) | Local | Possui conexão de 2,4 GHz e 5 GHz. Todos os dispositivos da rede doméstica se conectam à frequência de 5 GHz. | Confidencial |
| **Desktop** *(Referência)* | Ocasional | Proprietário | No local | Contém informações privadas, como fotos. | Restrito |
| **Smartphone para visitantes** *(Referência)* | Ocasional | Amigo | No local e fora do local | Conecta-se à minha rede doméstica. | Apenas para uso interno |
| **Laptop** *(Novo)* | Diária | Proprietário | No local | Usado para gerenciar o negócio. Armazena contratos vigentes, dados financeiros da empresa e credenciais de login de clientes. | **Restrito** |
| **Dispositivo de armazenamento** *(Novo)* | Contínuo | Proprietário | No local | Dispositivo conectado que guarda os backups automáticos de todos os computadores e o histórico fiscal do negócio. | **Confidencial** |
| **Impressora Inteligente** *(Novo)* | Uso ocasional | Proprietário | No local | Impressora inteligente conectada via Wi-Fi para impressão de notas e documentos. Pode ser um ponto de entrada se o firmware estiver desatualizado. | **Apenas para uso interno** |

---

## 📄 Análise de classificação e justificativa de sensibilidade

### 1. Laptop
*   **Acesso e Características:** Conectado diariamente a rede sem fio criptografada pelo proprietário de dentro do escritório.
*   **Sensibilidade:** Classificado como **Restrito**** porque armazena as informações mais sensíveis da nossa operação comercial (dados financeiros e acessos de clientes).

### 2. Dispositivo de armazenamento
*   **Acesso e Características:** Mantém conexão contínua via cabo diretamente ligada à rede local sob responsabilidade do proprietário.
*   **Sensibilidade:** Classificado como **Confidential** pois serve como o cofre de dados e repositório de segurança da empresa.

### 3. Impressora inteligente
*   **Acesso e Características:** Conectado ocasionalmente via Wi-Fi quando há necessidade de emitir documentos fiscais dentro do escritório.
*   **Sensibilidade:** Classificada como **Apenas para uso interno** porque a função é estritamente de uso local por pessoas autorizadas que estão presencialmente no ambiente.
