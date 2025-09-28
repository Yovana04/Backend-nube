# Despliegue en Render (Flask) + MySQL en Railway

## 1) Variables de entorno (Render -> Environment)
Usa estos nombres exactos (tu código ya los lee en `config/db.py`):
- `DB_HOST`
- `DB_PORT`
- `DB_USER`
- `DB_PASSWORD`
- `DB_NAME`
- `JWT_SECRET_KEY`
- `ALLOWED_ORIGINS` (opcional)
- `FLASK_DEBUG` (false en producción)

Puedes guiarte con `.env.example` (no subas `.env` al repo).

## 2) Python Service en Render
- **Build Command**
```
pip install -r requirements.txt
```
- **Start Command**
```
gunicorn app:app --bind 0.0.0.0:$PORT
```

> Render inyecta `PORT`. No definas `PORT` manualmente.
> Si necesitas debugging local: `python app.py` (usa `FLASK_DEBUG=true`).

## 3) Railway (MySQL)
- Crea la BD MySQL.
- Usa **Public Network** y copia Host, Port, User, Password, Database a las vars de Render.
- Crea tablas ejecutando `schema.sql` en Railway (Connect -> SQL Editor).

## 4) Pruebas (Postman)
1. Registrar usuario: `POST /usuarios/registrar`
2. Iniciar sesión: `POST /usuarios/login`  (captura `token`)
3. Datos usuario: `GET /usuarios/datos` (Authorization: Bearer <token>)
4. Crear tarea: `POST /tareas/crear`
5. Obtener tareas: `GET /tareas/obtener`
6. Modificar tarea: `PUT /tareas/modificar/:id`

## 5) Local (opcional)
```
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
cp .env.example .env  # y rellena valores
python app.py
```
