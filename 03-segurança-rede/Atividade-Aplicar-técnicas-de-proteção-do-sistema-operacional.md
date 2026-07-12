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

## 📂 Materiais de apoio e evidências do caso
*Clique nas caixas abaixo para expandir e ler a documentação.*

<details>
<summary>📋 1. O enário completo da invasão (Contexto)</summary>

### Descrição do ataque:
Um ex-funcionário insatisfeito realizou um ataque de força bruta contra o painel de administração da hospedagem do site `yummyrecipesforme.com`. Como a conta administrativa ainda utilizava a senha padrão de fábrica, o hacker conseguiu adivinhar a credencial após várias tentativas automáticas.

### Ação maliciosa:
* Após efetuar o login, o atacante alterou o código-fonte do site inserindo uma função maliciosa em JavaScript.
* Essa função induzia os visitantes a baixar um arquivo falso sob o pretexto de "atualizar o navegador" ou acessar "receitas gratuitas".
* O script modificava o comportamento do navegador, redirecionando o tráfego dos clientes reais para um domínio malicioso controlado pelo atacante: `greatrecipesforme.com`.
* Para finalizar, o invasor alterou a senha mestra de administração, bloqueando o acesso do proprietário legítimo.

### Descoberta do incidente:
Vários clientes enviaram e-mails ao suporte reclamando de lentidão nos computadores após executarem o arquivo do site. O dono da empresa tentou logar para investigar, mas percebeu que havia sido bloqueado, e imediatamente comunicou o time de analistas de segurança.
</details>

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
