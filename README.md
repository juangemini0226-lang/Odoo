# Odoo Community local (Docker)

Este paquete levanta Odoo 17 Community + PostgreSQL en tu PC usando Docker, con
una carpeta `addons/` ya lista para que pongas ahí tus módulos propios.

## Requisitos previos

1. Windows 10/11 con WSL2 habilitado.
2. Docker Desktop instalado y corriendo (motor WSL2 activado).

## Pasos

1. Copia toda esta carpeta `odoo-local` a donde quieras guardarla, por ejemplo
   `C:\odoo-local`.
2. Abre una terminal (PowerShell) dentro de esa carpeta.
3. Ejecuta:

   ```
   docker compose up -d
   ```

   La primera vez va a descargar las imágenes de Odoo y PostgreSQL (puede
   tardar varios minutos).
4. Verifica que los contenedores están corriendo:

   ```
   docker compose ps
   ```
5. Abre tu navegador en: http://localhost:8069
6. Vas a ver la pantalla de creación de base de datos. Completa:
   - Nombre de la base de datos (ej: `principal`)
   - Email y contraseña de tu usuario administrador
   - Marca o desmarca "Cargar datos de ejemplo" según prefieras
7. Una vez creada la base de datos, instala las apps "Inventario" y
   "Proyectos" desde el menú Apps dentro de Odoo.

## Tus módulos propios

Todo lo que pongas dentro de la carpeta `addons/` (cada módulo en su propia
subcarpeta, con su `__manifest__.py`) aparecerá disponible para instalar
dentro de Odoo, sin tocar el código fuente original. Esta carpeta es un buen
candidato para convertirla en un repositorio de Git separado más adelante.

## Comandos útiles

- Detener todo (sin borrar datos): `docker compose stop`
- Volver a levantar: `docker compose start`
- Apagar y borrar contenedores (los datos persisten en los volúmenes):
  `docker compose down`
- Ver logs de Odoo en vivo: `docker compose logs -f odoo`
- Borrar TODO incluyendo datos (empezar de cero):
  `docker compose down -v`

## Notas de seguridad

Esta configuración (usuario/contraseña de PostgreSQL y `admin_passwd`) está
pensada solo para uso local en tu PC. Si en algún momento expones esto a
internet, cambia esas credenciales por unas fuertes.
