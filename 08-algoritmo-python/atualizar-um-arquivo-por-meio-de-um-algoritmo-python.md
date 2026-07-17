# Atividade: Algoritmo Python para Atualização de Arquivos de Segurança 🐍🛡️

## 📝 Descrição do Projeto (Project description)
Como analista de segurança em uma organização de saúde, sou responsável por controlar o acesso a uma sub-rede restrita que contém registros confidenciais de pacientes. Esse controle é feito por meio de um arquivo de texto que lista os endereços IP autorizados (lista de permissões). Quando funcionários mudam de setor ou são desligados, preciso garantir que seus IPs sejam removidos imediatamente. Para automatizar esse processo e evitar falhas manuais, desenvolvi um algoritmo em Python que abre o arquivo de permissões, compara seu conteúdo com uma lista de remoção e atualiza os registros de forma limpa e rápida.

---

## 🔍 Open the file that contains the allow list
Para iniciar o algoritmo, o primeiro passo é mapear e abrir o arquivo que armazena os IPs autorizados. Usei o seguinte trecho de código para fazer isso:

```python
import_file = "allow_list.txt" 
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

with open(import_file, "r") as file:
