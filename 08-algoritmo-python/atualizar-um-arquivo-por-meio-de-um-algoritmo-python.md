# Atividade: Algoritmo python para atualização de arquivos de segurança 🐍

## 📝 Descrição do projeto
Como analista de segurança em uma organização de saúde, sou responsável por controlar o acesso a uma sub-rede restrita que contém registros confidenciais de pacientes. Esse controle é feito por meio de um arquivo de texto que lista os endereços IP autorizados. Quando funcionários mudam de setor ou são desligados, preciso garantir que seus IPs sejam removidos imediatamente. Para automatizar esse processo e evitar falhas manuais, desenvolvi um algoritmo em Python que abre o arquivo de permissões, compara seu conteúdo com uma lista de remoção e atualiza os registros de forma limpa e rápida.

---

## 🔍 Arquivo que contém a lista de permissões.
Para iniciar o algoritmo, o primeiro passo é mapear e abrir o arquivo que armazena os IPs autorizados. Usei o seguinte trecho de código para fazer isso.

```python
import_file = "allow_list.txt" 
remove_list = ["192.168.97.225", "192.168.158.170", "192.168.201.40", "192.168.58.57"]

with open(import_file, "r") as file:
```

Executar este código resultará em um erro, pois ele conterá apenas a primeira linha da instrução `with` completarei esta instrução `with` na tarefa seguinte.

---

## 🔍 Ler o conteúdo do arquivo
Com o arquivo aberto dentro do bloco, precisei transformar o conteúdo bruto em um formato legível para o Python.

```python
with open(import_file, "r") as file:
    ip_addresses = file.read()

print(ip_addresses)
```

Apliquei .read() diretamente na variável do arquivo file. Esse método lê todo o texto no arquivo e o converte em uma grande cadeia de caracteres (string). Salvei essa string em uma nova variável chamada ip_addresses para que pudesse manipular esses dados nas próximas linhas do script.

---

## 🔍 Converter a string em uma lista
Manipular uma string única contendo vários IPs misturados seria muito difícil, então o melhor caminho foi fatiar esse texto.

```python
ip_addresses = ip_addresses.split()
print(ip_addresses)
```

Utilizei o .split() na string ip_addresses. Essa função quebra o texto longo nos espaços em branco e quebras de linha, transformando aquela string única em uma lista de strings independentes. Agora, cada endereço IP virou um item isolado dentro da lista ip_addresses, o que permite analisar e remover elementos um por um.

---

## 🔍 Lista de remoção
Com a lista principal pronta, montei a estrutura de repetição para varrer os IPs que precisam ser cancelados

```python
for element in remove_list:
    print(element)
```

Configurei um loop for utilizando a variável temporária element para repetir sequencialmente por cada endereço IP presente na na lista de exclusão remove_list.

---

## 🔍 Remova os endereços IP que estão na lista de remoção
Dentro do laço de repetição, configurei a lógica que faz a exclusão dos endereços proibidos

```python
for element in remove_list:
    if element in ip_addresses:
        ip_addresses.remove(element)

print(ip_addresses)
```

criei uma estrutura condicional usando a palavra-chave `if` com o operador `in` para checar se o IP atual avaliado pela variável `element` realmente existe dentro da lista de permissões `ip_addresses`. Se a condição for verdadeira, o algoritmo aplica o `.remove(element)` diretamente na lista de permissões para apagar o IP. A aplicação do método `.remove()` dessa forma é totalmente segura e eficiente neste cenário porque não existem endereços IP duplicados na lista.

---

## 🔍 Atualizar o arquivo com a lista revisada de endereços IP
Para finalizar o script, precisei salvar a lista atualizada de volta no arquivo de texto físico, substituindo o conteúdo antigo

```python
ip_addresses = "\n".join(ip_addresses)

with open(import_file, "w") as file:
    file.write(ip_addresses)
```

Primeiro, usei o método `.join()` aplicando a string de quebra de linha `"\n"` para juntar todos os itens da lista revisada de volta em uma única string, garantindo que cada endereço IP fique organizado em sua própria linha no arquivo. Depois, abri novamente o arquivo indicado em `import_file`, mas dessa vez passando o argumento `"w"`, informando ao Python que quero dados. Por fim, executei o método `.write(ip_addresses)` para gravar o texto limpo, atualizando as permissões de forma definitiva.

---

🏁 Resumo do projeto
Desenvolvi um algoritmo em Python focado na automação de tarefas de controle de acesso para proteção de ambientes de saúde. O script utiliza a instrução estruturada with combinada com as funções open(), .read() e .write() para ler e atualizar arquivos locais de forma segura. Através da conversão de tipos de dados com .split() e .join(), foi possível tratar strings como listas dinâmicas. Por fim, a implementação de laços condicionais e loops for permitiu varrer e expurgar com precisão os IPs bloqueados através do método .remove(), eliminando gargalos operacionais e diminuindo os riscos de acessos indevidos na organização.
