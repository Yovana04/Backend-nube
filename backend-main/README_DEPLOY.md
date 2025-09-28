# Despliegue en Render

## 6) Si falla el build en Render (mysqlclient)
Si ves `Exited with status 1 while building your code` y en los logs aparece algo de `mysqlclient` o `MySQLdb`, agrega el archivo `apt.txt` en la raíz con:
```
default-libmysqlclient-dev
build-essential
pkg-config
```
Render instalará esas dependencias del sistema antes de `pip install`, y `mysqlclient` podrá compilarse correctamente.
