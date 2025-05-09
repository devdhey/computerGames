# ⚙️ Passo a Passo para Transformar a Aplicação Python em Executável

Este guia detalha como usar o **PyInstaller** para criar um executável da sua aplicação Python de pesquisa de jogos.

**Pré-requisitos:**

* **Python Instalado:** Certifique-se de que o Python esteja instalado e configurado corretamente.
* **PyInstaller Instalado:** Instale com: `pip install pyinstaller`
* **Arquivo `computer_games.csv`:** Este arquivo deve estar no mesmo diretório do seu script Python (`seu_script.py`).

**Passos:**

1.  **Abra o Terminal/Prompt de Comando:** No seu sistema operacional, abra a interface de linha de comando.

2.  **Navegue até o Diretório do Projeto:** Use o comando `cd` para ir até a pasta onde o seu arquivo `seu_script.py` e `computer_games.csv` estão salvos.

    ```bash
    cd /caminho/para/seu/projeto
    ```

3.  **Execute o PyInstaller:** Digite e execute o seguinte comando no terminal:

    ```bash
    pyinstaller --onefile --windowed --add-data "computer_games.csv:." seu_script.py
    ```

    * `pyinstaller`: Chama a ferramenta PyInstaller.
    * `--onefile`: Cria um único arquivo executável.
    * `--windowed`: Indica que é uma aplicação gráfica (sem console).
    * `--add-data "computer_games.csv:."`: Inclui o arquivo CSV no executável, colocando-o na raiz.
    * `seu_script.py`: Substitua pelo nome do seu arquivo Python principal.

4.  **Aguarde a Conclusão:** O PyInstaller processará os arquivos e criará o executável. Isso pode levar alguns minutos.

5.  **Localize o Executável:** O arquivo executável gerado estará na pasta `dist` dentro do diretório do seu projeto.

    * **Windows:** `dist/seu_script.exe`
    * **macOS:** `dist/seu_script.app`
    * **Linux:** `dist/seu_script`

6.  **Execute o Executável:** Navegue até a pasta `dist` e execute o arquivo. O arquivo `computer_games.csv` estará acessível dentro do executável.

**Observações:**

* Certifique-se de que todas as bibliotecas necessárias (como `ttkbootstrap`) estejam instaladas no mesmo ambiente Python que você está usando para gerar o executável.
* Para adicionar um ícone, use a opção `--icon=caminho/do/icone`.
* Teste o executável em diferentes sistemas, se possível, para garantir a compatibilidade.
