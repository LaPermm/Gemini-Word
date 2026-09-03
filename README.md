Gemini Assistant para Microsoft Word
Complemento personalizado de panel de tareas (Task Pane Add-in) que integra la API de Google Gemini en Microsoft Word mediante carga lateral (sideloading) y catálogo compartido local, eludiendo bloqueos de la tienda oficial o restricciones de licencias institucionales.

Requisitos previos
Microsoft Word (versión de escritorio para Windows).

Página del complemento alojada en HTTPS (ej. GitHub Pages: [https://lapermm.github.io/Gemini-Word/](https://lapermm.github.io/Gemini-Word/)).

API Key de Google Gemini (obtenida gratis desde Google AI Studio).

Guía de instalación paso a paso
1. Crear y compartir la carpeta local de manifiestos
Office requiere una ruta de red UNC (formato \\servidor\recurso) para cargar complementos locales de confianza.

Abre el Explorador de archivos y crea una carpeta en tu disco C:\ llamada OfficeManifests (ruta: C:\OfficeManifests).

Haz clic derecho sobre la carpeta OfficeManifests > Propiedades.

Ve a la pestaña Uso compartido y pulsa el botón Uso compartido avanzado....

Marca la casilla Compartir esta carpeta.

Haz clic en Permisos, verifica que tu usuario (o Todos) tenga permisos de Lectura, presiona Aceptar y luego Aplicar.

Copia la ruta de red generada. Deberá verse como:

\\localhost\OfficeManifests

2. Registrar la carpeta en el Centro de confianza de Word
Abre Microsoft Word.

Ve a Archivo > Opciones.

En el menú lateral, selecciona Centro de confianza y haz clic en el botón Configuración del Centro de confianza....

Haz clic en Catálogos de complementos de confianza (menú izquierdo).

En el campo Dirección URL de catálogo, escribe:

\\localhost\OfficeManifests

Haz clic en Agregar catálogo.

En la lista inferior, marca la casilla Mostrar en el menú junto a la ruta añadida.

Haz clic en Aceptar en ambas ventanas y reinicia Word por completo.

3. Crear y colocar el archivo manifest.xml
Abre el Bloc de notas o tu editor de código.

Pega la siguiente estructura XML asegurándote de que la URL apunte a tu despliegue en GitHub Pages:

XML:

<?xml version="1.0" encoding="UTF-8"?>
<OfficeApp xmlns="http://schemas.microsoft.com/office/appforoffice/1.1"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:type="TaskPaneApp">
  <Id>b7c2a1e4-9d5f-4a3b-8e1c-d4e5f6a7b8c9</Id>
  <Version>1.0.0.0</Version>
  <ProviderName>Personal</ProviderName>
  <DefaultLocale>es-ES</DefaultLocale>
  <DisplayName DefaultValue="Panel IA Gemini" />
  <Description DefaultValue="Asistente de IA para documentos" />
  <IconUrl DefaultValue="https://assets.msn.com/staticsb/statics/latest/bing/copilot/favicon.png" />
  <SupportUrl DefaultValue="https://lapermm.github.io/Gemini-Word/" />
  <Hosts>
    <Host Name="Document" />
  </Hosts>
  <DefaultSettings>
    <SourceLocation DefaultValue="https://lapermm.github.io/Gemini-Word/" />
  </DefaultSettings>
  <Permissions>ReadWriteDocument</Permissions>
</OfficeApp>

Guarda el archivo con el nombre manifest.xml directamente dentro de C:\OfficeManifests.

4. Ejecutar el complemento en Word
Abre un documento en blanco en Word.

Dirígete a la pestaña Insertar > Complementos > Mis complementos (o el menú desplegable equivalente).

Selecciona la pestaña CARPETA COMPARTIDA.

Haz clic sobre Panel IA Gemini y presiona Agregar.

El panel lateral se desplegará a la derecha:

Pega tu API Key de Gemini en el primer campo (se almacena localmente en localStorage).

Ya puedes interactuar en modo libre o seleccionar texto en el documento y ejecutar acciones automáticas.

Solución de problemas comunes
No aparece la pestaña "Carpeta compartida": Asegúrate de haber reiniciado Word después de añadir la URL en el Centro de confianza y verifica que la casilla Mostrar en el menú esté activa.

El panel muestra una versión vieja del código (Caché): Haz clic derecho en cualquier espacio vacío dentro del panel lateral de Word y presiona Recargar (Reload).

Error de autenticación / credenciales: Confirma que la API Key provenga de Google AI Studio y que no haya sido subida directamente al código fuente público de GitHub.
