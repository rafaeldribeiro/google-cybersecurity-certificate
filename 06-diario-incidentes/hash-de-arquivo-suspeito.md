# Atividade: Investigar hash de arquivo suspeito

## 📝 Descrição do projeto
Simulei a atuação de um analista de segurança nível 1 trabalhando no centro de operações de segurança de uma empresa de serviços financeiros.

O objetivo deste projeto foi investigar um alerta de download de arquivo suspeito no computador de um funcionário corporativo. A partir do hash SHA-256 do arquivo malicioso, utilizei a plataforma global de inteligência de ameaças **VirusTotal** para auditar a reputação do arquivo, extrair outros indicadores de comprometimento e mapear usando a estrutura da pirâmide da dor.


<details>
<summary>📸 link do material de apoio</summary>


[Pyramid of Pain.pdf](https://github.com/user-attachments/files/30060725/Pyramid.of.Pain.pdf)



</details>


---

## Linha do tempo do incidente
*   **13:11** - O funcionário da empresa recebe um e-mail contendo uma planilha eletrônica protegida por senha como anexo.
*   **13:13** - O colaborador digita a senha fornecida no corpo do e-mail, faz o download do arquivo e o executa com sucesso.
*   **13:15** - Uma série de arquivos executáveis **.exe** não autorizados é criada silenciosamente na máquina do usuário.
*   **13:20** - O Sistema de detecção de intrusão **IDS** da rede corporativa detecta a presença desses arquivos e dispara um alerta automático para a equipe do SOC.

---

## Relatório de Investigação

### O arquivo analisado é malicioso?
**Sim, o arquivo é altamente malicioso.**

### Justificativa
Ao submeter o hash SHA-256 (`54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b`) na caixa de busca do VirusTotal, a análise retornou uma ameaça.
*   **Proporção de detecção:** O arquivo foi sinalizado malicioso por mais de **55 dos 74 principais fornecedores de segurança** globais incluindo grandes nomes como Microsoft, Kaspersky, CrowdStrike e Symantec, que classificaram o arquivo como um cavalo de troia associado a família de malwares.
*   **Pontuação da comunidade:** A pontuação coletiva baseada nas contribuições da comunidade de analistas do VirusTotal foi negativa, reforçando a urgência da ameaça.
*   **Padrões de comportamento em sandbox:** Os relatórios de execução em sandbox mostraram que a planilha, ao ser aberta, executa um script em segundo plano (macro VBA) responsável por forçar o download e a injeção de arquivos executáveis não autorizados na pasta temporária da máquina infectada, batendo perfeitamente com a atividade relatada na linha do tempo.

---

## Indicadores de comprometimento na pirâmide da dor

Os Indicadores de comprometimento adicionais obtidos nas diferentes abas do VirusTotal foram mapeados na **pirâmide da dor**. Essa organização nos ajuda a visualizar o nível de dificuldade que causamos ao invasor ao bloquearmos cada recurso de ataque.


### 1. Valores de hash - *Nível: Fácil*
*   **IoC Adicional:** `MD5: 95583b6320a1df27f813bcfe3cbffdfd`
*   **Análise de defesa:** O hash identifica o arquivo. Ao bloquear esse hash de arquivo nos computadores e filtros de e-mail da clínica, foi impedido o arquivo idêntico que seja baixado de novo, embora o atacante consiga alterar facilmente um único caractere invisível no código para gerar um novo hash e contornar a assinatura.

### 2. Endereços IP - *Nível: Fácil*
*   **IoCs Adicionais:** `185.190.140.165` e `188.166.160.22`
*   **Análise de defesa:** São os endereços de servidores externos que o vírus tenta acessar na internet para baixar o malware completo.

### 3. Nomes de domínio - *Nível: Simples*
*   **IoCs adicionais:** `drb-holding.com` e `custom-minds.com`
*   **Análise de defesa:** São os endereços de rede que o vírus chama para fazer a ponte com o servidor de comando e controle. Bloquear esses domínios nos servidores DNS corporativos é uma excelente blindagem.

### 4. rede/host - *Nível: Chato*
*   **IoCs adicionais:** Criação de novos arquivos binários (.exe e .dll) ocultos na pasta temporária local `C:\Users\Public\`
*   **Análise de defesa:** São as marcas físicas que o vírus deixa na máquina após a execução. Monitorar e impedir a criação anormal de novos arquivos executáveis em pastas públicas de usuários ou em chaves do registro do sistema dificulta bastante a vida do hacker, pois alterar o funcionamento interno da escrita do vírus dá trabalho a ele.

### 5. Ferramentas - *Nível: Desafiador*
*   **IoCs adicionais:** Uso de comandos administrativos nativos do Windows, como `powershell.exe`, `cmd.exe` e `regsvr32.exe`
*   **Análise de defesa:** O malware abusa de ferramentas legítimas do sistema operacional para passar despercebido pelos antivírus. Bloquear ou aplicar políticas de restrição severas de script para o powerShell e prompt de comando em computadores de funcionários comuns do financeiro desarma a infraestrutura do atacante, exigindo que ele crie ferramentas próprias para executar o código.

### 6. TTPs - *Nível: Extremamente difícil*
*   **IoCs adicionais:** Técnicas do catálogo MITRE ATT&CK como **T1204.002 User Execution: Malicious Attachment** e **T1059.005 VBA Scripting**
*   **Análise de defesa:** Induzir um funcionário a abrir um e-mail fingindo ser um documento importante e convencer a digitar uma senha para rodar macros. Combater as TTPs por meio de firewalls de e-mail avançados, políticas de desativação total de macros VBA de fora da rede e treinamento frequente de conscientização força o atacante a reformular toda a sua operação de ataque do zero.
