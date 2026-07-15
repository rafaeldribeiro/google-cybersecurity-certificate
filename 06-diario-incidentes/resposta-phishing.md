# Atividade: Atividade: Usar um manual para responder a um incidente de phishing

## 📝 Descrição do projeto
Mmeu objetivo foi guiar uma investigação de segurança seguindo estritamente as regras de um manual de resposta.

A investigação partiu de um alerta de segurança acionado no servidor de e-mails da empresa. Utilizei técnicas de análise de cabeçalho, detecção de erros gramaticais e validação de hashes criptográficos para confirmar a falsidade do e-mail e realizar o devido encaminhamento.


<details>
<summary>📸 link do material de apoio</summary>


[Alert ticket.pdf](https://github.com/user-attachments/files/30068136/Alert.ticket.pdf)

[Phishing incident response playbook.pdf](https://github.com/user-attachments/files/30068130/Phishing.incident.response.playbook.pdf)





</details>






---

## 🎫 Tíquete de alerta de segurança

Abaixo está o registro atualizado do tíquete de incidente de segurança no sistema.

| Campo do tíquete | Informações registradas no sistema |
| :--- | :--- |
| **Ticket ID** | A-2703 |
| **Mensagem de alerta** | SERVER-MAIL: Tentativa de phishing, possível download de malware|
| **Gravidade** | Média |
| **Ticket Status** | **encaminhado** |
| **Detalhes** | O usuário pode ter recebido um e-mail malicioso, aberto anexos ou clicado em links suspeitos |
| **Informações adicional** | **Hash malicioso verificado (SHA256):** `54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b` <br><br> **Dados brutos do e-mail interceptado:** <br> - **De (From):** Def Communications `<76tguyhh6tgftrt7tg.su>` (IP: `114.114.114.114`) <br> - **Para (To):** `<hr@inergy.com>` (IP: `176.157.125.93`) <br> - **Assunto:** `Re: Infrastructure Egnieer role` <br> - **Mensagem:** "Dear HR at Ingergy, I am writing for to express my interest in the engineer role posted from the website. There is attached my resume and cover letter. For privacy, the file is password protected. Use the password paradise10789 to open. <br> - **Anexo:** `filename="bfsvc.exe"` |

### 💬 Comentários e resolução do analista

> **Resumo do Caso:** Este alerta ID: `A-2703` foi acionado devido a detecção de uma possível tentativa de phishing com download de malware enviada ao e-mail corporativo do setor de Recursos Humanos.
>
> **Motivos de encaminhamento:** Optei por alterar o status do tíquete para **encaminhado** e enviar as informações para análise avançada de Nível 2 por três motivos críticos:
> 1. **Extensão de arquivo incoerente:** O remetente afirma enviar um currículo e carta de apresentação, mas o anexo possui a extensão executável `.exe` `bfsvc.exe`, que permite a execução direta de códigos maliciosos nos computadores locais caso seja aberto.
> 2. **Criptografia para burlar filtros:** O arquivo está protegido por senha (`paradise10789`) com a desculpa de manter a privacidade, tática clássica de atacantes para impedir que sistemas automáticos de varredura do firewall leiam e detectem ameaças dentro do arquivo.
> 3. **Remetente suspeito:** O e-mail apresenta erros sérios de escrita como ("Egnieer" e "Ingergy"), e o endereço do remetente utiliza o domínio `<76tguyhh6tgftrt7tg.su>`, que é totalmente suspeito.

---

## 📒 Diário do analista

Seguindo o processo exigido na **Etapa 5** do manual de conduta, registrei o incidente no diário de bordo para registrar a dinâmica dos fatos.

### 🔍 As 5 Perguntas

*   **Quem causou?**  
    Um atacante externo desconhecido, passando por um candidato para emprego chamado "Clyde West", utilizando o pseudônimo de e-mail "Def Communications".
*   **O que aconteceu?**  
    O invasor tentou induzir o setor de RH da empresa baixar e executar um malware hospedado dentro de um arquivo `.exe` disfarçado de currículo e protegido por senha.
*   **Quando ocorreu?**  
    O e-mail malicioso foi recebido na quarta-feira, dia 20 de julho de 2022, às `09:30:14`
*   **Onde ocorreu?**  
    O ataque teve como alvo a caixa de entrada do e-mail do setor de recursos humanos `hr@inergy.com`
*   **Por que ocorreu?**  
    O incidente ocorreu como parte de um ataque de phishing projetado para enganar funcionários do RH para que descarregassem e executassem um backdoor na rede corporativa.
