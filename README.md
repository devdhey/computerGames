# 🎮 Aplicação de Pesquisa de Jogos

Este projeto é uma aplicação gráfica desenvolvida em Python que permite ao usuário pesquisar jogos com base em três filtros principais: **Gênero**, **Ano de Lançamento** e **Desenvolvedora**. A interface foi construída com `Tkinter` e estilizada com o pacote `ttkbootstrap`.

---

## ⚠️ Importância da Instalação no Mesmo Interpretador

É **crucial** que as bibliotecas necessárias para este projeto, principalmente o `ttkbootstrap`, sejam instaladas no **mesmo interpretador Python** que você pretende usar para executar o script principal da aplicação (`seu_script.py`, assumindo que este seja o nome do seu arquivo Python).

**Por que isso é importante?**

* **Isolamento de Ambientes:** Diferentes projetos Python podem depender de versões específicas de uma mesma biblioteca. Instalar as dependências no mesmo ambiente (seja o ambiente global padrão ou um ambiente virtual como `virtualenv` ou `conda`) garante que as dependências de um projeto não interfiram nas de outro.

* **Consistência:** Ao instalar as bibliotecas no mesmo interpretador onde o projeto reside, você assegura que o Python utilizado para executar o código tenha acesso direto aos pacotes necessários. Se as bibliotecas forem instaladas em outro interpretador, o Python do seu projeto não as encontrará, resultando em erros como `ModuleNotFoundError`.

* **Reproducibilidade:** Utilizar um ambiente específico para o seu projeto facilita a reprodução do ambiente em outras máquinas. Você pode gerar um arquivo de requisitos (`requirements.txt`) a partir deste ambiente, garantindo que qualquer pessoa possa instalar as mesmas dependências na mesma versão.

**Em resumo, instalar as dependências no mesmo interpretador do projeto evita conflitos de pacotes e garante que a aplicação funcione corretamente.**

---

## 🧩 Funcionalidades

- Carregamento automático de dados de um arquivo CSV (`computer_games.csv`).
- Filtros interativos para refinar a busca por gênero, ano e desenvolvedora através de menus dropdown.
- Exibição dos jogos encontrados em uma tabela com rolagem vertical e cabeçalhos clicáveis para potencial ordenação (funcionalidade padrão do `Treeview` do `tkinter`).
- Interface de usuário moderna e agradável, estilizada com o tema visual da biblioteca `ttkbootstrap`.

---

## ⚙️ Requisitos

Antes de executar o projeto, certifique-se de ter o **Python 3.7 ou superior** instalado. É fundamental utilizar o **mesmo interpretador** (ambiente virtual recomendado) para instalar as dependências listadas abaixo **no mesmo local onde os arquivos do projeto estão salvos**.

### 📦 Instalação de Bibliotecas Necessárias

1.  **Abra o terminal ou prompt de comando.**
2.  **Navegue até a pasta do seu projeto.** Utilize o comando `cd` (change directory) para isso. Por exemplo:
    ```bash
    cd /caminho/para/seu/projeto
    ```
3.  **Execute o seguinte comando para instalar a biblioteca `ttkbootstrap`:**
    ```bash
    pip install ttkbootstrap
    ```

    Este comando irá baixar e instalar a biblioteca `ttkbootstrap` dentro do seu ambiente Python atual (o mesmo onde o projeto está).

---

## 🚀 Funcionamento do Projeto

1.  **Carregamento de Dados:** Ao iniciar o script Python (`seu_script.py`), a função `carregar_jogos_csv` é chamada. Esta função lê os dados do arquivo `computer_games.csv` localizado no mesmo diretório do script. Os dados são processados e armazenados em uma estrutura de dicionário (`jogos_db`), onde a chave é o gênero do jogo e o valor é uma lista de tuplas contendo informações como título, ano, desenvolvedora, produtora e sistema operacional. Adicionalmente, são extraídos e armazenados conjuntos únicos de gêneros, anos e desenvolvedoras para popular os filtros na interface.
   
   Observação: **Certifique-se** de que o arquivo `computer_games.csv` esteja localizado na mesma pasta/local que o **script** `python`

3.  **Interface Gráfica:** A biblioteca `tkinter` (através do tema `ttkbootstrap`) cria uma janela com os seguintes elementos:
    * Um título informativo.
    * Um frame contendo três menus dropdown (`Combobox`) para filtrar os jogos por "Gênero", "Ano" e "Desenvolvedora". A opção "Todos" está disponível em cada filtro para não aplicar restrições.
    * Um botão "Buscar Jogos" que, ao ser clicado, aciona a função `buscar_jogos`.
    * Um botão "Fechar" para encerrar a aplicação.
    * Uma área de tabela (`Treeview`) para exibir os resultados da busca com cabeçalhos para "Título", "Ano", "Desenvolvedora", "Produtora" e "SO". Uma barra de rolagem vertical é adicionada para visualizar todos os resultados caso a lista seja longa.

4.  **Filtragem e Busca:** Quando o botão "Buscar Jogos" é pressionado, a função `buscar_jogos` é executada. Esta função:
    * Obtém os valores selecionados nos menus de filtro de gênero, ano e desenvolvedora.
    * Limpa qualquer resultado anterior exibido na tabela.
    * Itera sobre o dicionário `jogos_db`. Para cada gênero (ou o gênero selecionado, se um filtro específico foi aplicado), itera sobre a lista de jogos associada.
    * Para cada jogo, verifica se ele corresponde aos filtros de ano e desenvolvedora selecionados (se houver).
    * Se o jogo atender a todos os critérios de filtro, suas informações (título, ano, desenvolvedora, produtora e sistema operacional) são inseridas como uma nova linha na tabela de resultados.

5.  **Visualização dos Resultados:** Os jogos que correspondem aos critérios de busca são exibidos na tabela. Cada coluna mostra uma informação diferente sobre o jogo. A barra de rolagem permite navegar por longas listas de resultados.

6.  **Fechamento da Aplicação:** Ao clicar no botão "Fechar", a janela principal da aplicação é destruída, encerrando o programa.

Para executar a aplicação, navegue até a pasta do projeto no seu terminal e execute o script Python:

```bash
python seu_script.py
