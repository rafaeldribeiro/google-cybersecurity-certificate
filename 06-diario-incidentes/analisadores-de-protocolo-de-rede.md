# Atividade: Analisadores de protocolo de rede 🌐🔍

<details>
<summary>📸 link do material de apoio</summary>

[Diagram template.pdf](https://github.com/user-attachments/files/30059317/Diagram.template.pdf)

https://www.tcpdump.org/index.html#documentation

https://www.wireshark.org/docs/wsug_html/

</details>

## 📝 Descrição do projeto
Realizei uma pesquisa comparativa sobre os dois principais analisadores de protocolo do mercado: o **wireshark** e o **tcpdump**.

O objetivo deste projeto foi entender as particularidades de cada ferramenta, mapear suas diferenças de interface e usabilidade, identificar suas semelhanças técnicas e entender quando e por que utilizar cada uma no cotidiano de um analista de segurança.

---

## 🛠️ Análise detalhada das ferramentas

### 🔵 wireshark
O Wireshark é conhecido como o analisador de rede visual mais popular do mundo.
*   **Interface gráfica (GUI):** Diferente de ferramentas de terminal, o Wireshark oferece uma interface cheia de recursos visuais, onde os pacotes de rede são organizados em linhas coloridas (por exemplo, pacotes com erro ou alertas aparecem em vermelho ou preto por padrão). Isso facilita a identificação visual de problemas.
*   **Análise pofunda e interativa:** Ele permite que o analista clique em um pacote específico e desmonte toda a sua estrutura (cabeçalhos de Ethernet, IP, TCP, etc.) de forma expansível com apenas alguns cliques, além de permitir seguir o fluxo para ler conversas inteiras que passaram pela rede em texto legível.

### 🟢 tcpdump
O tcpdump é o analisador padrão para ambientes de linha de comando.
*   **Interface de linha de comando (CLI):** Ele roda inteiramente no terminal do Linux. Não possui janelas ou botões. Toda a filtragem e exibição são feitas através de comandos digitados no teclado.
*   **Baixo consumo de tecursos:** Por não ter interface gráfica, o tcpdump é extremamente leve e rápido. Ele é ideal para ser executado diretamente em servidores remotos de produção ou roteadores onde não é permitido ou não é possível instalar programas pesados com interface visual.

---

## Semelhanças entre as Ferramentas

Apesar de parecerem muito diferentes por fora, por dentro elas compartilham o mesmo DNA

1.  **Open-source:** Ambas as ferramentas são gratuitas, possuem código-fonte aberto e são mantidas por comunidades globais ativas de desenvolvedores, sendo padrões de mercado em qualquer empresa do mundo.
2.  **Mesmo formato de arquivo:** Ambas utilizam e compreendem a biblioteca de captura de pacotes padrão. Isso significa que você pode usar o comando leve do `tcpdump` para capturar o tráfego de um servidor e salvar em um arquivo `.pcap`, e depois abrir esse mesmo arquivo no `Wireshark` do seu computador de trabalho para analisar os gráficos com calma.
3.  **Filtragem de tráfego:** Ambas permitem aplicar filtros de captura e de exibição para limpar o ruído da rede. Seja no terminal ou na tela colorida, o analista consegue filtrar para ver apenas tráfego de um IP específico, de uma porta como a porta 80 do HTTP ou de um protocolo como o ICMP.

---

## 🏁 Resumo do projeto
Pesquisar essas ferramentas me fez compreender que a escolha entre Wireshark e tcpdump depende do contexto operacional. Se preciso auditar um servidor em nuvem sem interface gráfica ou fazer uma captura rápida sem comprometer o desempenho da máquina, uso o **tcpdump**. Se preciso investigar um tráfego complexo, analisar cabeçalhos detalhadamente ou apresentar relatórios visuais para a gerência, o **Wireshark** é a escolha ideal. Dominar as duas ferramentas expande de forma gigantesca a caixa de ferramentas de qualquer analista de segurança de rede.
