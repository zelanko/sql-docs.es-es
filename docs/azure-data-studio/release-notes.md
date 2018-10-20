---
title: Notas de la versión de Data Studio Azure | Microsoft Docs
description: Notas de la versión de Data Studio Azure
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dfa3636ddba734d9c6ee6c9d9da4560a3cd61304
ms.sourcegitcommit: ef115025e57ec342c14ed3151ce006f484d1fadc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/18/2018
ms.locfileid: "49411202"
---
# <a name="azure-data-studio-release-notes"></a>Notas de la versión de Data Studio Azure

**[Descargue la versión de octubre.](download.md)**

## <a name="october-2018-october-release"></a>Octubre de 2018 (versión de octubre)

fecha de lanzamiento: 18 de octubre de 2018  
versión: 1.1.3

- Introducción a Azure Resource Explorer para examinar las bases de datos SQL de Azure
- Mejorar la solidez de conectividad del explorador de objetos y el Editor de consultas
- Mejoras de las extensiones de agente SQL
- Actualizar a la [extensión de versión preliminar de SQL Server de 2019](https://docs.microsoft.com/sql/azure-data-studio/sql-server-2019-extension?view=sql-server-ver15)

### <a name="bug-fixes"></a>Correcciones de errores

Para obtener información detallada, consulte el [registro de cambios](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), y [versiones](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="september-2018-september-ga-release"></a>(Versión de septiembre GA) de septiembre de 2018

fecha de lanzamiento: 24 de septiembre de 2018  
versión: 1.0

Versión de disponibilidad general de Azure Data Studio (anteriormente SQL Operations Studio).

- Anuncio de la extensión de la versión preliminar de SQL Server de 2019.
  - Admite las características de vista previa de SQL Server 2019, incluidas [clúster de macrodatos](../big-data-cluster/big-data-cluster-overview.md) admite.
    - Conectarse a la puerta de enlace de Spark o HDFS se incluye con la versión preliminar de SQL Server 2019.
    - Examinar HDFS, cargar archivos, guardar archivos e iniciar acciones útiles como analizar en el Bloc de notas para los archivos CSV.
    - Envío de trabajos de Spark desde el panel o haga doble clic en una conexión de Spark o HDFS en el Explorador de objetos.
  - Datos de Azure Notebooks de Studio
    - Crear o Abrir Bloc de notas con un visor integrado del Bloc de notas. En esta versión, el Bloc de notas Visor admite la conexión a locales kernels y solo el clúster de macrodatos de SQL Server 2019.
    - Usar las bibliotecas de Acelerador de código de PROSE en el Bloc de notas para obtener información sobre los tipos de datos y formato de archivo para la preparación de datos rápida.
  - Explorador de recursos de Azure
    - La vista del explorador de recursos de Azure le permite examinar los puntos de conexión relacionados con los datos para las cuentas de Azure y crear conexiones en ellos en el Explorador de objetos. En esta versión se admiten servidores y bases de datos de SQL Azure.
  - Asistente para la tabla externa de creación de SQL Server Polybase
    - Crear una tabla externa y sus estructuras de metadatos compatibles con un asistente fácil de usar. En esta versión, se admiten servidores remotos de SQL Server y Oracle.
- Rendimiento de la cuadrícula de resultados y las mejoras de la experiencia de usuario de gran número de conjuntos de resultados de consulta.
- Actualizar código fuente de Visual Studio Code desde 1,23 a 1.26.1 con el diseño de cuadrícula y ha mejorado el Editor de configuración (versión preliminar).
- Mejoras de accesibilidad para el lector de pantalla, navegación mediante el teclado y alto contraste.
- Agregar `Connection name` opción para proporcionar un nombre alternativo en la vista de servidores-let.

### <a name="bug-fixes"></a>Correcciones de errores

- Corregir [emitir #2647](https://github.com/Microsoft/azuredatastudio/issues/143): los gráficos dio un gran paso hacia atrás.
- Corregir [emitir 2648 #](https://github.com/Microsoft/azuredatastudio/issues/143): SELECT que devuelve toda la columna de los hipervínculos JSON.
- …

Para obtener información detallada, consulte el [registro de cambios](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), y [versiones](https://github.com/Microsoft/azuredatastudio/releases).


## <a name="august-2018-august-public-preview"></a>Agosto de 2018 (versión preliminar pública de agosto)

fecha de lanzamiento: 30 de agosto de 2018  
versión: 0.32.8

*0.32.8 contiene correcciones para un par regresiones se encuentra en 0.32.7 ([#1971](https://github.com/Microsoft/azuredatastudio/issues/1971), [2372 #](https://github.com/Microsoft/azuredatastudio/issues/2372)*)

El *versión preliminar pública de agosto* se centra en correcciones de errores, la estabilización de producto y rellenando los huecos en los escenarios existentes.  

- Anuncio de la extensión de importación SQL Server
- Administración de sesiones de SQL Server Profiler
- Compatibilidad con plantillas de sesión de SQL Server Profiler
- Mejoras del Agente SQL Server
- Nueva extensión de la Comunidad: kit de primer servicio de respuesta
- Mejoras de calidad de vida: las cadenas de conexión

### <a name="bug-fixes"></a>Correcciones de errores

- Analizar SQL en una ventana del Editor de consultas mediante el `Parse Syntax` comando.
- Corregir [emitir #143](https://github.com/Microsoft/azuredatastudio/issues/143): haga doble clic en seleccionar no en nombre de variable.
- Corregir [emitir #387](https://github.com/Microsoft/azuredatastudio/issues/387): icono de la pestaña base de datos SQL está en rojo.
- Corregir [emitir 825 #](https://github.com/Microsoft/azuredatastudio/issues/825): solicitar: automáticamente conectarse al servidor actual después de la secuencia de comandos como... 
- Corregir [emitir 1278 #](https://github.com/Microsoft/azuredatastudio/issues/1278): sqlops.desktop [Entry escritorio] - valor redundante para el nombre de & comentario.
- Corregir [emitir 1285 #](https://github.com/Microsoft/azuredatastudio/issues/1285): actualización hace que el icono de la aplicación se quitan o reemplazan en Windows.
- Corregir [emitir 1317 #](https://github.com/Microsoft/azuredatastudio/issues/1317): corregir el separador decimal.
- Corregir [emitir 1474 #](https://github.com/Microsoft/azuredatastudio/issues/1474): Cancelar cambiar conexión desconecta la conexión actual.
- Corregir [emitir 1497 #](https://github.com/Microsoft/azuredatastudio/issues/1497): vista como el gráfico se cortan las opciones en la parte inferior.
- Corregir [emitir 1524 #](https://github.com/Microsoft/azuredatastudio/issues/1524): Shell/Dashboard: iconos de viewlet Main son arrastrables y puede bloquear la aplicación.
- Corregir [emitir 1578 #](https://github.com/Microsoft/azuredatastudio/issues/1578): no se puede expandir o contraer carpeta del explorador de archivos remoto, haga clic en el nombre.
- Corregir [emitir 1620 #](https://github.com/Microsoft/azuredatastudio/issues/1620): característica Sugerencia: obtener la cadena de conexión para la conexión existente.
- Corregir [emitir 1624 #](https://github.com/Microsoft/azuredatastudio/issues/1624): SelectBox no cambian de color cuando se deshabilita.
- Corregir [emitir 1728 #](https://github.com/Microsoft/azuredatastudio/issues/1728): Guardar como JSON o EXCEL o CSV no funcionan.
- Corregir [emitir 1744 #](https://github.com/Microsoft/azuredatastudio/issues/1744): panel de resultados pierde sus posiciones de desplazamiento al cambiar entre pestañas.
- Corregir [emitir 1748 #](https://github.com/Microsoft/azuredatastudio/issues/1748): mensaje de Error al guardar la hora de archivo segunda (y posteriores) de Excel.
- Corregir [emitir 1782 #](https://github.com/Microsoft/azuredatastudio/issues/1782): editar datos: celda no revierta al valor original de presionar la tecla ESC.
- Corregir [emitir 1836 #](https://github.com/Microsoft/azuredatastudio/issues/1836): los archivos .sql que no está asociados con SQL Operations Studio.
- Corregir [emitir 1850 #](https://github.com/Microsoft/azuredatastudio/issues/1850): escribir N'' completa automáticamente a N'' '.
- Corregir [emitir 1985 #](https://github.com/Microsoft/azuredatastudio/issues/1985): copia de cuadrícula de resultados de consulta está desactivada de forma 1 columna.
- Corregir [emitir 1998 #](htpts://github.com/Microsoft/azuredatastudio/pull/1998): agregar VS Code versión a sobre el cuadro de diálogo.
- Corregir [emitir 2042 #](https://github.com/Microsoft/azuredatastudio/pull/2042): agente: botón habilitado para importar las consultas de los archivos de sql.
- Corregir [emitir 2091 #](https://github.com/Microsoft/azuredatastudio/issues/2091): no se puede usar el método abreviado Ctrl + C para copiar desde el panel de resultados.
- Corregir [emitir 2099 #](https://github.com/Microsoft/azuredatastudio/pull/2099): se han agregado más opciones saveAsCsv.
- Corregir [emitir 2107 #](https://github.com/Microsoft/azuredatastudio/issues/2107): icono de documento de actualización para los documentos de panel y Profiler.
- Corregir [emitir 2129 #](https://github.com/Microsoft/azuredatastudio/pull/2129): datos de edición de guardar la posición de desplazamiento al cambiar de fichas.
- Corregir [emitir 2152 #](https://github.com/Microsoft/azuredatastudio/issues/2152): resultados de la cuadrícula de fila indicador cero Based.

## <a name="known-issues"></a>Problemas conocidos

- [Problema #2371](https://github.com/Microsoft/azuredatastudio/issues/2371) Guardar como sólo guarda primera fila de datos de Excel
- [Problema #2150](https://github.com/Microsoft/azuredatastudio/issues/2150): no se puede conectar en Ubuntu 16.04 para SQL en un contenedor


## <a name="july-2018-july-public-preview"></a>Julio de 2018 (versión preliminar pública de julio)

fecha de lanzamiento: 19 de julio de 2018  
versión: 0.31.4

El *versión preliminar pública de julio* se centra en la versión inicial de los escenarios de configuración del Agente SQL Server, mejoras de plantilla de sesión y la vista de SQL Server Profiler y continuadas correcciones para problemas de GitHub notificados por los clientes. Esta versión contiene los puntos destacados siguientes:  

- [Agente SQL Server para la extensión de SQL Operations Studio](sql-server-agent-extension.md) mejoras
 - Se ha agregado la vista de alertas, operadores y los servidores proxy y los iconos en el panel izquierdo
 - Cuadros de diálogo se ha agregado de nuevo trabajo, nuevo paso de trabajo, nueva alerta y New (operador)
 - Se ha agregado Eliminar trabajo, eliminar alertas y operador Delete (ratón)
 - Visualización de ejecuciones anteriores se ha agregado
 - Filtros agregados para cada nombre de columna
- [SQL Server Profiler para la extensión de SQL Operations Studio](sql-server-profiler-extension.md) mejoras
 - Teclas de acceso rápido agregada para iniciar y rápidamente inicios y paradas Profiler
 - Se ha agregado 5 plantillas predeterminadas para ver los eventos extendidos
 - Nombre de la conexión de servidor y base de datos se ha agregado
 - Se ha agregado compatibilidad para las instancias de Azure SQL Database
 - Sugerencia agregada para salir a Profiler cuando se cierra la pestaña cuando Profiler aún se está ejecutando
- Versión de extensión de Scripts de combinación
- Puntos de extensibilidad de cuadro de diálogo y Asistente para agregados para los autores de extensiones
- Solucionar problemas de GitHub:
 - Corregir [emitir 728](https://github.com/Microsoft/azuredatastudio/issues/728): ninguna respuesta al agregar conexión en macOS
 - Corregir [emitir 1612](https://github.com/Microsoft/azuredatastudio/issues/1612): presentación del texto de cuadrícula de resultados está equivocada por caracteres internacionales
 - Corregir [emitir 1693](https://github.com/Microsoft/azuredatastudio/issues/1693): cuadro de diálogo de copia de seguridad: se ha interrumpido la interfaz de usuario del explorador de archivos
 - Corregir [emitir 1713](https://github.com/Microsoft/azuredatastudio/issues/1713): número de filas afectadas
 - Corregir [emitir 1718](https://github.com/Microsoft/azuredatastudio/issues/1718): no se puede conectar a cualquier origen de datos
 - Corregir [emitir 1719](https://github.com/Microsoft/azuredatastudio/issues/1719): TypeError al conectarse al servidor
 - Corregir [emitir 1724](https://github.com/Microsoft/azuredatastudio/issues/1724): los cuadros de diálogo extensión han dejado de funcionar
 - Corregir [emitir 1749](https://github.com/Microsoft/azuredatastudio/issues/1749): error: se interpretan los datos HTML en una columna
 - Corregir [emitir 1789](https://github.com/Microsoft/azuredatastudio/issues/1789): extensibilidad: si agrega un proveedor de conexión desinstalar nunca quitará de la lista
 - Corregir [emitir 1791](https://github.com/Microsoft/azuredatastudio/issues/1791): extensiones Sqlops: queryeditor.connect() se conecta a la base de datos de destino, pero no muestra la interfaz de usuario está conectado el editor
 - Corregir [emitir 1799](https://github.com/Microsoft/azuredatastudio/issues/1799): gráfico de tamaño de base de datos de Top 10 no funciona en las instancias distingue mayúsculas de minúsculas
 - Corregir [emitir 1814](https://github.com/Microsoft/azuredatastudio/issues/1814): definición de tipo de error de escritura sqlops.d.ts causando implícito 'any'
 - Corregir [emitir 1817](https://github.com/Microsoft/azuredatastudio/issues/1817): Error de Ortografia
 - Corregir [emitir 1830](https://github.com/Microsoft/azuredatastudio/issues/1830): establecer iconPath en ButtonComponent después de llamar a component() no cambia el icono
 - Corregir [emitir 1843](https://github.com/Microsoft/azuredatastudio/issues/1843): organización de tablas mejor


## <a name="june-2018-june-public-preview"></a>Junio de 2018 (versión preliminar de junio público)

fecha de lanzamiento: 20 de junio de 2018  
versión: 0.30.6

El *versión preliminar pública de junio* contiene los puntos destacados siguientes:  

- **SQL Server Profiler para SQL Operations Studio *Preview***  versión inicial de extensión.
- El nuevo **SQL Data Warehouse** extensión incluye widgets de panel personalizable completo muestra información para el almacenamiento de datos. Esto desbloquea escenarios clave en torno a la administración y ajuste el almacenamiento de datos para asegurarse de que está optimizado para rendimiento coherente.
- **Editar datos "Filtrado y ordenación"** admite.
- **Agente SQL Server de SQL Operations Studio *Preview***  mejoras de extensión para los trabajos y el historial de trabajos vistas.
- Mejorado **Asistente & marco de generador de IU de cuadro de diálogo** API de extensibilidad.
- Actualizar la integración de código de origen de plataforma de código de VS [(1.22) de marzo de 2018](https://code.visualstudio.com/updates/v1_22) y [abril de 2018 (1,23)](https://code.visualstudio.com/updates/v1_23) libera.
- Solucionar problemas de GitHub:
  - Solicitud de característica ([emitir 1204](https://github.com/Microsoft/azuredatastudio/issues/1204)): por favor, que los resultados de ancho de la cuadrícula de ajuste automático de columna a los datos o recordar los cambios manuales si se vuelve a ejecutar la misma consulta.
  - Corregir [emitir 1398](https://github.com/Microsoft/azuredatastudio/issues/1398): debe agregar show del mensaje y el botón Agregar cuenta cuenta cuando la cuenta vinculada está vacía.
  - Corregir [emitir 1399](https://github.com/Microsoft/azuredatastudio/issues/1399): ficha cuenta vinculada se interrumpe cuando se contrae la vista.
  - Corregir [emitir 1374](https://github.com/Microsoft/azuredatastudio/issues/1374): servicio de las herramientas de SQL se bloquea al abrir el archivo .sql desde el disco.
  - Corregir [emitir 1372](https://github.com/Microsoft/azuredatastudio/issues/1372): palabra clave de SQL que faltan "BETWEEN".
  - Corregir [emitir 1395](https://github.com/Microsoft/azuredatastudio/issues/1395): palabra clave 'MATCH', bloquea el servicio de herramientas de SQL.
  - Corregir [emitir 1496](https://github.com/Microsoft/azuredatastudio/issues/1496): opción de menú contextual de "Nueva Profiler" en el Explorador de objetos no hace nada.
  - Corregir [emitir 1495](https://github.com/Microsoft/azuredatastudio/issues/1495): plan de consulta de "Explicación" editor de consultas se interrumpe.


## <a name="may-2018-may-public-preview"></a>Mayo de 2018 (es posible que la versión preliminar pública)

fecha de lanzamiento: 7 de mayo de 2018  
versión: 0.29.3

El *versión preliminar pública puede* se centra en la estabilización y correcciones de errores. Esta compilación contiene los puntos destacados siguientes:  

- Anuncio de extensión de búsqueda de SQL disponible en el Administrador de extensiones.
- Localización de la Comunidad disponible en 10 idiomas: alemán, español, francés, italiano, japonés, coreano, portugués, ruso, chino simplificado y chino tradicional.
- Recopilación de telemetría reducido, una mejor experiencia de participar y vínculos en el producto a la declaración de privacidad.
- Administrador de extensiones tiene Marketplace mejorada experiencia para detectar fácilmente las extensiones de la Comunidad.
- Extensión trabajos del Agente SQL y el historial de trabajos Vista mejora.
- Actualizaciones de whoisactive y extensiones de los informes de servidor.
- Mejorar el desplazamiento de administrar propiedades de panel.
- Solucionar problemas de GitHub:
   - Corregir [emitir 703](https://github.com/Microsoft/azuredatastudio/issues/703): escritura de texto de estilo HTML en datos de edición hace que el valor no se muestran correctamente hasta que la actualización
   - Corregir [emitir 821](https://github.com/Microsoft/azuredatastudio/issues/821): azuredatastudio.deb dependencia del paquete
   - Corregir [emitir 1260](https://github.com/Microsoft/azuredatastudio/issues/1260): palabra clave 'distinct' no resaltado
   - Corregir [emitir 1332](https://github.com/Microsoft/azuredatastudio/issues/1332): reversión edición datos fila no funciona
   - Corregir [emitir 1215](https://github.com/Microsoft/azuredatastudio/issues/1215): extensión del Agente SQL y la barra de estado
   - Corregir [emitir 1316](https://github.com/Microsoft/azuredatastudio/issues/1316): cambiar el tamaño no de agente SQL después de cambiar el tamaño de windows




## <a name="april-2018-april-public-preview"></a>Abril de 2018 (abril Public Preview)

fecha de publicación: 25 de abril de 2018  
versión: 0.28.6

El *versión preliminar pública de abril* contiene correcciones de errores y mejoras. 

- Mejoras en la extensión de la versión preliminar del agente de SQL.
- Archivo protegido y gran compatibilidad mejorada para guardar administrador protegido y > 256 millones de archivos dentro de SQL Operations Studio.
- Terminal integrado de división para trabajar con varios terminales abiertos al mismo tiempo.
- Imprimir pies de recuento de archivo en disco de instalación reducido para instalaciones más rápidas y tiempos de inicio.
- Continuar solucionar problemas de GitHub:
   - Corregir [emitir 37](https://github.com/Microsoft/azuredatastudio/issues/37): cuando el Visor gráfico produce un error, se produce un comportamiento inesperado.
   - Corregir [emitir 462](https://github.com/Microsoft/azuredatastudio/issues/462): solicitud de característica: opción para grupos de servidores se expanda de forma predeterminada.
   - Corregir [emitir 606](https://github.com/Microsoft/azuredatastudio/issues/606): intellisense - propuesta no válida para el comando 'update'.
   - Corregir [emitir 967](https://github.com/Microsoft/azuredatastudio/issues/967): esperar el plan de consulta cuando selecciona el plan de presentación XML en la cuadrícula de resultados.
   - Corregir [emitir 1023](https://github.com/Microsoft/azuredatastudio/issues/1023): agregar corchetes para llamada ms_foreachdb desde flyfishingdba.
   - Corregir [emitir 1048](https://github.com/Microsoft/azuredatastudio/issues/1048): error de protocolo de enlace de inicio de sesión previo SSL/TLS.
   - Corregir [emitir 1050](https://github.com/Microsoft/azuredatastudio/issues/1050): ver información clara antes de mostrar el error.
   - Corregir [emitir 1057](https://github.com/Microsoft/azuredatastudio/issues/1057): nuevas acciones de consulta en el Explorador de widget y restauración se interrumpen.
   - Corregir [emitir 1068](https://github.com/Microsoft/azuredatastudio/issues/1068): panel Salida windows pop-up con mensaje de error para la base de datos de SQL Azure.
   - Corregir [emitir 1069](https://github.com/Microsoft/azuredatastudio/issues/1069): error de servidor necesario cuando se muestra inicialmente se muestra el cuadro de diálogo conexión.
   - Corregir [emitir 1070](https://github.com/Microsoft/azuredatastudio/issues/1070): grupos de servidores requieren ahora un doble clic para expandir.
   - Corregir [emitir 1072](https://github.com/Microsoft/azuredatastudio/issues/1072): es parcialmente transparente en segundo plano de control de selección.
   - Corregir [emitir 1115](https://github.com/Microsoft/azuredatastudio/issues/1115): Corregir contraste alto todos los problemas de accesibilidad en SQL Operations Studio.
   - Corregir [emitir 1101](https://github.com/Microsoft/azuredatastudio/issues/1101): se produce un error de extensión al vínculo de actualización "descargar manualmente" se dirige a una ubicación incorrecta.
   - Corregir [emitir 1103](https://github.com/Microsoft/azuredatastudio/issues/1103): desplazamiento V no está trabajando en la ficha Inicio.
   - Corregir [emitir 1104](https://github.com/Microsoft/azuredatastudio/issues/1104): fichas de la extensión SQL dejó de funcionar.


Un resaltado significativo para la versión preliminar pública de abril es la actualización de código de origen de plataforma 1.21 de código de Visual Studio. Esto introduce varias actualizaciones para el editor de núcleo y workbench desde el punto de 1.19 sincronización anterior. Algunos ejemplos incluyen lo siguiente:

- [Nueva interfaz de usuario de notificaciones](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui) : administrar fácilmente y revisar las notificaciones de SQL Operations Studio.
- [Integra la división Terminal](https://code.visualstudio.com/updates/v1_21#_split-terminals) -trabajar con varios terminales abiertos al mismo tiempo.
- [Guardar los archivos protegidos y grandes](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges) : guarda administrador protegido y > 256 millones de archivos dentro de SQL Operations Studio.
- [Ha mejorado la compatibilidad con archivos grandes](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements) -optimizaciones de búfer de texto para archivos de gran tamaño.
- [Búsqueda de configuración mejorada](https://code.visualstudio.com/updates/v1_20#_settings-search) - fácil encontrar la configuración correcta con búsqueda en lenguaje natural.
- [Fragmentos de código globales](https://code.visualstudio.com/updates/v1_20#_global-snippets) -crear fragmentos de código que se puede usar en todos los tipos de archivo.
- [Selección múltiple de explorador](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer) -realizar acciones en varios archivos a la vez.
- [Errores y advertencias en el explorador](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer) : rápidamente ir a los errores en la base de código.
- [Arrastrar y colocar, copiar y pegar a través de windows](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support) -moverlos entre ventanas abiertas de SQL Operations Studio.
- [Soporte técnico de submódulo de GIT](https://code.visualstudio.com/updates/v1_20#_git-submodules) -Git realizar operaciones en repositorios Git anidados.
- [Compatibilidad con lectores de pantalla de Terminal](https://code.visualstudio.com/updates/v1_20#_screen-reader-support) -Terminal integrado ahora tiene el modo "Optimizado de lector de pantalla".
- [Diseño del editor centrado](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout) -maximizar el espacio en pantalla de visualización de código.
- [Resultados de búsqueda horizontal (versión preliminar)](https://code.visualstudio.com/updates/v1_21#_horizontal-search) -pueden ahora ver los resultados en un panel horizontal.

Para obtener más detalles, desproteger el [notas de versión de febrero de código de Visual Studio](https://code.visualstudio.com/updates/v1_21)y el [notas de versión de enero de código de Visual Studio](https://code.visualstudio.com/updates/v1_20).

Para obtener más información, consulte el [registro de cambios](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md).

## <a name="march-2018-march-public-preview"></a>Marzo de 2018 (versión preliminar pública de marzo)

fecha de lanzamiento: 28 de marzo de 2018  
versión: 0.27.3

El *versión preliminar pública de marzo* continúa abordar los principales problemas de GitHub y se centra en mejorar nuestra historia de extensibilidad. Activar específicamente el Administrador de extensiones, mejorar la administración del panel y proporcione el Agente SQL y las extensiones de insights. Esta versión incluye las siguientes mejoras:

- Mejorar el modelo de extensibilidad de panel para admitir información con pestañas y paneles de configuración.
   - Administrador de extensiones permite simple adquisición de extensiones.
   - Las extensiones del panel para sp_whoisactive desde [whoisactive.com](http://www.whoisactive.com).
   - Para obtener más información, consulte [amplían la funcionalidad de SQL Operations Studio](extensions.md).
- Agregar más [API de extensibilidad para la conexión y el objeto explorer](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API) administración.
- Seguir corrigiendo clientes importantes que afectan a [problemas de GitHub](https://github.com/Microsoft/azuredatastudio/issues).


## <a name="february-2018-february-public-preview"></a>Febrero de 2018 (versión preliminar pública de febrero)

fecha de lanzamiento: 15 de febrero de 2018  
versión: 0.26.7

El *versión preliminar pública de febrero* incluye algunas sugerencias de características y correcciones de errores de alta prioridad. Esta versión incluye las siguientes mejoras:

- Introducción a la instalación de actualización automática, que proporciona una notificación cuando esté disponible para descargar una nueva versión 
- El campo de cuadro de diálogo de conexión 'Database' es ahora una lista desplegable rellena dinámicamente que contendrá una lista de bases de datos que se rellena desde el servidor especificado.
- Corregir [emitir 6](https://github.com/Microsoft/azuredatastudio/issues/6): mantener la conexión y la base de datos seleccionada al abrir nuevas pestañas de consulta.
- ¿Corregir [emitir 22](https://github.com/Microsoft/azuredatastudio/issues/22): 'Server Name' y 'Nombre de base de datos -' estos pueden ser listas desplegables en lugar de los cuadros de texto?
- Corregir [emitir 549](https://github.com/Microsoft/azuredatastudio/issues/549): instalación silenciosa de muy/Silent da como resultado de apertura después de la instalación de aplicación.
- Corregir [emitir 481](https://github.com/Microsoft/azuredatastudio/issues/481): agregar la opción "Buscar actualizaciones".
- Editor SQL coloración y correcciones de finalización automática:
   - Corregir [emitir 584](https://github.com/Microsoft/azuredatastudio/issues/584): palabra clave "FULL" no resaltado por IntelliSense.
   - Corregir [emitir 345](https://github.com/Microsoft/azuredatastudio/issues/345): funciones SQL colorear dentro del editor.
   - Corregir [emitir 300](https://github.com/Microsoft/azuredatastudio/issues/300): [#tempData] más reciente "]" se mostrará de color verde.
   - Corregir [emitir 225](https://github.com/Microsoft/azuredatastudio/issues/225): error de coincidencia de color de palabra clave.
   - Corregir [emitir 60](https://github.com/Microsoft/azuredatastudio/issues/60): sql no válido color resaltado de sintaxis cuando se usa una tabla temporal en cláusula from.
- Introducir la API de extensibilidad de conexión.
- Integración de VS 1.19 del Editor de código.
- Actualizar componente JustinPealing/html--plan de consulta para la recogida varias mejoras del Visor de Plan de consulta.


## <a name="january-2018-january-public-preview"></a>Enero de 2018 (versión preliminar pública de enero)

fecha de lanzamiento: 17 de enero de 2018  
versión: 0.25.4

El *versión preliminar pública de enero* incluye algunas sugerencias de características y correcciones de errores de alta prioridad. Esta versión incluye las siguientes mejoras:

- Guardado de las conexiones de servidor están disponibles en el cuadro de diálogo de conexión.
- Habilitar salida activo. Salida activo está desactivada de forma predeterminada, al habilitar vea [configuración activa exit](settings.md#hot-exit).
- Según el grupo de servidores de colores de pestaña. Color de ficha está desactivada de forma predeterminada, al habilitar vea [pestaña Configuración de color](settings.md#tab-color).
- Cambio *nombre del servidor* a *Server* en el cuadro de diálogo de conexión.
- Corrección dividida *ejecutar la consulta actual* comando.
- Corregir errores de secuencias de comandos de separación de arrastrar y colocar.
- Corregir incorrectos de los iconos anclados menú Inicio.
- Falta la cuenta de Azure icono de personalización de marca de corregir.


## <a name="december-2017-december-public-preview"></a>Diciembre de 2017 (versión preliminar pública de diciembre)

fecha de lanzamiento: 19 de diciembre de 2017  
versión: 0.24.1

El *versión preliminar pública de diciembre* incluye varias correcciones de errores en todas las áreas de características, así como las siguientes mejoras:

- Crear cuadro de diálogo de regla de Firewall ahora está disponible para ayudar a conectar a Azure SQL Database y Azure SQL Data Warehouse.
- Se ha agregado el programa de instalación de Windows y Linux DEB y RPM paquetes de instalación.
- Administrar el editor de diseño visual del panel.
- *Secuencia de comandos como Alter* y *como la ejecución del Script* comandos.
- *Ejecutar la consulta actual con el Plan real* comando.
- Integración de plataforma del editor de VS Code 1.18.1.
- Habilitar los archivos de instalación de prueba de la extensión VSIX.
- Admite la sintaxis de iteración de "N GO" por lotes.


## <a name="november-2017"></a>Noviembre de 2017

fecha de lanzamiento: 15 de noviembre de 2017  
versión: 0.23.6

- Versión inicial del [!INCLUDE[name-sos](../includes/name-sos-short.md)].


## <a name="next-steps"></a>Pasos siguientes

Consulte uno de los siguientes tutoriales para empezar a trabajar:
- [Conectar y consultar SQL Server](quickstart-sql-server.md)
- [Conectar y consultar la base de datos SQL Azure](quickstart-sql-database.md)
- [Conectar y consultar el almacén de datos de Azure](quickstart-sql-dw.md)

Contribuir a [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
