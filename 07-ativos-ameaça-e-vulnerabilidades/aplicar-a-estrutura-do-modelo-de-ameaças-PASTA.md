# Atividade: Modelagem de Ameaças usando o Framework PASTA 👟🛡️

## 📝 Descrição do Projeto (Project Description)
Este projeto prático representa a nona atividade do Curso 5 (**Ativos, Ameaças e Vulnerabilidades**) do Certificado Profissional de Cybersecurity do Google. Como estudante de Segurança da Informação, simulei a execução de um processo de modelagem de ameaças preventivo para o novo aplicativo de e-commerce de tênis colecionáveis da nossa empresa.

Utilizei o consagrado framework **PASTA** (Process for Attack Simulation and Threat Analysis), que é dividido em 7 estágios estruturados, para alinhar os objetivos comerciais do negócio com as defesas técnicas de TI, antecipando falhas antes de colocarmos o app em produção.

---

## 📂 Relatório Técnico de Modelagem de Ameaças (PASTA Threat Model)

### 📌 Estágio I: Definir Objetivos Comerciais e de Segurança (Define business and security objectives)
Para entender o propósito do aplicativo de tênis, mapeei três objetivos comerciais essenciais para a operação do negócio[cite: 21]:
1.  **Facilitar conexões e transações ágeis:** Permitir que compradores e vendedores se cadastrem, anunciem estoques, troquem mensagens diretas e realizem vendas de forma rápida e fluida[cite: 21].
2.  **Manter a privacidade e conformidade financeira:** Proteger a privacidade dos dados de pagamento dos usuários para evitar penalidades legais e atender às regulamentações financeiras padrão do setor[cite: 21].
3.  **Garantir a confiança do cliente:** Estabelecer uma experiência de checkout tranquila com múltiplas opções de pagamento, amparada por um sistema transparente de avaliações de vendedores[cite: 21].

---

### 📌 Estágio II: Definir o Escopo Técnico (Define the technical scope)
O aplicativo faz uso de quatro tecnologias principais para funcionar: **APIs de terceiros**, criptografia **PKI (AES e RSA)**, funções hash **SHA-256** e o banco de dados **SQL**[cite: 21]. 

*   **Priorização de Tecnologia:** 
    Priorizo a análise de segurança da tecnologia **SQL** e das **APIs de terceiros**[cite: 21]. Como o aplicativo depende de consultas dinâmicas para listar os tênis e de APIs externas para processar os pagamentos, o banco de dados e as comunicações externas são as maiores superfícies de ataque[cite: 21]. Garantir a proteção dessas duas frentes evita o vazamento imediato de informações sensíveis[cite: 21].

---

### 📌 Estágio III: Decompor o Aplicativo (Decompose application)
Nesta etapa, analisamos os fluxos de dados de cada processo lógico[cite: 21, 23]. O mapeamento básico de busca de produtos foi estruturado assim[cite: 23]:

*   **Usuário** solicita a busca de tênis à venda -> **Processo de busca de produtos** (Lógica do app) -> Solicita a listagem de inventário no **Banco de Dados (SQL)**, que retorna os resultados para o usuário através da interface[cite: 23].

---

### 📌 Estágio IV: Análise de Ameaças (Threat analysis)
Com base na nossa superfície de ataque tecnológica e nos fluxos de dados, identifiquei duas ameaças que representam riscos graves às informações tratadas:
1.  **Injeção de SQL (SQL Injection):** Um agente mal-intencionado envia comandos SQL maliciosos nos campos de texto da aplicação (como as buscas por tênis) para burlar o sistema de autenticação ou ler dados sigilosos.
2.  **Sequestro de Sessão (Session Hijacking):** Um invasor intercepta ou adivinha um token de sessão ativo de um usuário legítimo para assumir o controle de sua conta e fazer compras fraudulentas.

---

### 📌 Estágio V: Análise de Vulnerabilidades (Vulnerability analysis)
Para que as ameaças anteriores tenham sucesso, elas precisam explorar pontos fracos no sistema[cite: 21]:
1.  **Falta de Declarações Preparadas (Lack of prepared statements):** O código do backend não sanitiza as entradas de texto dos usuários, permitindo que o interpretador SQL execute trechos de comandos maliciosos injetados nos formulários[cite: 21, 22].
2.  **Credenciais de Login Fracas (Weak login credentials):** O sistema aceita senhas fáceis e não exige um segundo fator de autenticação para validar os acessos, facilitando técnicas de adivinhação e força bruta[cite: 21, 22].

---

### 📌 Estágio VI: Modelagem de Ataque (Attack modeling)
Mapeamos a correlação entre os ativos (dados dos usuários), os vetores de ataque e as vulnerabilidades em uma árvore de ataque simplificada baseada nas descobertas anteriores[cite: 21, 22]:

*   **Comprometer Dados do Usuário (User Data)**[cite: 22]
    *   **Via Injeção de SQL (SQL Injection):** Facilitado pela **Falta de Declarações Preparadas** no banco de dados[cite: 22].
    *   **Via Sequestro de Sessão (Session Hijacking):** Facilitado por **Credenciais de Login Fracas** ou sem proteções adicionais[cite: 22].

---

### 📌 Estágio VII: Análise de Risco e Impacto / Controles de Segurança (Risk analysis and impact)
Para conter as ameaças e corrigir as vulnerabilidades levantadas ao longo do PASTA, determinei a implementação de quatro controles de segurança fundamentais antes de autorizar o lançamento do app[cite: 21]:
1.  **Prepared Statements (Declarações Preparadas):** Obrigatoriedade no desenvolvimento do código para neutralizar qualquer tentativa de injeção de SQL nos formulários[cite: 21, 22].
2.  **Autenticação Multifator (MFA):** Bloqueia logins não autorizados, mitigando os riscos de vazamentos de credenciais ou sequestro de sessões de compras[cite: 19, 21].
3.  **Criptografia Forte (AES e TLS):** Utilização do AES para guardar os dados confidenciais do banco de dados e TLS para blindar os dados de cartão de crédito e chaves de tráfego contra interceptação na rede[cite: 20, 21].
4.  **Hashing de senhas com SHA-256 e Salt:** Garantir que as senhas fiquem salvas no banco de dados apenas em formato de resumos criptográficos irreversíveis, impedindo que acessos diretos exponham os segredos dos usuários[cite: 21].
