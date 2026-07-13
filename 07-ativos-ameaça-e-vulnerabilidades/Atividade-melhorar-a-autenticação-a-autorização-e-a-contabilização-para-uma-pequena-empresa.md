# Atividade: Melhorar a autenticação, autorização e contabilização 🔐

## 📝 Descrição do projeto
Neste projeto de portfólio, atuei como profissional de segurança cibernética contratado por uma empresa em crescimento que quase sofreu um desvio financeiro na folha de pagamento. Meu objetivo foi auditar os logs de eventos do sistema operacional.


<details>
<summary>📸 links dos materiais de apoio</summary>

[Accounting exercise.xlsx](https://github.com/user-attachments/files/29979147/Accounting.exercise.xlsx)

[Access control worksheet.pdf](https://github.com/user-attachments/files/29979140/Access.control.worksheet.pdf)


</details>

---

## 📂 Auditoria e cruzamento de dados
*Instruções: Clique na caixa abaixo para verificar os dados  que ligaram o log do incidente.*

<details>
<summary>📊 Evidências do caso</summary>

### 🚨 Registro do incidente
*   **Data/Hora:** 10/03/2023 às 8:29:57 AM
*   **Usuário:** `Legal\Administrator`
*   **Dispositivo/IP:** Nome do computador `Up2-NoGud` / IP `152.207.255.255`
*   **Ação:** Evento de folha de pagamento adicionado para banco desconhecido `FAUX_BANK`

### 👤 Cadastro no diretório
*   **Funcionário:** Robert Taylor Jr.
*   **Cargo:** Advogado Contratado
*   **IP registrado:** `152.207.255.255` 
*   **Último acesso informado:** `8:29:57 am (5 days ago)`
*   **Data de término do contrato:** 27/12/2019.
</details>

---

## Planilha de controles de acesso

Abaixo está o preenchimento técnico do relatório seguindo o modelo exigido pela equipe de segurança cibernética.

### Notas
*   **Observação 1:** O incidente foi causado através do endereço IP `152.207.255.255` utilizando uma conta administrativa padrão `Legal\Administrator` a partir de uma máquina com o nome "Up2-NoGud"
*   **Observação 2:** O cruzamento de dados prova que o acesso foi efetuado por Robert Taylor Jr cujas credenciais e endereço de rede ainda estavam ativos no sistema mesmo ele tendo sido desligado oficialmente da organização no dia 27/12/2019

---

### Problema
*   **Problema 1 (Ausência de processo de desativação):** A empresa falhou gravemente no controle operacional de desligamento. Contas de prestadores de serviço temporários e sazonais continuavam totalmente ativas e operacionais anos após o fim dos seus contratos.
*   **Problema 2 (Excesso de privilégios gerais):** Não existsia do princípio do privilégio mínimo. O diretório aponta que 100% dos funcionários (incluindo designers, contratados externos e funcionários sazonais) possuíam nível de privilégio configurado como **Admin**, permitindo que qualquer conta alterasse dados críticos da folha de pagamento.

---

### Recomendação
*   **Recomendação 1 (Política de offboarding automatizada):** Implementar um controle gerencial e operacional rígido que obrigue a revogação imediata de todas as contas, e-mails e permissões de qualquer colaborador ou terceiro no exato dia de encerramento do seu contrato ou demissão.
*   **Recomendação 2 (Controle de acesso baseado em funções - RBAC):** Aplicar o princípio do menor privilégio. A autorização de nível "Admin" deve ser restrita apenas ao proprietário e analistas de segurança. O acesso de gravação e alteração na folha de pagamento deve ser restrito exclusivamente ao gerente financeiro, deixando os demais funcionários apenas com acessos básicos necessários para suas tarefas.
