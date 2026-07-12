# Atividade: Gerenciar permissões de arquivos no linux 🐧



## 📝 Descrição do projeto
Neste projeto prático, assumi o papel de analista de segurança cibernética para auditar e ajustar as permissões de acesso do sistema de arquivos de uma equipe de pesquisa corporativa. Meu objetivo principal foi analisar se as trancas digitais dos arquivos estavam corretas e usar comandos nativos do terminal linux para remover acessos não autorizados, blindando o ambiente contra modificações indevidas.

<details>
<summary>📸 Links dos materiais de apoio</summary>

[Current file permissions.pdf](https://github.com/user-attachments/files/29932272/Current.file.permissions.pdf)

[Instructions for including Linux commands.pdf](https://github.com/user-attachments/files/29932269/Instructions.for.including.Linux.commands.pdf)

[File permissions in Linux.pdf](https://github.com/user-attachments/files/29932262/File.permissions.in.Linux.pdf)

</details>

---

## Verificar detalhes de arquivos e diretórios
Para listar todos os arquivos do diretório `/home/researcher2/projects`, incluindo os arquivos ocultos, e examinar as permissões atuais, utilizei o comando.

```bash
ls -la
```

---

## Descrever a cadeia de permissões

### 1º caractere 
(-): Indica o tipo do arquivo. O hífen significa que é um arquivo comum (se fosse a letra d, seria um diretório).

### 2º, 3º e 4º caracteres
(rw-): Permissões do dono. O usuário criador pode ler (r) e escrever/modificar (w), mas não pode executar (-).

## 5º, 6º e 7º caracteres
(ref): Permissões do grupo. Os membros do grupo de pesquisa podem apenas ler (r) o arquivo.

## 8º, 9º e 10º caracteres
(---): Permissões de terceiros (outros) Usuários externos não possuem nenhum tipo de acesso ao arquivo.

---

## Permissões de arquivos

## 1. Alterar permissões do arquivo comum.
A política da organização proíbe que usuários externos ("outros") tenha acesso de gravação/escrita a qualquer arquivo. Identifiquei que o `project_k.txt` violava essa regra. Usei o seguinte comando para remover a permissão de escrita de terceiros.

```Bash
chmod o-w project_k.txt
```

A string do arquivo mudou de `-rwxrwxrwx` para `-rwxrwxr-x`, garantindo a integridade dos dados contra alterações externas.

---

## 2. Alterar permissões em um arquivo oculto

O arquivo oculto `.project_x.txt` foi arquivado pela equipe. A nova diretriz exige que ninguém tenha permissão de escrita nele, mas o usuário e o grupo precisam conseguir ler o arquivo. Usei o comando `chmod` para definir essa política de leitura exclusiva `(r--r-----)`

```Bash
chmod 440 .project_x.txt
```

O arquivo oculto agora está protegido contra qualquer modificação acidental ou intencional, mantendo apenas o acesso de consulta ativo para quem precisa.

---

## 3. Alterar permissões de diretório

O diretório `drafts/` pertence ao usuário `researcher2`. A regra de segurança determina que apenas ele deve ter acesso a essa pasta e ao seu conteúdo. Para remover completamente os privilégios do grupo de usuários, executei

```Bash
chmod g-x drafts
```

A permissão do diretório mudou de `drwxr-x---` para `drwx------`. Agora, qualquer tentativa de um membro do grupo listar ou acessar os rascunhos será bloqueada pelo sistema operacional.

---

## Resumo

Neste projeto, apliquei conceitos práticos de administração de sistemas Linux para auditar a segurança de dados de uma equipe de pesquisa. Utilizando comandos como ls -la para mapear o ambiente e chmod para restringir privilégios, alinhei o sistema de arquivos às políticas de conformidade da empresa. Essas ações mitigaram riscos de vazamentos e modificações não autorizadas, consolidando a defesa em profundidade a nível de sistema operacional.














