# Atividade: Analisar a comunicação na camada de rede 🌐

## 📝 Apresentação do Projeto
Este projeto faz parte do Curso 3 (**Conectar e Proteger: Redes e Segurança de Redes**) do Certificado Profissional de Cybersecurity do Google. Como estudante do 2º semestre de Segurança da Informação, este é o meu registro prático de análise de pacotes brutos utilizando a ferramenta **tcpdump**.

No cenário desta atividade, o site de receitas `www.yummyrecipesforme.com` ficou indisponível para os clientes. Minha missão foi inspecionar os logs de tráfego para entender qual protocolo falhou e gerar o relatório técnico de incidente abaixo.

---

## 📂 Evidências do Incidente (Dados Brutos)
*Clique na caixa abaixo para verificar os registros capturados no terminal durante a investigação.*

<details>
<summary>🔍 Visualizar Logs do tcpdump</summary>

```text
13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 254

13:26:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:27:15.934126 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 320

13:28:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:28:50.0
