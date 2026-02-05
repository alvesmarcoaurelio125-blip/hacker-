[hacker.txt](https://github.com/user-attachments/files/25084428/hacker.txt)
from pathlib import Path
import shutil
import zipfile

base = Path("/mnt/data/site_imagem")
base.mkdir(exist_ok=True)

# Copy image
src = Path("/mnt/data/1543335157877 troll.jfif")
img = base / "imagem.jpg"
shutil.copy(src, img)

# Create index.html
html = base / "index.html"
html.write_text("""<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Imagem</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    html, body {
      margin: 0;
      padding: 0;
      width: 100%;
      height: 100%;
      background: black;
    }
    body {
      display: flex;
      align-items: center;
      justify-content: center;
    }
    img {
      max-width: 100%;
      max-height: 100%;
    }
  </style>
</head>
<body>
  <img src="imagem.jpg" alt="Imagem">
</body>
</html>
""", encoding="utf-8")

# Zip everything
zip_path = Path("/mnt/data/site_pronto.zip")
with zipfile.ZipFile(zip_path, 'w', zipfile.ZIP_DEFLATED) as z:
    z.write(html, arcname="index.html")
    z.write(img, arcname="imagem.jpg")

zip_path
