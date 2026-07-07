# 🛡️ Auditoria Interna de TI — Botium Toys

## 📝 Apresentação do Projeto
Este projeto faz parte do meu aprendizado no Certificado Profissional de Cybersecurity do Google. Como estudante do 2º semestre de Segurança da Informação e trazendo minha bagagem prática de 2 anos trabalhando com segurança patrimonial física, analisei o cenário da **Botium Toys**. 

A empresa expandiu suas vendas online para o mercado internacional, mas a infraestrutura digital ficou vulnerável e sem um plano de crescimento claro. Utilizei as diretrizes do **NIST CSF** para mapear os ativos e preencher esta auditoria, avaliando o que está funcionando e o que precisa ser corrigido urgentemente para evitar ataques e multas pesadas.

---

## 📂 Materiais de Apoio e Contexto do Caso
*Instruções: Clique nas caixas abaixo para expandir e ler os documentos oficiais que usei como base para esta auditoria.*

<details>
<summary>📄 1. Cenário, Escopo e Relatório de Riscos da Empresa</summary>

### Sobre a Botium Toys
Uma pequena empresa dos EUA que desenvolve e vende brinquedos. Possui um escritório principal, vitrine e depósito físicos, mas seu e-commerce cresceu atraindo clientes globais (inclusive na União Europeia).

### Ativos sob responsabilidade da TI:
* Dispositivos de usuários (desktops, laptops, smartphones).
* Sistemas de comércio eletrônico, contabilidade e gestão de inventário.
* Sistemas legados (antigos e em fim de vida útil).
* Infraestrutura física (câmeras de vigilância, trancas, sistemas de incêndio).

### Resumo do Relatório de Riscos:
* **Pontuação de Risco:** 8/10 (Muito Alta).
* **Problema Principal:** A gestão de ativos é inadequada e a empresa não cumpre regulamentações internacionais de privacidade, correndo risco de multas severas.
</details>

<details>
<summary>📋 2. Categorias de Controles Analisados (Diretrizes NIST)</summary>

Para avaliar a empresa, os controles foram divididos em três categorias fundamentais:
1.  **Controles Administrativos (Humanos):** Políticas de senhas, princípio do privilégio mínimo e separação de funções.
2.  **Controles Técnicos (Tecnológicos):** Firewalls, Sistemas de Detecção de Intrusão (IDS), Criptografia e Backups.
3.  **Controles Físicos (Operacionais):** Fechaduras, sistemas de CFTV (câmeras) e prevenção de incêndios.
</details>

---

## 📊 Lista de Verificação de Controles e Conformidade

Abaixo está o levantamento minucioso dos controles que a empresa já possui e daqueles que precisam ser implementados imediatamente.

### 1. Avaliação de Controles de Segurança

| Controle | Implementado? | Minha Análise Prática (Visão de Estudante / Ex-Segurança Patrimonial) |
| :--- | :---: | :--- |
| **Privilégio Mínimo** | ❌ **Não** | Alto risco: todos os funcionários têm acesso irrestrito a dados internos e financeiros de clientes. |
| **Planos de Recuperação de Desastres** | ❌ **Não** | Se o sistema cair hoje, a empresa não tem um plano estruturado para voltar a funcionar. |
| **Políticas de Senha** | ❌ **Não** | A política existente é fraca e não exige critérios modernos de complexidade (como caracteres especiais). |
| **Separação de Funções** | ❌ **Não** | Não há divisão de tarefas administrativas, o que facilita erros humanos ou fraudes internas. |
| **Firewall** |  **Sim** | Ponto positivo: a TI configurou regras adequadas para bloquear tráfego indesejado na rede. |
| **Sistema de Detecção de Intrusão (IDS)** | ❌ **Não** | O firewall barra a entrada, mas não há um sistema para detectar se alguém já está circulando na rede de forma anômala. |
| **Cópias de Segurança (Backups)** | ❌ **Não** | Risco crítico: a empresa simplesmente não faz backups de seus dados vitais. |
| **Software Antivírus** |  **Sim** | A TI instala e monitora os antivírus regularmente nas máquinas da empresa. |
| **Monitoramento de Sistemas Legados** |  **Sim** | Os sistemas antigos são monitorados manualmente, mas falta uma rotina previsível e organizada. |
| **Criptografia** | ❌ **Não** | Gravíssimo: os dados dos cartões de crédito dos clientes são processados e salvos localmente sem criptografia. |
| **Sistema de Gerenciamento de Senhas** | ❌ **Não** | Sem uma ferramenta centralizada, os funcionários esquecem as senhas e sobrecarregam o suporte da TI. |
| **Fechaduras Físicas** |  **Sim** | Excelente: a loja, os escritórios e o depósito possuem trancas físicas suficientes. |
| **Circuito Fechado de Televisão (CFTV)** |  **Sim** | O monitoramento por câmeras de segurança física está atualizado e funcionando perfeitamente. |
| **Detecção e Prevenção de Incêndios** |  **Sim** | Alarmes e sprinklers físicos estão operando para proteger o estoque físico de brinquedos e servidores. |

---

### 2. Avaliação de Práticas de Conformidade

#### 💳 Padrão de Segurança de Dados da Indústria de Cartões de Pagamento (PCI DSS)
* **Somente usuários autorizados têm acesso às informações de cartão:** ❌ **Não.** Qualquer funcionário consegue visualizar esses dados atualmente.
* **Informações do cartão armazenadas em ambiente seguro:** ❌ **Não.** Estão expostas no banco de dados interno sem defesas adicionais.
* **Implementação de criptografia nos dados de transações:** ❌ **Não.** Não existe criptografia para proteger as transações e dados armazenados.
* **Adoção de políticas seguras de gerenciamento de senhas:** ❌ **Não.** As regras atuais de senhas são superficiais e fracas.

#### 🇪🇺 Regulamento Geral de Proteção de Dados (GDPR / RGPD)
* **Dados dos clientes da UE mantidos em sigilo e segurança:** ❌ **Não.** A falta de criptografia e o acesso livre violam a privacidade exigida pela UE.
* **Plano para notificar os clientes em até 72 horas em caso de violação:** **Sim.** A TI desenvolveu esse plano de comunicação com sucesso.
* **Garantir que os dados sejam devidamente classificados e inventariados:** ❌ **Não.** A gestão de ativos atual foi classificada como inadequada.
* **Cumprimento das políticas e processos de privacidade pela equipe:** **Sim.** Existem políticas e processos aplicados e documentados dentro do departamento de TI.

#### 🔐 Controles de Sistemas e Organizações (SOC tipo 1, SOC tipo 2)
* **Políticas de acesso do usuário estabelecidas:** ❌ **Não.** Não há controle de privilégios ou barreira de credenciais para as contas de usuários.
* **Dados sensíveis (PII/SPII) são confidenciais/privados:** ❌ **Não.** A falta de controle de privilégios expõe dados sensíveis de clientes a qualquer um.
* **A integridade dos dados é garantida de forma consistente:** **Sim.** A equipe de TI integrou com sucesso os controles de integridade dos dados.
* **Os dados está disponíveis apenas para indivíduos autorizados:** ❌ **Não.** Usuários não autorizados conseguem ler informações críticas do banco de dados.

---

## 💡 Recomendações e Exemplos Práticos para o Gerente de TI

A pontuação de risco atual da Botium Toys é **8 de 10**, o que coloca a continuidade do negócio em perigo. Para ajudar o gerente de TI a justificar os investimentos de segurança para a diretoria, estruturei **3 exemplos práticos** baseados na nossa auditoria:

### 📝 Exemplo 1: O Risco de Processar Cartões sem Criptografia (PCI DSS)
* **Cenário Atual:** Os cartões de crédito dos clientes internacionais são guardados no banco de dados local sem criptografia.
* **O Impacto:** Se um cibercriminoso invadir a rede, ele terá acesso direto aos números dos cartões em texto claro. Além do prejuízo financeiro aos clientes, a Botium Toys sofrerá sanções severas, perda do direito de operar com bandeiras de cartão e multas pesadíssimas por violar o padrão **PCI DSS**.
* **Solução Recomendada:** Implementar criptografia de ponta a ponta (dados em trânsito e em repouso) para que os dados fiquem ilegíveis caso sejam interceptados.

### 📝 Exemplo 2: A Ameaça de Não Ter Backups (Recuperação de Desastres)
* **Cenário Atual:** O gerenciamento de estoque, contabilidade e e-commerce rodam em servidores locais, mas a empresa não possui nenhuma rotina de backup dos dados críticos.
* **O Impacto:** No caso de um ataque de *Ransomware* (onde os criminosos sequestram e criptografam os arquivos do sistema) ou de uma falha física grave no servidor, a Botium Toys perderá todo o histórico de vendas, dados de clientes e controle de inventário. Sem backups, o e-commerce ficaria fora do ar por dias ou semanas, paralisando o faturamento global.
* **Solução Recomendada:** Desenvolver um plano de recuperação de desastres e automatizar backups diários criptografados salvos em um ambiente em nuvem isolado.

### 📝 Exemplo 3: A Vulnerabilidade do Acesso Generalizado (Privilégio Mínimo)
* **Cenário Atual:** Todos os funcionários da empresa possuem acesso livre aos dados armazenados internamente, incluindo dados fiscais e registros confidenciais.
* **O Impacto:** Um funcionário do depósito ou da recepção, por curiosidade ou engenharia social (phishing), pode comprometer sua conta pessoal. Como a conta dele tem acesso a tudo, o invasor ganha as chaves de todo o sistema da empresa imediatamente, ampliando drasticamente o estrago do ataque.
* **Solução Recomendada:** Aplicar o **Princípio do Menor Privilégio**. Modificar as permissões para que os funcionários acessem apenas as ferramentas e dados estritamente necessários para realizar suas funções diárias.

---

## ✏️ Respostas Oficiais da Atividade (Verificação do Curso)

* **Pergunta 1:** Você revisou o escopo, as metas e o relatório de Avaliação de risco? **Sim.**
* **Pergunta 2:** Você considerou os riscos para os clientes, funcionários e/ou recursos da Botium Toys com base nos controles...? **Sim.**
* **Pergunta 3:** Você revisou o documento de categorias de controle? **Sim.**
* **Pergunta 4:** Você selecionou "sim" ou "não" para cada controle listado? **Sim.**
* **Pergunta 5:** Você selecionou "sim" ou "não" para cada prática recomendada de conformidade? **Sim.**
