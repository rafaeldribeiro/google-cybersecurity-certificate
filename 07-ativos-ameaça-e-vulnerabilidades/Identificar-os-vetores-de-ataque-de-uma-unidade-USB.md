# Atividade: Identificar os vetores de atque de uma unidade USB 💾⚠️

## 📝 Descrição do projeto
Analisei um incidente de risco físico e lógico, um pendrive corporativo encontrado caído no estacionamento do *Rhetorical Hospital*.

O objetivo deste relatório foi aplicar uma mentalidade de ataque para avaliar os perigos de vazamento de informações de identificação pessoal (PII), entender como um cibercriminoso usaria esses dados e sugerir controles técnicos, operacionais e gerenciais para mitigar ataques de **USB Baiting**.

<details>
<summary>📸 link do material de apoio</summary>

[Parking lot USB exercise.pdf](https://github.com/user-attachments/files/29989925/Parking.lot.USB.exercise.pdf)

<img width="1460" height="965" alt="img" src="https://github.com/user-attachments/assets/87766b1f-5e4b-47a6-806a-4f2eb6f388ca" />

</details>

---

## 📂 Relatório de análise do pendrive

### 🔍 Conteúdo do dispositivo
A unidade USB pertencente ao gerente de recursos humanos Jorge Bailey contém uma mistura altamente arriscada de arquivos pessoais e profissionais. Entre os itens encontrados, existem pastas com fotos de família e de animais de estimação, além de documentos corporativos confidenciais, como o cronograma de turnos de funcionários, cartas de contratação, orçamentos setoriais e o próprio currículo de Jorge. Manter esses arquivos armazenados juntos em um único dispositivo móvel expõe dados sensíveis do hospital e informações pessoais do funcionário ao mesmo tempo.

---

### 🚨 Mentalidade do Atacante
Um invasor que obtivesse acesso a esse pendrive poderia usar informações altamente pessoais, como a lista de casamento ou o currículo, para criar campanhas de engenharia social focadas como ataques de *spear phishing* contra Jorge ou seus familiares. Além disso, ter acesso às escalas de turnos e aos orçamentos de funcionários fornece ao criminoso um mapa detalhado da estrutura interna do hospital, revelando quem trabalha lá e permitindo planejar ataques lógicos ou físicos em horários de menor vigilância. Por fim, o próprio pendrive poderia ser usado de forma maliciosa em uma ação de *USB baiting*, onde o atacante insere um malware silencioso no dispositivo e o deixa no estacionamento esperando que um funcionário curioso o conecte a um computador interno do hospital para abrir uma porta de entrada *backdoor* na rede

---

### 🛡️ Análise de risco e mitigações
Para mitigar os riscos de ataques de *USB baiting*, o hospital deve implementar controles técnicos robustos, como o bloqueio lógico de portas USB em máquinas críticas da rede interna e a desativação da execução automática de mídias (recurso AutoRun). No nível operacional, o uso de ambientes virtuais isolados (sandboxes), exatamente como o que adotei nesta investigação, é indispensável para analisar mídias externas desconhecidas com total segurança. Além disso, do ponto de vista gerencial, campanhas periódicas de conscientização são necessárias para educar a equipe médica e administrativa a nunca conectar nenhum dispositivo encontrado em áreas públicas. Por fim, a organização deve formalizar uma política rígida que proíba a utilização de mídias de armazenamento pessoais para salvar arquivos de trabalho confidenciais.
