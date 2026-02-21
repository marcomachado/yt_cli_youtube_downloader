# YT CLI — Advanced YouTube Downloader

Ferramenta CLI modular para download de vídeos do YouTube usando `yt-dlp`, com:

- Ambiente virtual automático
- Instalação automática de dependências
- Histórico persistente
- Interface de linha de comando padronizada
- Isolamento total do sistema

---

# Objetivo

Fornecer uma ferramenta de download:

- 🔒 Isolada (venv local)
- 🔁 Reprodutível
- ⚙ Modular
- 🧠 Automatizada
- 🧼 Sem depender de instalação global do yt-dlp

---

# Arquitetura

Ao executar `yt`, o script:

1. Garante que `~/Videos` exista
2. Cria `~/Videos/venv` se necessário
3. Ativa o ambiente virtual
4. Verifica se `yt-dlp` está instalado
5. Instala automaticamente caso não esteja
6. Executa o download com parâmetros configurados

---

# Estrutura Gerada
```
~/Videos/
├── venv/ # Ambiente virtual Python
├── .yt_archive # Histórico de downloads
├── video1.mp4
├── video2.mp4
```
---

# Dependências

- Python 3.8+
- ffmpeg (obrigatório para merge e áudio)

## Instalação no Arch / Manjaro

```bash
sudo pacman -S python ffmpeg
```

### Instalação da Ferramenta
```
mkdir -p ~/.local/bin
nano ~/.local/bin/yt
chmod +x ~/.local/bin/yt
```
### Adicionar ao PATH (caso necessário):
```
export PATH="$HOME/.local/bin:$PATH"
```

### Funcionamento Interno
#### Setup automático
O usuário não precisa fazer nada manualmente.
```
python3 -m venv ~/Videos/venv
source ~/Videos/venv/bin/activate
pip install yt-dlp
```

### Uso
```
yt [opções] <URL1> [URL2] ...\
```

## Opções de Comandos
| Flag | Longa           | Descrição                                    |
| ---- | --------------- | -------------------------------------------- |
| `-a` | `--audio`       | Extrai apenas áudio (mp3)                    |
| `-q` | `--quality`     | Define qualidade máxima (720, 1080, 2160...) |
| `-n` | `--no-playlist` | Ignora playlist                              |
| `-s` | `--subs`        | Baixa e embute legendas                      |
| `-t` | `--thumbnail`   | Baixa e embute thumbnail                     |
| `-d` | `--dir`         | Define diretório customizado                 |
| `-l` | `--list`  | Lista histórico          |
| `-c` | `--clean` | Limpa histórico          |
| `-y` | `--yes`   | Confirma automaticamente |
| `-u` | `--update` | Atualiza yt-dlp |
| `-Q` | `--quiet`  | Modo silencioso |
| `-h` | `--help`   | Mostra ajuda    |

## Exemplos
#### Baixar vídeo
```
yt https://youtube.com/...
```
#### Baixar em 1080p
```
yt -q 1080 URL
```
#### Apenas áudio
```
yt -a URL
```
#### Baixar playlist inteira
```
yt PLAYLIST_URL
```
#### Ignorar playlist
```
yt -n URL
```
#### Limpar histórico
```
yt -c
```
#### Limpar sem confirmação
```
yt -c -y
```
#### Modo silencioso (cron)
```
yt -Q URL
```
#### Atualizar yt-dlp
```
yt -u
```