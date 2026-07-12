# Atividade: Analisar a comunicação na camada de rede 🌐

## 📝 Apresentação da atividade
Este foi o meu primeiro contato prático com análise de pacotes brutos usando a ferramenta **tcpdump**.

No cenário desta atividade, o site de receitas `www.yummyrecipesforme.com` ficou indisponível para os clientes. Minha missão foi inspecionar os logs de tráfego para entender qual protocolo falhou e gerar o relatório técnico de incidente abaixo.

<details>
<summary>📸 Clique aqui para visualizar o print</summary>

[Cybersecurity incident report network traffic analysis.pdf](https://github.com/user-attachments/files/29946224/Cybersecurity.incident.report.network.traffic.analysis.pdf)


<img width="906" height="452" alt="Captura de tela de 2026-07-09 21-14-44" src="https://github.com/user-attachments/assets/c3b5f0e1-9d03-479d-ad44-bdbf2c43de51" />

</details>

---

### 📄 Relatório de incidente

**parte 1:** Resumo do problema encontrado nos logs de tráfego DNS e ICMP

O protocolo UDP revela que o computador do cliente IP de origem `192.51.100.15` tentou enviar uma consulta DNS legítima (solicitando o registro "A" do domínio yummyrecipesforme.com) direcionada ao servidor DNS da empresa IP de destino `203.0.113.2` utilizando a porta de destino padrão de serviços de rede `.domain`

A análise é baseada nos resultados da rede, que mostram que o servidor de destino respondeu com um pacote ICMP com a mensagem de erro: `udp port 53 unreachable.`

A porta anotada na mensagem de erro **Porta 53** é normalmente usada para o serviço de **DNS**, que traduz os nomes de sites em endereços IP legíveis para as máquinas.

O problema mais provável aqui é que o serviço de DNS no servidor de destino está **desativado/caído**, ou existe um firewall bloqueando especificamente as requisições UDP que tentam entrar por essa porta, impedindo que o navegador descubra o IP do site para abrir a página via HTTPS.

---

**parte 2:** Análise detalhada dos dados e causa provável

**Horário em que o incidente ocorreu:** O problema foi registrado em tempo real entre **13:24:32** e **13:28:50**
**Como a equipe de TI ficou sabendo do incidente:** Vários clientes externos começaram a abrir chamados relatando que o site de receitas não carregava.
**Ações tomadas pelo departamento de TI para investigar o caso:** Para descobrir em qual camada da rede estava a falha, rodamos o analisador de protocolos de rede `tcpdump` forçava uma nova requisição do site. Isso permitiu capturar o tráfego exato que passava pelas interfaces de rede no momento do erro.
**Principais descobertas da investigação da TI:** O computador de teste dispara requisições via protocolo UDP para o servidor de DNS `203.0.113.2` na porta 53.
**Causa mais provável do incidente:** O software do servidor DNS parou de funcionar ou uma atualização recente nas regras de firewall acabou bloqueando acidentalmente a porta 53 UDP. Sem o serviço rodando ou acessível, nenhuma máquina consegue traduzir o nome do site para o IP correto.

---

## 📂 Evidências do Incidente
*Clique na caixa abaixo para verificar os registros capturados no terminal durante a investigação.*

<details>
<summary>🔍 Visualizar logs do tcpdump</summary>

```text
13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 254

13:26:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:27:15.934126 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 320

13:28:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:28:50.022967 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 150
