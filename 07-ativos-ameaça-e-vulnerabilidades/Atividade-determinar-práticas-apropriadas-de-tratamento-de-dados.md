# Atividade: Analisar vazamento de dados com base no rivilégio mínimo 🔐

## 📝 Descrição do Projeto
Analisei um incidente de vazamento de dados confidenciais de planos de negócios em uma empresa de tecnologia educacional.

O objetivo foi avaliar a falha operacional que permitiu o vazamento, revisar as diretrizes de controle de acesso do padrão **NIST SP 800-53: AC-6** e recomendar melhorias no gerenciamento de privilégios para evitar que incidentes semelhantes voltem a acontecer.














---

## 📂 Dados do incidente e análise de controles

### 🚨 Fatores que levaram ao vazamento
O vazamento de dados ocorreu devido a uma falha operacional humana combinada com a falta de controles automatizados de acesso, onde um gerente compartilhou uma pasta interna sigilosa e esqueceu de revogar as permissões da equipe após a reunião. Posteriormente, um representante de vendas ignorou os avisos e compartilhou acidentalmente o link da pasta completa com um parceiro externo, que acabou publicando as informações estratégicas nas redes sociais.

---

### 📋 Resumo sobre o NIST SP 800-53: AC-6
A diretriz NIST SP 800-53: AC-6 aborda diretamente o princípio do privilégio mínimo, estabelecendo que os usuários devem receber apenas o nível estritamente mínimo de acesso e autorização necessário para desempenhar suas funções. O foco dessa norma é forçar políticas e papéis de usuário que evitem que contas operem com privilégios acima dos objetivos reais do negócio, minimizando drasticamente a superfície de exposição e protegendo a privacidade das informações.

---

### 🛠️ Melhorias sugeridas
Com base nas recomendações de aprimoramento de controle do próprio framework do NIST, sugiro implementar duas medidas técnicas na plataforma de arquivos da empresa.
1.  **Revogar automaticamente o acesso a informações após um período de tempo:** Configurar o sistema de arquivos para revogar de forma automática o acesso de usuários a pastas compartilhadas após um tempo determinado (ex: expiração do link em 1 hora)
2.  **Restringir o acesso a recursos sensíveis com base na função do usuário.:** Restringir o acesso a recursos internos altamente confidenciais com base nas funções específicas de cada colaborador, garantindo que certos arquivos nunca fiquem acessíveis para setores que não necessitam deles.

---

### 💡 (Justificativa das recomendações
Essas duas melhorias reduzem de forma decisiva o risco de novos incidentes porque retiram o fator de esquecimento humano, já que os links temporários expiram de forma autônoma após o encerramento das reuniões.
