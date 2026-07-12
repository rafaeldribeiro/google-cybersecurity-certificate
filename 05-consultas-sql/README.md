# Atividade: Aplicar filtros a consultas SQL 🗄️

## 📝 Descrição do projeto
Neste projeto de portfólio, assumi o papel de analista de segurança para investigar possíveis incidentes de acesso e mapear vulnerabilidades em ativos usando a linguagem SQL. Através da filtragem de dados nas tabelas estruturadas de funcionários (`employees`) e de tentativas de acesso (`log_in_attempts`), executei consultas focadas em isolar comportamentos incomuns (como logins fora do horário e acessos vindos do exterior) e identificar máquinas que necessitavam de correções críticas de segurança.

<details>
<summary>📸 links dos materiais de apoio</summary>

[Apply filters to SQL queries.pdf](https://github.com/user-attachments/files/29933124/Apply.filters.to.SQL.queries.pdf)

[Instructions for including SQL queries.pdf](https://github.com/user-attachments/files/29933120/Instructions.for.including.SQL.queries.pdf)

[Table formats.pdf](https://github.com/user-attachments/files/29933115/Table.formats.pdf)

</details>

---

## 🛠️ Consultas e análises realizadas

### 1. Recuperar tentativas de login com falha Após o horário
Para investigar acessos suspeitos fora do expediente comercial, filtrei os registros da tabela `log_in_attempts` para isolar todas as falhas ocorridas após as 18:00:

```sql
SELECT * 
FROM log_in_attempts 
WHERE login_time > '18:00:00' AND success = FALSE;
