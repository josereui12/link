import os
import shutil

class BibliotecaArquivos:
    def __init__(self, diretorio='biblioteca_arquivos'):
        self.diretorio = diretorio
        if not os.path.exists(self.diretorio):
            os.makedirs(self.diretorio)

    def adicionar_arquivo(self, caminho_arquivo):
        if not os.path.exists(caminho_arquivo):
            print("Arquivo não encontrado.")
            return
        nome = os.path.basename(caminho_arquivo)
        destino = os.path.join(self.diretorio, nome)
        shutil.copy2(caminho_arquivo, destino)
        print(f"Arquivo '{nome}' adicionado à biblioteca.")

    def listar_arquivos(self):
        arquivos = os.listdir(self.diretorio)
        if arquivos:
            print("Arquivos na biblioteca:")
            for arquivo in arquivos:
                print(f" - {arquivo}")
        else:
            print("Nenhum arquivo na biblioteca.")

    def buscar_arquivo(self, nome_parcial):
        encontrados = [f for f in os.listdir(self.diretorio) if nome_parcial.lower() in f.lower()]
        if encontrados:
            print("Arquivos encontrados:")
            for arquivo in encontrados:
                print(f" - {arquivo}")
        else:
            print("Nenhum arquivo correspondente encontrado.")

    def remover_arquivo(self, nome_arquivo):
        caminho = os.path.join(self.diretorio, nome_arquivo)
        if os.path.exists(caminho):
            os.remove(caminho)
            print(f"Arquivo '{nome_arquivo}' removido.")
        else:
            print("Arquivo não encontrado na biblioteca.")

# Exemplo de uso
if __name__ == "__main__":
    biblioteca = BibliotecaArquivos()

    # Exemplo de comandos
    biblioteca.adicionar_arquivo("exemplo.txt")  # Substitua com um caminho real
    biblioteca.listar_arquivos()
    biblioteca.buscar_arquivo("exem")
    biblioteca.remover_arquivo("exemplo.txt")
