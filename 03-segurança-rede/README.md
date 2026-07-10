# 🌐 Análise de Tráfego de Rede: Incidente de DNS e ICMP

## 📝 Apresentação do Projeto
Este projeto faz parte do Curso 3 (**Conectar e Proteger: Redes e Segurança de Redes**) do Certificado Profissional de Cybersecurity do Google. Como estudante do 2º semestre de Segurança da Informação, este foi o meu primeiro contato prático com análise de pacotes brutos usando a ferramenta **tcpdump**.

No cenário analisado, os clientes da empresa relataram que não conseguiam acessar o site de receitas `www.yummyrecipesforme.com`. Minha missão como analista foi inspecionar os logs de tráfego de rede para entender qual protocolo falhou e qual a possível causa dessa indisponibilidade.

---

## 📂 Evidências do Incidente (Dados do Caso)
*Clique na caixa abaixo para verificar o cenário e os registros brutos coletados durante a investigação.*

<details>
<summary>🔍 <img width="906" height="452" alt="Captura de tela de 2026-07-09 21-14-44" src="https://github.com/user-attachments/assets/0b5f7777-7a22-4421-bbd7-5cef8522cd99" /> </summary>

### O Sintoma:
Os usuários tentavam carregar a página e recebiam um erro de "porta de destino inalcançável" após um longo tempo de espera. O mesmo erro aconteceu quando tentei acessar o site do meu navegador.

### Registros Capturados (Log do tcpdump):
```text
13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 254

13:26:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:27:15.934126 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 320

13:28:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:28:50.022967 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 150
