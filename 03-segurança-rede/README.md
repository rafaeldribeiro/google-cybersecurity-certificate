# Atividade: Analisar a comunicação na camada de rede

## 📝 Apresentação do Projeto
Este projeto faz parte do Curso 3 (**Conectar e Proteger: Redes e Segurança de Redes**) do Cybersecurity Google.

---

## 📂 Documentação e Contexto do Caso
*Clique na caixa abaixo para verificar o cenário e os registros brutos capturados que usei para a investigação.*

<details>
<summary>📄 <img width="906" height="452" alt="Captura de tela de 2026-07-09 21-14-44" src="https://github.com/user-attachments/assets/856b0f9e-d320-495f-8c62-0af0487c9ff0" /></summary>

<details>
<summary>🔍 Visualizar Logs do tcpdump e Cenário de Investigação</summary>

### O Sintoma do Incidente:
Vários clientes relataram que não conseguiram acessar o site da empresa `www.yummyrecipesforme.com` e viram o erro "porta de destino inalcançável" após esperar que a página carregasse.

### Registros Capturados (Log do tcpdump):
```text
13:24:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:24:36.098564 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 254

13:26:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:27:15.934126 IP 203.0.113.2 > 192.51.100.15: ICMP 203.0.113.2 udp port 53 unreachable length 320

13:28:32.192571 IP 192.51.100.15.52444 > 203.0.113.2.domain: 35084+ A? yummyrecipesforme.com. (24)
13:28:50.022967 IP 2
