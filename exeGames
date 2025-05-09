import tkinter as tk
from tkinter import messagebox
import ttkbootstrap as ttk
import csv
import re  # Para expressões regulares são sequências de caracteres que definem um padrão de busca em textos

# FUNÇÃO PARA CARREGAR DADOS DO CSV
def carregar_jogos_csv(caminho_csv):
    db = {}
    anos = set()
    devs = set()
    generos = set()
    # Lendo conteúdo do arquivo csv 
    with open(caminho_csv, newline='', encoding='utf-8') as csvfile:
        leitor = csv.DictReader(csvfile)
        # Lógica de seleção das colunas que serão exibidas
        for linha in leitor:
            genero = linha['Genre']
            titulo = linha['Name']
            desenvolvedora = linha['Developer']
            produtora = linha['Producer']
            sistema = linha['Operating System']
            ano_raw = linha['Date Released']
            # Ignorando dados incompletos
            if not (genero and titulo and desenvolvedora and ano_raw):
                continue

            # Extrai só o ano numérico (primeiro grupo de 4 dígitos)
            m = re.search(r'\d{4}', ano_raw)
            if not m:  # Se não achou ano, ele pula
                continue
            ano = m.group()                   

            if genero not in db:
                db[genero] = []
            # Adicionando o conteúdo a ser apresentado na aplicação
            db[genero].append((titulo, ano, desenvolvedora, produtora, sistema))
            anos.add(ano)
            devs.add(desenvolvedora)
            generos.add(genero)

    # Ordenação numérica dos anos (mais recente para mais antigo)
    return db, \
           sorted(generos), \
           sorted(anos, key=lambda a: int(a), reverse=True), \
           sorted(devs)


# CAMINHO DO ARQUIVO CSV
import sys
import os

if getattr(sys, 'frozen', False):  # se estiver empacotado com pyinstaller
    caminho_base = sys._MEIPASS
else:
    caminho_base = os.path.dirname(__file__)

caminho_csv = os.path.join(caminho_base, "computer_games.csv")

jogos_db, todos_generos, todos_anos, todas_devs = carregar_jogos_csv(caminho_csv)

# FUNÇÃO PARA BUSCAR JOGOS COM FILTROS
def buscar_jogos():
    genero = combo_genero.get()
    ano = combo_ano.get()
    dev = combo_dev.get()

    lista_jogos.delete(*lista_jogos.get_children())

    generos_selecionados = list(jogos_db.keys()) if genero == "Todos" else [genero]

    contador = 1  # contador global para a numeração de id correta
    # Seleção do filtro
    for genero_sel in generos_selecionados:
        for (titulo, ano_jogo, dev_jogo, prod, so) in jogos_db[genero_sel]:
            if (ano != "Todos" and ano_jogo != ano):
                continue
            if (dev != "Todos" and dev_jogo != dev):
                continue
            lista_jogos.insert("", tk.END, values=(contador, titulo, ano_jogo, dev_jogo, prod, so))
            contador += 1


# JANELA PRINCIPAL
root = ttk.Window(themename="cyborg")
root.title("Pesquisa de Jogos 🎮")
root.geometry("950x600")

# TÍTULO
label_titulo = ttk.Label(root, text="Pesquise Jogos por Gênero, Ano e Desenvolvedora", font=("Arial", 15, "bold"))
label_titulo.pack(pady=15)

# FRAME DE FILTROS
filtros_frame = ttk.Frame(root)
filtros_frame.pack(pady=10, padx=10, fill="x")

# COMBO GÊNERO
ttk.Label(filtros_frame, text="Gênero:", font=("Arial", 11)).grid(row=0, column=0, padx=5, pady=5, sticky="w")
combo_genero = ttk.Combobox(filtros_frame, values=["Todos"] + todos_generos, font=("Arial", 10), state="readonly", width=25)
combo_genero.grid(row=0, column=1, padx=5, pady=5)
combo_genero.set("Todos")

# COMBO ANO
ttk.Label(filtros_frame, text="Ano:", font=("Arial", 11)).grid(row=0, column=2, padx=5, pady=5, sticky="w")
combo_ano = ttk.Combobox(filtros_frame, values=["Todos"] + todos_anos, font=("Arial", 10), state="readonly", width=15)
combo_ano.grid(row=0, column=3, padx=5, pady=5)
combo_ano.set("Todos")

# COMBO DESENVOLVEDORA
ttk.Label(filtros_frame, text="Desenvolvedora:", font=("Arial", 11)).grid(row=0, column=4, padx=5, pady=5, sticky="w")
combo_dev = ttk.Combobox(filtros_frame, values=["Todos"] + todas_devs, font=("Arial", 10), state="readonly", width=30)
combo_dev.grid(row=0, column=5, padx=5, pady=5)
combo_dev.set("Todos")

# BOTÃO DE BUSCA
button_buscar = ttk.Button(root, text="Buscar Jogos", command=buscar_jogos, bootstyle="primary")
button_buscar.pack(pady=10)

# BOTÃO PARA FECHAR A APLICAÇÃO
button_fechar = ttk.Button(root, text="Fechar", command=root.destroy, bootstyle="danger-outline")  
# Fecha a janela  e em seguida adiciona cor/estilo opcional do ttkbootstrap
button_fechar.pack(pady=10)

# FRAME PARA A LISTA E SCROLLBAR
tabela_frame = ttk.Frame(root)
tabela_frame.pack(pady=10, padx=10, fill="both", expand=True)

# SCROLLBAR VERTICAL
scrollbar = ttk.Scrollbar(tabela_frame, orient="vertical")
scrollbar.pack(side="right", fill="y")

# TABELA DE RESULTADOS
colunas = ("#", "Título", "Ano", "Desenvolvedora", "Produtora", "SO")
lista_jogos = ttk.Treeview(
    tabela_frame,
    columns=colunas,
    show="headings",
    yscrollcommand=scrollbar.set)

# Conecta a Scrollbar com a Treeview
scrollbar.config(command=lista_jogos.yview)

# Cabeçalhos e colunas
for col in colunas:
    lista_jogos.heading(col, text=col)
    lista_jogos.column(col, width=150)

lista_jogos.pack(side="left", fill="both", expand=True)

# EXECUÇÃO
root.mainloop()
