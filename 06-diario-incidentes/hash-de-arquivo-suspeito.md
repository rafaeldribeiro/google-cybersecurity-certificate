# Atividade: Investigar hash de arquivo suspeito

## 📝 Descrição do Projeto
Simulei a atuação de um analista de segurança de Nível 1 trabalhando no centro de operações de segurança (SOC) de uma empresa de serviços financeiros.

O objetivo deste projeto foi investigar um alerta de download de arquivo suspeito no computador de um funcionário corporativo. A partir do hash SHA-256 do arquivo malicioso, utilizei a plataforma global de inteligência de ameaças **VirusTotal** para auditar a reputação do arquivo, extrair outros indicadores de comprometimento (IoCs) e mapear usando a estrutura da **Pirâmide da Dor.





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
Ao submeter o hash SHA-256 (`54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b`) na caixa de busca do VirusTotal, a análise retornou um veredito de ameaça indiscutível
*   **Proporção de detecção:** O arquivo foi sinalizado como malicioso por mais de **55 dos 74 principais fornecedores de segurança** globais incluindo grandes nomes como Microsoft, Kaspersky, CrowdStrike e Symantec, que classificaram o arquivo como um cavalo de troia associado a família de malwares.
*   **Pontuação da comunidade:** A pontuação coletiva baseada nas contribuições da comunidade de analistas do VirusTotal foi negativa, reforçando a urgência da ameaça.
*   **Padrões de comportamento em sandbox:** Os relatórios de execução em sandbox mostraram que a planilha, ao ser aberta, executa um script em segundo plano (macro VBA) responsável por forçar o download e a injeção de arquivos executáveis não autorizados na pasta temporária da máquina infectada, batendo perfeitamente com a atividade relatada em nossa linha do tempo.

---

## Indicadores de comprometimento na pirâmide da dor

Os Indicadores de comprometimento adicionais obtidos nas diferentes abas do VirusTotal foram mapeados na **Pirâmide da Dor**. Essa organização nos ajuda a visualizar o nível de dificuldade que causamos ao invasor ao bloquearmos cada recurso de ataque.
