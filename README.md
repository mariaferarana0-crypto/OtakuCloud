# OtakuCloud 2.0
Biblioteca personal de anime, manga y manhwa. PHP 8+, MySQL 8 / MariaDB 10.4+, HTML, CSS y JavaScript sin dependencias externas. Modo claro. Proyecto académico.

## Instalación en XAMPP (Windows)
1. Descomprime el ZIP. Copia la carpeta `otakucloud` a `C:\xampp\htdocs\otakucloud` (evita duplicar la carpeta).
2. Activa Apache y MySQL. Abre http://localhost/phpmyadmin/.
3. Si ya importaste la fase 2, NO vuelvas a importar `otakucloud.sql` ni `datos_prueba.sql`. Si es una instalación nueva, importa primero el esquema y luego los datos de prueba, seleccionando la base `otakucloud`.
4. Selecciona `otakucloud` e importa `database/actualizacion_v2.sql`. Es una actualización acumulativa no destructiva que incorpora manhwas reales y ficticios, más portadas. No necesitas `catalogo_real.sql`. Los capítulos son una muestra; las cubiertas de obras reales son gráficas no oficiales y las ficticias son ilustraciones originales. Consulta ACTUALIZAR.txt.
5. Abre http://localhost/otakucloud/ (no uses Live Server). Si Apache tiene otro puerto, agrégalo a la URL.
6. Regístrate con nombre, correo y contraseña de al menos 8 caracteres. Inicia sesión y agrega una obra a tu biblioteca. Marca capítulos.
7. Para crear el administrador: regístrate primero con una cuenta propia, cierra sesión, selecciona otakucloud en phpMyAdmin > SQL y ejecuta:
   `UPDATE usuarios SET rol='admin' WHERE correo='TU_CORREO_REAL';`
   Sustituye el correo por el que registraste. Inicia sesión desde http://localhost/otakucloud/acceso-admin.php. Las cuentas normales no pueden acceder por esa entrada. No hay contraseña de administrador predeterminada.

## Configuración
Los valores locales por defecto están en config/conexion.php (root, sin contraseña, puerto 3306). Si son diferentes, copia `config/local.example.php` a `config/local.php` y modifica los valores. No subas local.php a GitHub. En producción usa variables DB_HOST, DB_PORT, DB_NAME, DB_USER, DB_PASS o local.php con un usuario de base de datos dedicado y contraseña fuerte. Conserva HTTPS y restringe acceso web a config y database (.htaccess incluido para Apache; en otros servidores configura reglas equivalentes). No publiques credenciales ni exportaciones de datos personales.

## Módulos
Inicio, registro, inicio y cierre de sesión, catálogo con filtros, detalle, seguimiento por capítulo, favoritos, estados, reseñas, perfil, administración de obras, capítulos, géneros, usuarios y moderación. Estadísticas obtenidas de consultas reales. La portada local se indica como ruta assets/img/archivo.webp tras copiar una imagen autorizada. No hay carga de archivos desde formulario, lector, reproducción, OAuth, recuperación por correo ni notificaciones. El orden de destacadas es editorial, no ranking de popularidad. La navegación lateral se adapta a dispositivos móviles. El dashboard administrativo muestra los recuentos y gráficos derivados de datos registrados. El diseño adapta el mockup al navegador y utiliza CSS propio, no Bootstrap.

## Pruebas que deben ejecutar
- Registrar dos usuarios distintos, iniciar/cerrar sesión y probar contraseña incorrecta.
- Verificar búsqueda y filtro por formato/género.
- Agregar una obra, marcar/desmarcar capítulos, comprobar persistencia y progreso de cada usuario.
- Guardar favoritos, cambiar estado, reseñar y editar perfil.
- Con usuario normal, abrir index.php?page=admin: debe responder 403.
- Con administrador, crear/editar/eliminar una obra de prueba, gestionar capítulos, géneros y moderar una reseña.
- Comprobar vistas en PC y móvil, y repetir en el hosting con HTTPS.
- Guardar capturas reales. No se han ejecutado pruebas de integración MySQL en el entorno de generación.

## Git y despliegue
Crear un repositorio, invitar a los integrantes y realizar commits reales por módulo. En hosting PHP/MySQL, crear base de datos y usuario, importar SQL (si el hosting no permite CREATE DATABASE/USE, quitarlos de una copia del script y seleccionar la base asignada), configurar credenciales y subir archivos. Activar HTTPS y verificar pruebas. Mantener copias de seguridad. No usar root en producción. Añadir limitación de intentos de login a nivel servidor antes de exposición pública.
