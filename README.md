# Organizador-Autom-tico-de-Downloads
Preenchimento: altere a pasta 'DOWNLOADS_PATH' na linha 12
"""
Organizador Automático de Downloads
Preenchimento: altere a pasta 'DOWNLOADS_PATH' na linha 12
"""
import os
import shutil
from pathlib import Path

class OrganizadorArquivos:
    def __init__(self, pasta_origem):
        self.pasta = Path(pasta_origem)  # ← PREENCHA: caminho da pasta
        self.categorias = {
            "Imagens": [".jpg", ".jpeg", ".png", ".gif", ".bmp"],
            "Documentos": [".pdf", ".doc", ".docx", ".txt", ".xlsx"],
            "Videos": [".mp4", ".avi", ".mkv", ".mov"],
            "Musicas": [".mp3", ".wav", ".flac", ".aac"],
            "Compactados": [".zip", ".rar", ".7z", ".tar"],
            "Programas": [".exe", ".msi", ".dmg"]
        }
    
    def organizar(self):
        """Move arquivos para pastas por categoria"""
        if not self.pasta.exists():
            print(f"❌ Pasta não encontrada: {self.pasta}")
            return
        
        arquivos_movidos = 0
        
        for arquivo in self.pasta.iterdir():
            if arquivo.is_file():
                extensao = arquivo.suffix.lower()
                
                for categoria, extensoes in self.categorias.items():
                    if extensao in extensoes:
                        pasta_destino = self.pasta / categoria
                        pasta_destino.mkdir(exist_ok=True)
                        
                        destino = pasta_destino / arquivo.name
                        shutil.move(str(arquivo), str(destino))
                        print(f"✅ {arquivo.name} → {categoria}/")
                        arquivos_movidos += 1
                        break
        
        print(f"\n📁 Organização concluída! {arquivos_movidos} arquivos movidos.")

# === COMO CONFIGURAR ===
# Altere o caminho abaixo para sua pasta de downloads ou qualquer pasta:
DOWNLOADS_PATH = r"C:\Users\SeuUsuario\Downloads"  # Windows
# DOWNLOADS_PATH = "/home/usuario/Downloads"        # Linux/Mac
# DOWNLOADS_PATH = r"C:\caminho\para\sua\pasta"     # Qualquer pasta

# === COMO USAR ===
# 1. Configure o caminho acima
# 2. Execute: python organizador.py
# 3. Os arquivos serão organizados automaticamente

if __name__ == "__main__":
    print("🗂️  Organizador de Arquivos")
    confirmacao = input(f"Organizar: {DOWNLOADS_PATH}? (s/n): ")
    
    if confirmacao.lower() == 's':
        org = OrganizadorArquivos(DOWNLOADS_PATH)
        org.organizar()
    else:
        print("Operação cancelada.")
