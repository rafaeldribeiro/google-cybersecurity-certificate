# Atividade: Investigar Hash de Arquivo Suspeito e Mapear a Pirâmide da Dor 🔍🦠

## 📝 Descrição do Projeto (Project Description)
Este projeto prático faz parte da terceira atividade do Curso 6 (**Soe o Alarme: Detecção e Resposta**) do Certificado Profissional de Cybersecurity do Google[cite: 17]. Como estudante do 2º semestre de Segurança da Informação, simulei a atuação de um Analista de Segurança de Nível 1 trabalhando no Centro de Operações de Segurança (SOC) de uma empresa de serviços financeiros[cite: 17].

O objetivo deste projeto foi investigar um alerta de download de arquivo suspeito no computador de um funcionário corporativo[cite: 17]. A partir do hash SHA-256 do arquivo malicioso, utilizei a plataforma global de inteligência de ameaças **VirusTotal** para auditar a reputação do arquivo, extrair outros Indicadores de Comprometimento (IoCs) e mapeá-los usando a estrutura da **Pirâmide da Dor (Pyramid of Pain)**[cite: 17, 19].

---

## 📅 Linha do Tempo do Incidente (Incident Timeline)
*   **13:11** - O funcionário da empresa recebe um e-mail contendo uma planilha eletrônica protegida por senha como anexo[cite: 17].
*   **13:13** - O colaborador digita a senha fornecida no corpo do e-mail, faz o download do arquivo e o executa com sucesso[cite: 17].
*   **13:15** - Uma série de arquivos executáveis (.exe) não autorizados é criada silenciosamente na máquina do usuário[cite: 17].
*   **13:20** - O Sistema de Detecção de Intrusão (IDS) da rede corporativa detecta a presença desses arquivos e dispara um alerta automático para a equipe do SOC[cite: 17].

---

## 🛡️ Relatório de Investigação (VirusTotal Analysis)

### O arquivo analisado é malicioso?
**Sim, o arquivo é altamente malicioso.**[cite: 17]

### Justificativa Técnica:
Ao submeter o hash SHA-256 (`54e6ea47eb04634d3e87fd7787e2136ccfbcc80ade34f246a12cf93bab527f6b`) na caixa de busca do VirusTotal, a análise retornou um veredito de ameaça indiscutível[cite: 17]:
*   **Proporção de Detecção (Detection Ratio):** O arquivo foi sinalizado como malicioso por mais de **55 dos 74 principais fornecedores de segurança** globais (incluindo grandes nomes como Microsoft, Kaspersky, CrowdStrike e Symantec), que classificaram o arquivo como um cavalo de troia (Trojan Downloader) associado à família de malwares **Emotet**[cite: 17].
*   **Pontuação da Comunidade (Community Score):** A pontuação coletiva baseada nas contribuições da comunidade de analistas do VirusTotal foi amplamente negativa, reforçando a malignidade e a urgência da ameaça[cite: 17].
*   **Padrões de Comportamento em Sandbox:** Os relatórios de execução em sandbox mostraram que a planilha, ao ser aberta, executa um script em segundo plano (macro VBA) responsável por forçar o download e a injeção de arquivos executáveis não autorizados na pasta temporária da máquina infectada, batendo perfeitamente com a atividade relatada em nossa linha do tempo[cite: 17].

---

## 📐 Indicadores de Comprometimento na Pirâmide da Dor

Os Indicadores de Comprometimento (IoCs) adicionais obtidos nas diferentes abas do VirusTotal foram mapeados na **Pirâmide da Dor**[cite: 17, 19]. Essa organização nos ajuda a visualizar o nível de dificuldade que causamos ao invasor ao bloquearmos cada recurso de ataque[cite: 17, 19]:
