# Atividade: Analisar a comunicação na camada de rede

## 📝 Apresentação do Projeto
Este projeto faz parte do Curso 3 (**Conectar e Proteger: Redes e Segurança de Redes**) do Certificado Profissional de Cybersecurity do Google. Como estudante do 2º semestre de Segurança da Informação, este é o meu portfólio prático de análise de pacotes brutos usando a ferramenta **tcpdump** dentro da pasta `03-seguranca-rede`.

---

## 📂 Documentação e Contexto do Caso
*Clique na caixa abaixo para verificar o cenário e os registros brutos capturados que usei para a investigação.*

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
