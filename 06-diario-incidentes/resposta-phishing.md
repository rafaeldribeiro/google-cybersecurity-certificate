# Atividade: Resposta a Incidente de Phishing com Uso de Playbook 🛡️📧

## 📝 Descrição do Projeto (Project Description)
Este projeto faz parte da quarta atividade prática do Curso 6 (**Soe o Alarme: Detecção e Resposta**) do Certificado Profissional de Cybersecurity do Google. Como estudante do 2º semestre de Segurança da Informação atuando como Analista de SOC Nível 1, meu objetivo foi guiar uma investigação de segurança seguindo estritamente as regras de um manual de resposta (Phishing Playbook v1.0)[cite: 21].

A investigação partiu de um alerta de segurança acionado no servidor de e-mails da empresa. Utilizei técnicas de análise de cabeçalho, detecção de erros gramaticais e validação de hashes criptográficos para confirmar a falsidade do e-mail e realizar o devido encaminhamento técnico (escalonamento) para os analistas de Nível 2 da equipe.

---

## 🎫 Tíquete de Alerta de Segurança (Completed Security Ticket)

Abaixo está o registro atualizado do tíquete de incidente de segurança no sistema do SOC da organização após a conclusão da minha análise:

| Campo do Tíquete | Informações Registradas no Sistema |
| :--- | :--- |
| **Ticket ID** | A-2703[cite: 20] |
| **Alert Message** | SERVER-MAIL: Phishing attempt, possible download of malware[cite: 20] |
| **Severity (Gravidade)** | Medium (Média)[cite: 20] |
| **Ticket Status** | **Escalated (Encaminhado)**[cite: 20, 21] |
| **Details (Detalhes)** | O usuário pode ter recebido um e-mail malicioso, aberto anexos ou clicado em links suspeitos[cite: 20]. |
| **Additional Information** | **Hash malicioso verificado (SHA256):** `54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b`[cite: 20] <br><br> **Dados brutos do e-mail interceptado:** <br> - **De (From):** Def Communications `<76tguyhh6tgftrt7tg.su>` (IP: `114.114.114.114`)[cite: 20] <br> - **Para (To):** `<hr@inergy.com>` (IP: `176.157.125.93`)[cite: 20] <br> - **Assunto:** `Re: Infrastructure Egnieer role`[cite: 20] <br> - **Mensagem:** "Dear HR at Ingergy, I am writing for to express my interest in the engineer role posted from the website. There is attached my resume and cover letter. For privacy, the file is password protected. Use the password paradise10789 to open."[cite: 20] <br> - **Anexo:** `filename="bfsvc.exe"`[cite: 20] |

### 💬 Ticket Comments (Comentários e Resolução do Analista)

> **Resumo do Caso:** Este alerta (ID: A-2703) foi acionado devido à detecção de uma possível tentativa de phishing com download de malware enviada ao e-mail corporativo do setor de Recursos Humanos[cite: 20]. 
>
> **Motivos de Encaminhamento (Escalonamento):** Optei por alterar o status do tíquete para **Escalated (Encaminhado)** e enviar as informações para análise avançada de Nível 2 por três motivos críticos[cite: 21]:
> 1. **Extensão de Arquivo Incoerente:** O remetente afirma enviar um currículo e carta de apresentação, mas o anexo possui a extensão executável `.exe` (`bfsvc.exe`)[cite: 20], que permite a execução direta de códigos maliciosos nos computadores locais caso seja aberto.
> 2. **Criptografia para Burlar Filtros:** O arquivo está protegido por senha (`paradise10789`) com a desculpa de manter a privacidade[cite: 20], tática clássica de atacantes para impedir que sistemas automáticos de varredura do firewall leiam e detectem ameaças dentro do arquivo.
> 3. **Erros Graves e Remetente Suspeito:** O e-mail apresenta erros sérios de escrita (como "Egnieer" e "Ingergy")[cite: 20], e o endereço do remetente utiliza o domínio `<76tguyhh6tgftrt7tg.su>` (sigla da extinta União Soviética)[cite: 20], que é totalmente suspeito e desconhecido. Além disso, o hash criptográfico do arquivo anexo já foi validado em investigações anteriores como malicioso (Emotet)[cite: 20].

---

## 📒 Diário de Bordo do Analista (Incident Handler's Journal)

Seguindo o processo exigido na **Etapa 5** do manual de conduta, registrei o incidente no diário de bordo para registrar a dinâmica dos fatos[cite: 21]:

### 🔍 As 5 Perguntas (The 5 W's)[cite: 21]

*   **Who caused the incident? (Quem causou?)**  
    Um atacante externo desconhecido, fazendo-se passar por um candidato a emprego chamado "Clyde West", utilizando o pseudônimo de e-mail "Def Communications"[cite: 20].
*   **What happened? (O que aconteceu?)**  
    O invasor tentou induzir o setor de RH da empresa a baixar e executar um malware hospedado dentro de um arquivo `.exe` disfarçado de currículo e protegido por senha[cite: 20].
*   **When did the incident occur? (Quando ocorreu?)**  
    O e-mail malicioso foi recebido na quarta-feira, dia 20 de julho de 2022, às 09:30:14 AM[cite: 20].
*   **Where did the incident happen? (Onde ocorreu?)**  
    O ataque teve como alvo a caixa de entrada do e-mail do setor de Recursos Humanos (`hr@inergy.com`)[cite: 20].
*   **Why did the incident happen? (Por que ocorreu?)**  
    O incidente ocorreu como parte de um ataque de engenharia social (phishing) projetado para enganar funcionários do RH para que descarregassem e executassem um backdoor na rede corporativa, aproveitando-se do fato de que o setor lida constantemente com o recebimento de currículos externos de candidatos[cite: 20].
