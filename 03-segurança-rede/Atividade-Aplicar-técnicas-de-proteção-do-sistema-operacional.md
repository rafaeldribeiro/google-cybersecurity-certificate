# Atividade: Aplicar técnicas de proteção do sistema operacional 🖥️

## 📝 Apresentação da atividade
Assumi o papel de analista de segurança para investigar uma invasão cibernética sofrida pelo site de culinária `yummyrecipesforme.com`.

O incidente envolveu uma quebra de credenciais de administrador por força bruta, alteração do código-fonte do servidor web e o redirecionamento malicioso de usuários legítimos para o download de um malware. Minha missão foi analisar os registros de rede obtidos via **tcpdump**, documentar o incidente e indicar uma medida de segurança eficiente para mitigar essa vulnerabilidade.

<details>
<summary>📸 links dos materiais de apoio</summary>

[Security incident report template.pdf](https://github.com/user-attachments/files/29902656/Security.incident.report.template.pdf)

[tcpdump traffic log.pdf](https://github.com/user-attachments/files/29902688/tcpdump.traffic.log.pdf)

[How to read the tcpdump traffic log.pdf](https://github.com/user-attachments/files/29902671/How.to.read.the.tcpdump.traffic.log.pdf)

</details>

---

### Seção 1:  Identificar o protocolo de rede envolvido no incidente

**1.** Identificado nos registros com o sufixo `dns.google.domain.` Esse protocolo foi utilizado no início do processo timestamp `14:18:32` para converter o endereço textual do site em um IP numérico legível para a rede `203.0.113.22`

**2.** Identificado no log pelo sufixo `.http` associado a porta padrão 80 e pela requisição explícita de dados `HTTP: GET / HTTP/1.1 às 14:18:36.` O HTTP foi o protocolo responsável por carregar a página web comprometida que continha a função JavaScript maliciosa e por iniciar o download do arquivo executável contendo o malware.

---

### Seção 2: Documentar o incidente

**Descrição do ataque:**
Um ex-funcionário insatisfeito realizou um ataque de força bruta contra o painel de administração da hospedagem do site `yummyrecipesforme.com`. Como a conta administrativa ainda utilizava a senha padrão de fábrica, o hacker conseguiu adivinhar a credencial após várias tentativas automáticas.

**Ação maliciosa:**
* Após efetuar o login, o atacante alterou o código-fonte do site inserindo uma função maliciosa em JavaScript.
* Essa função induzia os visitantes a baixar um arquivo falso sob o pretexto de "atualizar o navegador" ou acessar "receitas gratuitas".
* O script modificava o comportamento do navegador, redirecionando o tráfego dos clientes reais para um domínio malicioso controlado pelo atacante: `greatrecipesforme.com`.
* Para finalizar, o invasor alterou a senha mestra de administração, bloqueando o acesso do proprietário legítimo.

**Descoberta do incidente:**
Vários clientes enviaram e-mails ao suporte reclamando de lentidão nos computadores após executarem o arquivo do site. O dono da empresa tentou logar para investigar, mas percebeu que havia sido bloqueado, e imediatamente comunicou o time de analistas de segurança.

---

### Seção 3: Recomendar uma medida de remediação para ataques de força bruta

Medida recomendada: Implementação de autenticação de dois fatores (2FA) combinada com uma política de bloqueio de Cconta


<details>
<summary>🔍 2. Registro de Tráfego Capturado (Log tcpdump)</summary>

Estes são os registros coletados no ambiente isolado que serviram de evidência técnica para a análise:

```text
14:18:32.192571 IP your.machine.52444 > dns.google.domain: 35084+ A? yummyrecipesforme.com. (24)
14:18:32.204388 IP dns.google.domain > your.machine.52444: 35084 1/0/0 A 203.0.113.22 (40)
14:18:36.786501 IP your.machine.36086 > yummyrecipesforme.com.http: Flags [S], seq 2873951608, win 65495...
14:18:36.786517 IP yummyrecipesforme.com.http > your.machine.36086: Flags [S.], seq 3984334959, ack 2873951609...
14:18:36.786589 IP your.machine.36086 > yummyrecipesforme.com.http: Flags [P.], length 73: HTTP: GET / HTTP/1.1
...<a lot of traffic on the port 80>...
14:20:32.192571 IP your.machine.52444 > dns.google.domain: 21899+ A? greatrecipesforme.com. (24)
14:20:32.204388 IP dns.google.domain > your.machine.52444: 21899 1/0/0 Α 192.0.2.17 (40)
14:25:29.576493 IP your.machine.56378 > greatrecipesforme.com.http: Flags [S], seq 1020702883...
14:25:29.576590 IP your.machine.56378 > greatrecipesforme.com.http: Flags [P.], length 73: HTTP: GET / HTTP/1.1
