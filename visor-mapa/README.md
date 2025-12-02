# Visor-Mapa — Instrucciones rápidas de despliegue

Resumen: aplicación Flask que crea un mapa a partir de un archivo Excel. Requisitos principales en `requirements.txt`. `Procfile` y `gunicorn` ya están configurados para despliegues en PaaS.

Pruebas locales

1. Instala dependencias (recomendado usar un virtualenv):

```powershell
cd 'C:\Users\DEBORA\OneDrive\Desktop\visor-mapa'
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

2. Ejecuta localmente (modo desarrollo):

```powershell
python app.py
# Abrir: http://localhost:5000
```

Desplegar en Render (recomendado)

1. Crea un repo en GitHub y sube este proyecto (ver comandos abajo).
2. En https://render.com crea un nuevo "Web Service", conecta el repo.
3. Branch: `main`. Environment: `Python`.
4. Build command: dejar vacío o `pip install -r requirements.txt`.
5. Start command: `gunicorn app:app --bind 0.0.0.0:$PORT`.

Desplegar en Heroku (alternativa)

1. Instala Heroku CLI y haz `heroku login`.
2. `heroku create nombre-app`.
3. `git push heroku main` (Heroku usa `Procfile` y `requirements.txt`).

Notas importantes

- El almacenamiento en `uploads/` es efímero en la mayoría de PaaS; usa S3 o similar si necesitas persistencia.
- El tile de Google usado en `app.py` puede estar sujeto a TOS; considera usar OpenStreetMap para producción.

Comandos Git (PowerShell)

```powershell
cd 'C:\Users\DEBORA\OneDrive\Desktop\visor-mapa'
git init
git add .
git commit -m "Prep: agregar runtime, gitignore y README"
git branch -M main
git remote add origin https://github.com/TU_USUARIO/TU_REPO.git
git push -u origin main
```

Si quieres, puedo crear estos commits localmente (`git add`/`git commit`) y darte los pasos para empujar al remoto. No puedo crear el repositorio en tu GitHub sin tus credenciales.
