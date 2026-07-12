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
```

A consulta avalia a tabela de acessos procurando por duas condições obrigatórias ao mesmo tempo graças ao operador AND. Ela checa se o horário na coluna login_time é maior que 18h e se o valor na coluna success é falso (FALSE ou 0), revelando possíveis tentativas noturnas de invasão por força bruta.

---

### 2. Recuperar tentativas de login em datas específicas
Para analisar a atividade de rede em torno de um evento suspeito que aconteceu no dia 09/05/2022, puxei os dados daquela data e do dia anterior.

```sql
SELECT * 
FROM log_in_attempts 
WHERE login_date = '2022-05-08' OR login_date = '2022-05-09';
```

Aqui utilizei o operador OR na coluna login_date. Dessa forma, o banco de dados me traz o histórico completo de acessos de ambos os dias, permitindo traçar uma linha do tempo para entender o comportamento do tráfego antes e durante o incidente.

---

### 3. Recuperar tentativas de login fora do México
O time determinou que o ataque recente não teve origem no México. Para investigar acessos vindos de outros países, usei o seguinte filtro.

```sql
SELECT * 
FROM log_in_attempts 
WHERE NOT country LIKE 'MEX%';
```

Usei o operador de exclusão NOT combinado com a palavra-chave LIKE e o caractere %. O padrão 'MEX%' instrui o SQL a ignorar qualquer registro que comece com essas letras, excluindo com uma única linha tanto a sigla "MEX" quanto o nome "MEXICO" presentes no banco, listando apenas as conexões internacionais.

---

### 4. Recuperar funcionários no departamento de marketing
Precisávamos aplicar atualizações de segurança específicas nos computadores do time de Marketing localizados em todo o prédio East (Ala Leste).

```sql
SELECT * 
FROM employees 
WHERE department = 'Marketing' AND office LIKE 'East%';
```

O operador AND garante que o funcionário pertença ao setor de marketing. Para rastrear os escritórios da Ala Leste, usei LIKE 'East%', mapeando automaticamente salas como East-170 ou East-320 sem precisar digitar cada código de sala manualmente.

---

### 5. Recuperar funcionários em finanças ou vendas
Para uma rotina de manutenção diferente voltada exclusivamente aos departamentos financeiro e comercial, executei a seguinte filtragem.

```sql
SELECT * 
FROM employees 
WHERE department = 'Finance' OR department = 'Sales';
```

Como um funcionário não pode trabalhar em dois setores ao mesmo tempo, o operador OR é a escolha correta. O SQL analisa a coluna department e agrupa em uma mesma lista os colaboradores que pertencem a qualquer uma dessas duas áreas.

---

### 6. Recuperar todos os funcionários que não estão em TI
Como a equipe de tecnologia da informação já tinha recebido a última vacina de segurança, precisei mapear todos os outros departamentos restantes para agendar a atualização.

```sql
SELECT * 
FROM employees 
WHERE NOT department = 'Information Technology';
```

Utilizei o operador NOT diretamente na coluna department. O banco de dados faz uma varredura e traz o cadastro de toda a empresa, exceto os profissionais de 'information technology', gerando a lista exata para a nossa equipe de suporte atuar.

---

### Resumo.
A utilização de consultas filtradas em SQL foi imporatnte para transformar milhares de linhas de logs em dados estratégicos e acionáveis. Dominar a combinação de operadores lógicos (AND, OR, NOT) e buscas por aproximação (LIKE) me permitiu auditar acessos suspeitos geograficamente, rastrear incidentes com precisão de data/horário e organizar de forma cirúrgica os patches de segurança nos ativos da organização, fortalecendo a governança e a segurança da informação.
