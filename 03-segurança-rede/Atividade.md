# Atividade: Analisar a comunicação na camada de rede 🌐

## 📝 Apresentação da atividade
Este projeto faz parte do curso 3 (**Conectar e proteger: redes e segurança de redes**) do curso cybersecurity do google. Este foi o meu primeiro contato prático com análise de pacotes brutos usando a ferramenta **tcpdump**.

No cenário desta atividade, o site de receitas `www.yummyrecipesforme.com` ficou indisponível para os clientes. Minha missão foi inspecionar os logs de tráfego para entender qual protocolo falhou e gerar o relatório técnico de incidente abaixo.

<details>
<summary>📸 Clique aqui para ver o print dos logs</summary>

<img width="906" height="452" alt="Captura de tela de 2026-07-09 21-14-44" src="https://github.com/user-attachments/assets/c3b5f0e1-9d03-479d-ad44-bdbf2c43de51" />

</details>

---

## 📂 Evidências do Incidente
*Clique na caixa abaixo para verificar os registros capturados no terminal durante a investigação.*

<details>
<summary>🔍 Visualizar Logs do tcpdump</summary>

```text
13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 254

13:26:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:27:15.934126 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 320

13:28:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:28:50.022967 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 150
