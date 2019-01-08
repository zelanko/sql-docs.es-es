---
title: Notas de la versión y el registro de cambios
titleSuffix: Azure Data Studio
description: Notas de la versión de Data Studio Azure
ms.custom: seodec18
ms.date: 11/06/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 22542b42aff4b6d2d37e4a7342395d154d16dc95
ms.sourcegitcommit: 189a28785075cd7018c98e9625c69225a7ae0777
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2018
ms.locfileid: "53030349"
---
# <a name="azure-data-studio-latest-release-notes-and-changelog"></a>Notas de versión más recientes de Studio de datos y registro de cambios de Azure

**[Descargue la versión de noviembre.](download.md)**

## <a name="november-2018-november-release"></a>Noviembre de 2018 (versión de noviembre)

fecha de lanzamiento: 6 de noviembre de 2018  
Versión: 1.2.4

- Actualizar a la [extensión de versión preliminar de SQL Server de 2019](https://docs.microsoft.com/sql/azure-data-studio/sql-server-2019-extension?view=sql-server-ver15)
- Pegar la extensión del Plan de presentación
- Introducción a la extensión de las consultas de color de alta densidad, incluido el tema del editor de SSMS
- Correcciones en las extensiones de agente SQL Server Profiler e importación
- .Net Core de corregir la causa del problema de Socket KeepAlive quita conexiones inactivas en macOS
- Servicio de las herramientas de actualización de SQL a.Net Core 2,2 Preview 3 (para la compatibilidad con AAD eventual)

### <a name="bug-fixes"></a>Correcciones de errores
- Corregir [emitir #2933](https://github.com/Microsoft/azuredatastudio/issues/2933): Conexión perdida a Azure SQL DB
- Corregir [emitir 2914 #](https://github.com/Microsoft/azuredatastudio/issues/2914): Nodo de base de datos de "Argumento no válido" excepción expansión OE
- Corregir [emitir #2935](https://github.com/Microsoft/azuredatastudio/pull/2935): Los mensajes de varias líneas se muestran correctamente en los resultados de consulta
- Corregir [emitir 2906 #](https://github.com/Microsoft/azuredatastudio/pull/2906): Corrija el nombre del documento editar datos al nombre de la tabla contiene caracteres especiales
- Corregir [emitir #2929](https://github.com/Microsoft/azuredatastudio/issues/2929): Integrado en la extensión de registro de cambios indica comprobar las notas de VSCode de cambios
- Corregir [emitir #2719](https://github.com/Microsoft/azuredatastudio/issues/2719): El tema de contraste alto dobles/triples iconos
- Corregir [emitir #3047](https://github.com/Microsoft/azuredatastudio/pull/3047): Agregar una interfaz de línea de comandos para conectarse a un servidor SQL Server
- Corregir [emitir #3031](https://github.com/Microsoft/azuredatastudio/pull/3031): Agregar compatibilidad de tema del plan de consulta
- …

Para obtener información detallada, consulte el [registro de cambios](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), y [versiones](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="october-2018-october-release"></a>Octubre de 2018 (versión de octubre)

fecha de lanzamiento: 29 de octubre de 2018  
Versión: 1.1.4

- Introducción a Azure Resource Explorer para examinar las bases de datos SQL de Azure
- Mejorar la solidez de conectividad del explorador de objetos y el Editor de consultas
- Mejoras de las extensiones de agente SQL
- Actualizar a la [extensión de versión preliminar de SQL Server de 2019](https://docs.microsoft.com/sql/azure-data-studio/sql-server-2019-extension?view=sql-server-ver15)

### <a name="bug-fixes"></a>Correcciones de errores
- Corregir [emitir 2717 #](https://github.com/Microsoft/azuredatastudio/issues/2717): Resultado de la columna XML, haga clic en formato
- Corregir [emitir #2993](https://github.com/Microsoft/azuredatastudio/issues/2993): Windows de resultado del ancho es incompleta
- Corregir [emitir 2999 #](https://github.com/Microsoft/azuredatastudio/issues/2999): No se pudo cargar el archivo System.Diagnostics.Tracing en Mac al conectarse a la base de datos
- Corregir [emitir 2851 #](https://github.com/Microsoft/azuredatastudio/issues/2851): Gráfico de serie temporal no se representará correctamente
- Corregir [emitir 2996 #](https://github.com/Microsoft/azuredatastudio/issues/2996): Pérdida de la tabla temporal debido a cambios repentinos de sesión
- …

Para obtener información detallada, consulte el [registro de cambios](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), y [versiones](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="september-2018-september-ga-release"></a>(Versión de septiembre GA) de septiembre de 2018

fecha de lanzamiento: 24 de septiembre de 2018  
Versión: 1,0

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
  - Asistente para la tabla externa de creación de SQL Server PolyBase
    - Crear una tabla externa y sus estructuras de metadatos compatibles con un asistente fácil de usar. En esta versión, se admiten servidores remotos de SQL Server y Oracle.
- Rendimiento de la cuadrícula de resultados y las mejoras de la experiencia de usuario de gran número de conjuntos de resultados de consulta.
- Actualizar código fuente de Visual Studio Code desde 1,23 a 1.26.1 con el diseño de cuadrícula y ha mejorado el Editor de configuración (versión preliminar).
- Mejoras de accesibilidad para el lector de pantalla, navegación mediante el teclado y alto contraste.
- Agregar `Connection name` opción para proporcionar un nombre alternativo en la vista de servidores-let.

### <a name="bug-fixes"></a>Correcciones de errores

- Corregir [emitir #2647](https://github.com/Microsoft/azuredatastudio/issues/143): Los gráficos dio un gran paso hacia atrás.
- Corregir [emitir #2648](https://github.com/Microsoft/azuredatastudio/issues/143): SELECT que devuelve toda la columna de los hipervínculos JSON.
- …

Para obtener información detallada, consulte el [registro de cambios](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), y [versiones](https://github.com/Microsoft/azuredatastudio/releases).


## <a name="august-2018-august-public-preview"></a>Agosto de 2018 (versión preliminar pública de agosto)

fecha de lanzamiento: 30 de agosto de 2018  
Versión: 0.32.8

*0.32.8 contiene correcciones para un par regresiones se encuentra en 0.32.7 ([#1971](https://github.com/Microsoft/azuredatastudio/issues/1971), [2372 #](https://github.com/Microsoft/azuredatastudio/issues/2372)*)

El *versión preliminar pública de agosto* se centra en correcciones de errores, la estabilización de producto y rellenando los huecos en los escenarios existentes.  

- Anuncio de la extensión de importación SQL Server
- Administración de sesiones de SQL Server Profiler
- Compatibilidad con plantillas de sesión de SQL Server Profiler
- Mejoras del Agente SQL Server
- Nueva extensión de la Comunidad: Kit de primer servicio de respuesta
- Mejoras de calidad de vida: Cadenas de conexión

### <a name="bug-fixes"></a>Correcciones de errores

- Analizar SQL en una ventana del Editor de consultas mediante el `Parse Syntax` comando.
- Corregir [emitir #143](https://github.com/Microsoft/azuredatastudio/issues/143): Haga doble clic en seleccionar no en nombre de variable.
- Corregir [emitir #387](https://github.com/Microsoft/azuredatastudio/issues/387): Icono de la pestaña base de datos SQL está en rojo.
- Corregir [emitir 825 #](https://github.com/Microsoft/azuredatastudio/issues/825): Solicitud: Conexión automática al servidor actual después de la secuencia de comandos como... 
- Corregir [emitir 1278 #](https://github.com/Microsoft/azuredatastudio/issues/1278): sqlops.desktop [Entry escritorio] - valor redundante para el nombre de & comentario.
- Corregir [emitir 1285 #](https://github.com/Microsoft/azuredatastudio/issues/1285): Actualizando el icono de la aplicación hace que se quitan o reemplazan en Windows.
- Corregir [emitir 1317 #](https://github.com/Microsoft/azuredatastudio/issues/1317): Corrija el separador decimal.
- Corregir [emitir 1474 #](https://github.com/Microsoft/azuredatastudio/issues/1474): Cancelar cambio de conexión desconecta la conexión actual.
- Corregir [emitir 1497 #](https://github.com/Microsoft/azuredatastudio/issues/1497): Ver como se cortan las opciones en la parte inferior del gráfico.
- Corregir [emitir 1524 #](https://github.com/Microsoft/azuredatastudio/issues/1524): Panel/shell: Iconos de viewlet principal son arrastrables y pueden bloquear la aplicación.
- Corregir [emitir 1578 #](https://github.com/Microsoft/azuredatastudio/issues/1578): No se puede expandir o contraer carpeta del explorador de archivos remoto, haga clic en el nombre.
- Corregir [emitir 1620 #](https://github.com/Microsoft/azuredatastudio/issues/1620): Sugerencia de característica: Obtener la cadena de conexión para la conexión existente.
- Corregir [emitir 1624 #](https://github.com/Microsoft/azuredatastudio/issues/1624): SelectBox no cambia de color cuando se deshabilita.
- Corregir [emitir 1728 #](https://github.com/Microsoft/azuredatastudio/issues/1728): Guardar como JSON o EXCEL o CSV no funcionan.
- Corregir [emitir #1744](https://github.com/Microsoft/azuredatastudio/issues/1744): Panel de resultados pierde sus posiciones de desplazamiento al cambiar entre pestañas.
- Corregir [emitir 1748 #](https://github.com/Microsoft/azuredatastudio/issues/1748): Mensaje de error al guardar la hora de archivo segunda (y posteriores) de Excel.
- Corregir [emitir 1782 #](https://github.com/Microsoft/azuredatastudio/issues/1782): Editar datos: celda no revierta al valor original de presionar la tecla ESC.
- Corregir [emitir 1836 #](https://github.com/Microsoft/azuredatastudio/issues/1836): los archivos .sql que no está asociados con SQL Operations Studio.
- Corregir [emitir 1850 #](https://github.com/Microsoft/azuredatastudio/issues/1850): Escribe N'' completa automáticamente a N'' '.
- Corregir [emitir 1985 #](https://github.com/Microsoft/azuredatastudio/issues/1985): Copia de cuadrícula de resultados de consulta está desactivada de forma 1 columna.
- Corregir [emitir 1998 #](htpts://github.com/Microsoft/azuredatastudio/pull/1998): Agregar la versión de VS Code para sobre el cuadro de diálogo.
- Corregir [emitir 2042 #](https://github.com/Microsoft/azuredatastudio/pull/2042): : Habilita el botón Importar consultas desde archivos de sql.
- Corregir [emitir 2091 #](https://github.com/Microsoft/azuredatastudio/issues/2091): No puede usar el método abreviado Ctrl + C para copiar desde el panel de resultados.
- Corregir [emitir 2099 #](https://github.com/Microsoft/azuredatastudio/pull/2099): Agregar más opciones saveAsCsv.
- Corregir [emitir 2107 #](https://github.com/Microsoft/azuredatastudio/issues/2107): Actualiza el icono de documento para los documentos de panel y Profiler.
- Corregir [emitir #2129](https://github.com/Microsoft/azuredatastudio/pull/2129): Guardar la posición de desplazamiento de datos de edición al cambiar de fichas.
- Corregir [emitir 2152 #](https://github.com/Microsoft/azuredatastudio/issues/2152): Indicador de fila de la cuadrícula de resultados basado en cero.

## <a name="known-issues"></a>Problemas conocidos

- [Problema #2371](https://github.com/Microsoft/azuredatastudio/issues/2371) Guardar como sólo guarda primera fila de datos de Excel
- [Problema #2150](https://github.com/Microsoft/azuredatastudio/issues/2150): No se puede conectar en Ubuntu 16.04 para SQL en un contenedor


## <a name="july-2018-july-public-preview"></a>Julio de 2018 (versión preliminar pública de julio)

fecha de lanzamiento: 19 de julio de 2018  
Versión: 0.31.4

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
 - Corregir [emitir 728](https://github.com/Microsoft/azuredatastudio/issues/728): Ninguna respuesta al agregar conexión en macOS
 - Corregir [emitir 1612](https://github.com/Microsoft/azuredatastudio/issues/1612): Presentación del texto de cuadrícula de resultados está equivocada por caracteres internacionales
 - Corregir [emitir 1693](https://github.com/Microsoft/azuredatastudio/issues/1693): Cuadro de diálogo copia de seguridad: Se ha interrumpido la interfaz de usuario del explorador de archivos
 - Corregir [emitir 1713](https://github.com/Microsoft/azuredatastudio/issues/1713): Número de filas afectadas
 - Corregir [emitir 1718](https://github.com/Microsoft/azuredatastudio/issues/1718): No se puede conectar a cualquier origen de datos
 - Corregir [emitir 1719](https://github.com/Microsoft/azuredatastudio/issues/1719): TypeError al conectarse al servidor
 - Corregir [emitir 1724](https://github.com/Microsoft/azuredatastudio/issues/1724): Los cuadros de diálogo extensión han dejado de funcionar
 - Corregir [emitir 1749](https://github.com/Microsoft/azuredatastudio/issues/1749): ERROR: Se interpretan los datos HTML en una columna
 - Corregir [emitir 1789](https://github.com/Microsoft/azuredatastudio/issues/1789): Extensibilidad: si agrega un proveedor de conexión desinstalar nunca quitará de la lista
 - Corregir [emitir 1791](https://github.com/Microsoft/azuredatastudio/issues/1791): Las extensiones de Sqlops: queryeditor.connect() se conecta a la base de datos de destino, pero no muestra la interfaz de usuario que está conectado el editor
 - Corregir [emitir 1799](https://github.com/Microsoft/azuredatastudio/issues/1799): Gráfico de tamaño de 10 DB superior no funciona en las instancias distingue mayúsculas de minúsculas
 - Corregir [emitir 1814](https://github.com/Microsoft/azuredatastudio/issues/1814): definición de tipo de error de escritura sqlops.d.ts causando implícito 'any'
 - Corregir [emitir 1817](https://github.com/Microsoft/azuredatastudio/issues/1817): Error de Ortografia
 - Corregir [emitir 1830](https://github.com/Microsoft/azuredatastudio/issues/1830): Establecer iconPath en ButtonComponent después de llamar a component() no cambia el icono
 - Corregir [emitir 1843](https://github.com/Microsoft/azuredatastudio/issues/1843): Una mejor organización de la tabla


## <a name="june-2018-june-public-preview"></a>Junio de 2018 (versión preliminar de junio público)

fecha de lanzamiento: 20 de junio de 2018  
Versión: 0.30.6

El *versión preliminar pública de junio* contiene los puntos destacados siguientes:  

- **SQL Server Profiler para SQL Operations Studio *Preview***  versión inicial de extensión.
- El nuevo **SQL Data Warehouse** extensión incluye widgets de panel personalizable completo muestra información para el almacenamiento de datos. Esto desbloquea escenarios clave en torno a la administración y ajuste el almacenamiento de datos para asegurarse de que está optimizado para rendimiento coherente.
- **Editar datos "Filtrado y ordenación"** admite.
- **Agente SQL Server de SQL Operations Studio *Preview***  mejoras de extensión para los trabajos y el historial de trabajos vistas.
- Mejorado **Asistente & marco de generador de IU de cuadro de diálogo** API de extensibilidad.
- Actualizar la integración de código de origen de plataforma de código de VS [(1.22) de marzo de 2018](https://code.visualstudio.com/updates/v1_22) y [abril de 2018 (1,23)](https://code.visualstudio.com/updates/v1_23) libera.
- Solucionar problemas de GitHub:
  - Solicitud de característica ([emitir 1204](https://github.com/Microsoft/azuredatastudio/issues/1204)): Por favor, que los resultados de ancho de la cuadrícula de ajuste automático de columna a los datos o recordar los cambios manuales si la misma consulta se vuelve a ejecutar.
  - Corregir [emitir 1398](https://github.com/Microsoft/azuredatastudio/issues/1398): Debe mostrar Agregar mensaje y botón Agregar cuenta cuenta cuando la cuenta vinculada está vacía.
  - Corregir [emitir 1399](https://github.com/Microsoft/azuredatastudio/issues/1399): Ficha cuenta vinculada se interrumpe cuando se contrae la vista.
  - Corregir [emitir 1374](https://github.com/Microsoft/azuredatastudio/issues/1374): Herramientas de servicio de SQL se bloquea al abrir el archivo .sql desde el disco.
  - Corregir [emitir 1372](https://github.com/Microsoft/azuredatastudio/issues/1372): Falta la palabra clave SQL "BETWEEN".
  - Corregir [emitir 1395](https://github.com/Microsoft/azuredatastudio/issues/1395): Palabra clave 'MATCH' bloquea el servicio de herramientas de SQL.
  - Corregir [emitir 1496](https://github.com/Microsoft/azuredatastudio/issues/1496): "Nuevo Profiler" opción de menú contextual en el Explorador de objetos no hace nada.
  - Corregir [emitir 1495](https://github.com/Microsoft/azuredatastudio/issues/1495): Plan de consulta de "Explicación" editor de consultas se interrumpe.


## <a name="may-2018-may-public-preview"></a>Mayo de 2018 (es posible que la versión preliminar pública)

fecha de lanzamiento: 7 de mayo de 2018  
Versión: 0.29.3

El *versión preliminar pública puede* se centra en la estabilización y correcciones de errores. Esta compilación contiene los puntos destacados siguientes:  

- Anuncio de extensión de búsqueda de SQL disponible en el Administrador de extensiones.
- Localización de comunidad para 10 idiomas disponible: Chino alemán, español, francés, italiano, japonés, coreano, portugués, ruso, simplificado y chino tradicional.
- Recopilación de telemetría reducido, una mejor experiencia de participar y vínculos en el producto a la declaración de privacidad.
- Administrador de extensiones tiene Marketplace mejorada experiencia para detectar fácilmente las extensiones de la Comunidad.
- Extensión trabajos del Agente SQL y el historial de trabajos Vista mejora.
- Actualizaciones de whoisactive y extensiones de los informes de servidor.
- Mejorar el desplazamiento de administrar propiedades de panel.
- Solucionar problemas de GitHub:
   - Corregir [emitir 703](https://github.com/Microsoft/azuredatastudio/issues/703): Escritura de texto de estilo HTML en datos de edición hace que el valor no se muestran correctamente hasta que la actualización
   - Corregir [emitir 821](https://github.com/Microsoft/azuredatastudio/issues/821): azuredatastudio.deb dependencia del paquete
   - Corregir [emitir 1260](https://github.com/Microsoft/azuredatastudio/issues/1260): Palabra clave 'distinct' no resaltado
   - Corregir [emitir 1332](https://github.com/Microsoft/azuredatastudio/issues/1332): Editar datos revertir fila no funciona
   - Corregir [emitir 1215](https://github.com/Microsoft/azuredatastudio/issues/1215): Extensión del Agente SQL y la barra de estado
   - Corregir [emitir 1316](https://github.com/Microsoft/azuredatastudio/issues/1316): Cambio de tamaño no de agente SQL después de cambiar el tamaño de windows




## <a name="april-2018-april-public-preview"></a>Abril de 2018 (abril Public Preview)

fecha de lanzamiento: 25 de abril de 2018  
Versión: 0.28.6

El *versión preliminar pública de abril* contiene correcciones de errores y mejoras. 

- Mejoras en la extensión de la versión preliminar del agente de SQL.
- Archivo protegido y gran compatibilidad mejorada para guardar administrador protegido y > 256 millones de archivos dentro de SQL Operations Studio.
- Terminal integrado de división para trabajar con varios terminales abiertos al mismo tiempo.
- Imprimir pies de recuento de archivo en disco de instalación reducido para instalaciones más rápidas y tiempos de inicio.
- Continuar solucionar problemas de GitHub:
   - Corregir [emitir 37](https://github.com/Microsoft/azuredatastudio/issues/37): Cuando el Visor gráfico produce un error, se produce un comportamiento inesperado.
   - Corregir [emitir 462](https://github.com/Microsoft/azuredatastudio/issues/462): Solicitud de característica: Opción para grupos de servidores se expanda de forma predeterminada.
   - Corregir [emitir 606](https://github.com/Microsoft/azuredatastudio/issues/606): intellisense - propuesta no válida para el comando 'update'.
   - Corregir [emitir 967](https://github.com/Microsoft/azuredatastudio/issues/967): Espera que el plan de consulta cuando selecciona el plan de presentación XML en la cuadrícula de resultados.
   - Corregir [emitir 1023](https://github.com/Microsoft/azuredatastudio/issues/1023): Agregue los corchetes para llamada ms_foreachdb desde flyfishingdba.
   - Corregir [emitir 1048](https://github.com/Microsoft/azuredatastudio/issues/1048): Error de protocolo de enlace SSL/TLS de inicio de sesión previo.
   - Corregir [emitir 1050](https://github.com/Microsoft/azuredatastudio/issues/1050): Ver información clara antes de mostrar el error.
   - Corregir [emitir 1057](https://github.com/Microsoft/azuredatastudio/issues/1057): Nuevas acciones de consulta en el Explorador de widget y restauración se interrumpen.
   - Corregir [emitir 1068](https://github.com/Microsoft/azuredatastudio/issues/1068): Panel Salida windows pop-up con mensaje de error para la base de datos de SQL Azure.
   - Corregir [emitir 1069](https://github.com/Microsoft/azuredatastudio/issues/1069): Cuadro de diálogo conexión muestra el error de servidor necesario cuando se muestra inicialmente.
   - Corregir [emitir 1070](https://github.com/Microsoft/azuredatastudio/issues/1070): Grupos de servidores requieren ahora un doble clic para expandir.
   - Corregir [emitir 1072](https://github.com/Microsoft/azuredatastudio/issues/1072): En segundo plano de control de selección es semitransparente.
   - Corregir [emitir 1115](https://github.com/Microsoft/azuredatastudio/issues/1115): Corregir contraste alto todos los problemas de accesibilidad en SQL Operations Studio.
   - Corregir [emitir 1101](https://github.com/Microsoft/azuredatastudio/issues/1101): Se produce un error de extensión al vínculo de actualización "descargar manualmente" se dirige a una ubicación incorrecta.
   - Corregir [emitir 1103](https://github.com/Microsoft/azuredatastudio/issues/1103): Desplazamiento de V no está trabajando en la ficha Inicio.
   - Corregir [emitir 1104](https://github.com/Microsoft/azuredatastudio/issues/1104): Fichas de la extensión SQL dejó de funcionar.


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
Versión: 0.27.3

El *versión preliminar pública de marzo* continúa abordar los principales problemas de GitHub y se centra en mejorar nuestra historia de extensibilidad. Activar específicamente el Administrador de extensiones, mejorar la administración del panel y proporcione el Agente SQL y las extensiones de insights. Esta versión incluye las siguientes mejoras:

- Mejorar el modelo de extensibilidad de panel para admitir información con pestañas y paneles de configuración.
   - Administrador de extensiones permite simple adquisición de extensiones.
   - Las extensiones del panel para sp_whoisactive desde [whoisactive.com](http://www.whoisactive.com).
   - Para obtener más información, consulte [amplían la funcionalidad de SQL Operations Studio](extensions.md).
- Agregar más [API de extensibilidad para la conexión y el objeto explorer](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API) administración.
- Seguir corrigiendo clientes importantes que afectan a [problemas de GitHub](https://github.com/Microsoft/azuredatastudio/issues).


## <a name="february-2018-february-public-preview"></a>Febrero de 2018 (versión preliminar pública de febrero)

fecha de lanzamiento: 15 de febrero de 2018  
Versión: 0.26.7

El *versión preliminar pública de febrero* incluye algunas sugerencias de características y correcciones de errores de alta prioridad. Esta versión incluye las siguientes mejoras:

- Introducción a la instalación de actualización automática, que proporciona una notificación cuando esté disponible para descargar una nueva versión 
- El campo de cuadro de diálogo de conexión 'Database' es ahora una lista desplegable rellena dinámicamente que contendrá una lista de bases de datos que se rellena desde el servidor especificado.
- Corregir [emitir 6](https://github.com/Microsoft/azuredatastudio/issues/6): Mantenga la conexión y la base de datos seleccionada al abrir nuevas pestañas de consulta.
- Corregir [emitir 22](https://github.com/Microsoft/azuredatastudio/issues/22): ¿' Server Name' y 'Nombre de base de datos -' estos pueden ser listas desplegables en lugar de los cuadros de texto?
- Corregir [emitir 549](https://github.com/Microsoft/azuredatastudio/issues/549): Instalación silenciosa de muy/silent da lugar a abrir después de la instalación de aplicación.
- Corregir [emitir 481](https://github.com/Microsoft/azuredatastudio/issues/481): Agregue la opción "Buscar actualizaciones".
- Editor SQL coloración y correcciones de finalización automática:
   - Corregir [emitir 584](https://github.com/Microsoft/azuredatastudio/issues/584): Palabra clave "Completa" no resaltada por IntelliSense.
   - Corregir [emitir 345](https://github.com/Microsoft/azuredatastudio/issues/345): Colorear las funciones SQL en el editor.
   - Corregir [emitir 300](https://github.com/Microsoft/azuredatastudio/issues/300): [#tempData] más reciente "]" se mostrará de color verde.
   - Corregir [emitir 225](https://github.com/Microsoft/azuredatastudio/issues/225): Error de coincidencia de color de palabra clave.
   - Corregir [emitir 60](https://github.com/Microsoft/azuredatastudio/issues/60): Sql no válido color resaltado de sintaxis cuando se usa una tabla temporal en cláusula from.
- Introducir la API de extensibilidad de conexión.
- Integración de VS 1.19 del Editor de código.
- Actualizar componente JustinPealing/html--plan de consulta para la recogida varias mejoras del Visor de Plan de consulta.


## <a name="january-2018-january-public-preview"></a>Enero de 2018 (versión preliminar pública de enero)

fecha de lanzamiento: 17 de enero de 2018  
Versión: 0.25.4

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
Versión: 0.24.1

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
Versión: 0.23.6

- Versión inicial del [!INCLUDE[name-sos](../includes/name-sos-short.md)].


## <a name="next-steps"></a>Pasos siguientes

Consulte uno de los siguientes tutoriales para empezar a trabajar:
- [Conectar y consultar SQL Server](quickstart-sql-server.md)
- [Conectar y consultar la base de datos SQL Azure](quickstart-sql-database.md)
- [Conectar y consultar el almacén de datos de Azure](quickstart-sql-dw.md)

Contribuir a [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
