# Projeto de portfólio: Rresponder a Iincidentes com a estrutura NIST CSF 🛡️

## 📝 Apresentação do projeto
Este é o meu projeto final do Curso 3 (**Conectar e Proteger: Redes e Segurança de Redes**) do curso cybersecurity do google. Utilizei a estrutura do **NIST CSF** para analisar e organizar a resposta a um ataque de rede sofrido por uma empresa de multimídia.

O objetivo deste relatório é documentar o incidente demonstrando como mapear um ataque de negação de serviço (DoS) dentro das 5 funções principais de segurança da informação.









---

## 📄 Relatório de análise de incidente

### 📋 1. Resumo do evento
Recentemente, nossa agência de multimídia sofreu um ataque do tipo **DoS (Negação de Serviço)** por inundação de pacotes ICMP. Um criminoso explorou um firewall que estava totalmente desconfigurado para sobrecarregar nossa infraestrutura. O impacto foi a paralisação completa da nossa rede interna por duas horas, impedindo o tráfego normal de acessar qualquer recurso. O incidente foi contido bloqueando os pacotes ICMP maliciosos e isolando os serviços.

---

### 🔍 2. As 5 funções do NIST CSF

#### 🔹 Identificar
*   **O que aconteceu:** Ataque DoS via inundação (flood) de pacotes de ping ICMP.
*   **Ativos afetados:** A rede interna da empresa e o servidor de conectividade.
*   **Vulnerabilidade encontrada:** O firewall da empresa estava sem nenhuma configuração de segurança ativa, deixando as portas abertas.
*   **Impacto no negócio:** Duas horas de indisponibilidade total dos serviços de rede.

#### 🔹 Proteger
Para blindar a rede contra novos ataques parecidos, implementamos duas defesas no firewall.
*   **Limitação de taxa:** Nova regra que controla e limita a quantidade de pacotes ICMP que podem entrar na rede por segundo.
*   **Filtro contra IPs falsificados (Anti-Spoofing):** Sistema de verificação para checar se o endereço IP de origem dos pacotes é verdadeiro.

#### 🔹 Detectar
Para descobrir ataques mais rápido no futuro, instalamos duas ferramentas de monitoramento
*   **Software de monitoramento de rede:** Sistema configurado para emitir alertas automáticos sempre que o volume de tráfego subir de forma anormal.
*   **Sistema IDS/IPS:** Uma ferramenta de detecção e prevenção de intrusão para analisar características suspeitas nos pacotes ICMP para bloquear antes que cheguem ao servidor.

#### 🔹 Responder
A estratégia usada pela equipe de gerenciamento de incidentes para conter o ataque.
*   Bloqueio imediato da entrada de todos os pacotes ICMP no firewall de borda.
*   Isolamento da rede, deixando todos os serviços não críticos temporariamente offline para diminuir o uso de memória da máquina.
*   Análise posterior dos registros de tráfego para aplicar as melhorias no firewall.

#### 🔹 Recuperar
O plano de ação para restaurar a normalidade da agência envolveu.
*   Priorização e restabelecimento imediato dos serviços de rede considerados críticos para o funcionamento do negócio.
*   Retorno dos serviços secundários (não críticos) depois da estabilização e configuração das novas barreiras do firewall.
