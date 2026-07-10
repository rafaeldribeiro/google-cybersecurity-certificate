# Atividade: Analisar ataques à rede de computadores

## 📝 Apresentação da atividade
Este projeto prático faz parte do Curso 3 (**Conectar e proteger: redes e segurança de redes**) do curso cybersecurity do google.

O objetivo deste trabalho foi inspecionar o tráfego do servidor web afetado, descobrir o mecanismo do ataque que gerou a queda do sistema e preencher o relatório técnico oficial exigido pela gerência.

---

## 📂 Materiais de apoio integrados
*Clique na caixa abaixo para ler o resumo.*

<details>
<summary>📊 Estatísticas e detalhes da captura do tráfego</summary>

### 💻 Identificação dos endereços IP:
*   **192.0.2.1:** IP do servidor Web da nossa empresa.
*   **203.0.113.0:** IP de origem desconhecida.
*   **Rede 198.51.100.0/24:** Faixa de IPs dos computadores dos nossos funcionários legítimos.
*   **Porta de Destino 443:** Porta do servidor usada para tráfego web seguro e criptografado.

### 📉 Comportamento do Servidor no Log:
*   **Início (itens 52 a 54):** O servidor responde inicialmente ao atacante de forma padrão.
*   **Sobrecarga (itens 73 a 80):** O tráfego legítimo dos funcionários (como os IPs `198.51.100.5` e `198.51.100.7`) começa a falhar, gerando erros de **HTTP 504 Gateway Time-out** e pacotes de reset **[RST, ACK]**
*   **Paralisação Total (do item 125 ao 214):** O servidor web esgotou seus recursos, para de responder a parte exterior e a captura registra apenas a inundação de pacotes vinda do atacante.
</details>

---

## 📄 Relatório de Incidente de Segurança Cibernética

### 🔍 Seção 1: O tipo de ataque que pode ter causado esta interrupção na rede.

*   **Explicação para a mensagem de erro do tempo limite de conexão do site:** 
    A ocorrência de um ataque de Negação de Serviço (DoS) a nível de rede, especificamente uma inundação de solicitações conhecida como **SYN flood attack**
*   **Os registros mostram que:** 
    Um único endereço de IP externo e não autorizado (`203.0.113.0`) começou a bombardear de forma contínua e repetitiva a porta de serviços web (`443`) do nosso servidor (`192.0.2.1`) com pacotes do tipo `[SYN]`, sem nunca finalizar o processo de comunicação esperado.
*   **Este evento poderia ser:** 
    Classificado estritamente como um ataque **DoS direto**. A planilha de monitoramento confirma que todo o tráfego está saindo de uma única máquina, diferenciando de um DDoS, que usaria múltiplos computadores espalhados pela internet para camuflar a ação.

---

### Seção 2: Como o ataque está causando o mau funcionamento do site.

#### Handshake de três vias do TCP
Quando os nossos funcionários ou visitantes comuns tentam carregar a página de vendas da agência, o protocolo TCP realiza um processo de conexão em três etapas obrigatórias.
1.  **SYN (Synchronize):** O navegador do funcionário envia um pacote inicial para o servidor dizendo "Olá, gostaria de sincronizar e abrir uma conexão com você na porta 443."
2.  **SYN, ACK (Synchronize-Acknowledge):** O nosso servidor recebe o pedido, separa uma parte da sua memória para aquela conexão e responde: "Olá! Eu aceito o seu pedido. Aqui estão as minhas informações, estou aguardando sua confirmação"
3.  **ACK (Acknowledge):** O computador do funcionário recebe o sinal e manda a resposta final: "Confirmado, estou entrando!". Com isso, a conexão é aberta e o site começa a carregar na tela.

#### A inundação de pacotes SYN
Quando o agente mal intencionado dispara milhares de pacotes `[SYN]` ao mesmo tempo a partir do IP `203.0.113.0`, ele quebra esse fluxo de propósito. O atacante faz o passo 1 (SYN), o nosso servidor executa o passo 2 (SYN, ACK) e gasta memória guardando o espaço daquela conexão. Porém, o atacante ignora o passo 3 e **nunca envia o pacote ACK de confirmação**. 

Como o servidor recebe centenas desses pedidos falsos por segundo, a fila de conexões pendentes enche a memória do sistema rapidamente.

#### 📉 O que os logs indicam
Os dados capturados revela o esgotamento completo da infraestrutura:
*   Os funcionários legítimos tentam se conectar, mas o servidor está ocupado demais esperando as respostas falsas do atacante.
*   Isso se traduz nos logs com as linhas amarelas de erro, os usuários recebem mensagens de **Gateway Time-out (504)** porque o servidor demora tanto para responder que os intermediários desistem, ou pacotes **[RST, ACK]** forçando a queda da tentativa de conexão.
*   A partir do **item de log nº 125**, a capacidade do servidor zera, ele para de responder completamente a qualquer tráfego legítimo, deixando nossa equipe de publicidade impossibilitada de trabalhar e gerando prejuízos comerciais para a agência.

#### 🛡️ Minhas Sugestões (opcional)
Como o bloqueio simples de IP feito no nosso firewall não segura o atacante por muito tempo se ele falsificar o endereço (IP spoofing), recomendo à gerência adotar.
1.  **SYN cookies:** Configurar o sistema operacional do servidor para usar SYN Cookies, o que impede que a memória seja gasta guardando espaço para conexões que não enviaram o ACK final.
2.  **Limitação de taxa:** Configurar o firewall de borda para limitar a quantidade de pacotes SYN que um único IP pode enviar por segundo.
3.  **Habilitação de IPS/WAF:** Ativar um sistema de prevenção de intrusão que identifique o padrão repetitivo de inundações TCP e bloqueie a atividade maliciosa antes que ela consuma a banda do servidor.
