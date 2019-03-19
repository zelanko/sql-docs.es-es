---
title: Notas de la versión
titleSuffix: Azure Data Studio
description: Notas de la versión de Data Studio Azure
ms.custom: seodec18
ms.date: 03/06/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 746f3d97ed0157f6b97128dbfdf1b88a5276062c
ms.sourcegitcommit: 11ab8a241a6d884b113b3cf475b2b9ed61ff00e3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/18/2019
ms.locfileid: "58161632"
---
# <a name="release-notes-for-azure-data-studio"></a>Notas de la versión para Azure Data Studio

**[Descargue e instale la versión más reciente.](download.md)**

## <a name="march-2019"></a>Marzo de 2019

18 de marzo de 2019 &nbsp;  /  &nbsp; versión: 1.5.1

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Agregar [extensión PostgreSQL para Azure Data Studio](postgres-extension.md) | Características admitidas: <br/>&bull; &nbsp; Cuadro de diálogo de conexión <br/>&bull; &nbsp; Explorador de objetos <br/>&bull; &nbsp; Editor de consultas <br/>&bull; &nbsp; Creación de gráficos <br/>&bull; &nbsp; Paneles <br/>&bull; &nbsp; Fragmentos de código <br/>&bull; &nbsp; Editar datos <br/>&bull; &nbsp; Blocs de notas |
| Se ha agregado SQL blocs de notas | Se agregó compatibilidad de Kernel de SQL al Visor de cuaderno integrada: <br/>&bull; &nbsp; Es compatible con Transact-SQL <br/>&bull; &nbsp; Compatibilidad con PGSQL |
| Extensión de PowerShell agregada  | Lleva a través de la [extensión PowerShell](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell) experiencia desde VS Code.  |
| Extensión agregada de dacpac de SQL Server  | Quita al Asistente para aplicaciones de capa de datos de extensión de importación de SQL Server en una nueva extensión.  |
| Extensión de la Comunidad se ha agregado QueryPlan.show | Agrega compatibilidad con la integración para visualizar los planes de consulta  |
| Extensión de SQL Server de 2019 Preview actualizada | &bull; &nbsp; Compatibilidad con Jupyter Notebook, específicamente kernels Python3 y Spark, se han movido a la herramienta de Azure Data Studio core. <br/>&bull; &nbsp; Correcciones de errores para el Asistente de datos externos  |
| Resolver errores y problemas. | Consulte [errores y problemas en GitHub](https://github.com/Microsoft/azuredatastudio/milestone/25?closed=1). |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>Problemas conocidos
- [#4427](https://github.com/Microsoft/azuredatastudio/issues/4427): Al hacer clic en ejecutar en la celda antes de Kernel está listo para Spark produce Error irrecuperable **solución alternativa:** Espere hasta que los kernels se cargan hasta que se ejecuta ninguna de las celdas
- [#4493](https://github.com/Microsoft/azuredatastudio/issues/4493): ANUNCIOS iniciadas desde SSMS con autenticación de SQL: contraseña solicita al usuario **solución alternativa:** Uso de la autenticación de Windows por ahora. 
- [#4494](https://github.com/Microsoft/azuredatastudio/issues/4494): No se puede instalar la característica de Bloc de notas SQL <br/>
**Solución alternativa:** Siga los pasos de solución [aquí](https://github.com/Microsoft/azuredatastudio/issues/4494#issuecomment-473043832). 
- [#4503](https://github.com/Microsoft/azuredatastudio/issues/4503): Azure Data Studio no puede estar abierto directamente desde la carpeta de descarga (Mac) <br />
**Solución alternativa:** Reinicie el equipo después de la descompresión de la aplicación. Investigar. 
- [#4539](https://github.com/Microsoft/azuredatastudio/issues/4539):  Guardar como Bloc de notas pierde el contexto de conexión <br />
**Solución alternativa:** Se corregirá en la siguiente versión. 
- [#4458](https://github.com/Microsoft/azuredatastudio/issues/4458): Extraer dacpac se bloquea SqlToolsService si se usa la versión no válida <br/>
**Solución alternativa:** Reinicie Azure Data Studio y asegúrese de que se usa la versión correcta.
- Nuevos iconos de Bloc de notas y Abrir Bloc de notas se pierden <br/> 
**Solución alternativa:** El tipo de conexión heredada está en desuso. Se recomienda conectar al punto de conexión de SQL Server y obtendrá todas las acciones (nuevo bloc de notas, trabajo de Spark) según lo previsto. 

## <a name="february-2019"></a>Febrero de 2019

13 de febrero de 2019 &nbsp;  /  &nbsp; versión: 1.4.5

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Agregar **módulo de administración de SQL Server** paquete de extensión. | Esto facilita instalar Extensiones relacionadas con la administración de SQL Server. Esto incluye:<br/>&bull; &nbsp; [Agente SQL Server](sql-server-agent-extension.md?view=sql-server-2017)<br/>&bull; &nbsp; [SQL Server Profiler](https://docs.microsoft.com/sql/azure-data-studio/sql-server-profiler-extension.md?view=sql-server-2017)<br/>&bull; &nbsp; [Importación de SQL Server](sql-server-import-extension.md?view=sql-server-2017) |
| Se ha agregado el filtrado extendido de soporte técnico de evento en la extensión de Profiler. | &nbsp; |
| Guardar agregado como característica XML que se puede guardar los resultados de T-SQL como XML. | &nbsp; |
| Se ha agregado mejoras en el Asistente para aplicaciones de capa de datos. | &bull; &nbsp; Se ha agregado botón Generar script<br/>&bull; &nbsp; Vista agregada para proporcionar a las advertencias de posible pérdida de datos durante la implementación. |
| Actualizaciones a la extensión de la versión preliminar de SQL Server de 2019. | Consulte [extensión de versión preliminar de SQL Server de 2019](sql-server-2019-extension.md?view=sql-server-ver15). |
| Resultados de streaming habilitada de forma predeterminada durante mucho tiempo ejecución de consultas. | &nbsp; |
| Resolver errores y problemas. | Consulte [errores y problemas en GitHub](https://github.com/Microsoft/azuredatastudio/milestone/23?closed=1). |
| &nbsp; | &nbsp; |

## <a name="january-2019-hotfix"></a>Enero de 2019 (revisión)

16 de enero de 2019 &nbsp;  /  &nbsp; versión: 1.3.9 &nbsp;  /  &nbsp; versión de revisión

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Se ha corregido algunos problemas detectados en 1.3.8. | Consulte [versión de revisión de enero, en GitHub](https://github.com/Microsoft/azuredatastudio/milestone/24?closed=1).<br/><br/>Para obtener información detallada, consulte:<br/>&bull; &nbsp; [Registro de cambios, en GitHub](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md).<br/>&bull; &nbsp; [Versiones en GitHub](https://github.com/Microsoft/azuredatastudio/releases). |
| &nbsp; | &nbsp; |

## <a name="january-2019"></a>Enero de 2019

09 de enero de 2019 &nbsp;  /  &nbsp; versión: 1.3.8

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Agrega a un nuevo instalador de usuario de Windows. | A diferencia del instalador de sistema existente, el nuevo instalador de usuario no requiere privilegios de administrador. Esto también permite una experiencia de actualización más fácil para que no sean administradores. |
| Se agregó compatibilidad de autenticación de Azure Active Directory. | &nbsp; |
| Presentación de información de rendimiento de DM Idera SQL (versión preliminar). | &nbsp; |
| Compatibilidad del Asistente para aplicaciones de capa de datos en la extensión de importación de SQL Server. | &nbsp; |
| Actualizar a la extensión de la versión preliminar de SQL Server de 2019. | Consulte [extensión de versión preliminar de SQL Server de 2019](sql-server-2019-extension.md?view=sql-server-ver15). |
| Mejoras de SQL Server Profiler. | &nbsp; |
| Resultados de la transmisión por secuencias para las consultas grandes (versión preliminar). | &nbsp; |
| Extensiones de la Comunidad: sp_executesql to sql y la nueva base de datos. | &nbsp; |
| Resolver errores y problemas. | Consulte [errores y problemas en GitHub](https://github.com/Microsoft/azuredatastudio/milestone/19?closed=1). |
| &nbsp; | &nbsp; |

## <a name="november-2018"></a>Noviembre de 2018

6 de noviembre de 2018 &nbsp;  /  &nbsp; versión: 1.2.4

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Actualizar a la extensión de la versión preliminar de SQL Server de 2019. | Consulte [extensión de versión preliminar de SQL Server de 2019](sql-server-2019-extension.md?view=sql-server-ver15). |
| Pegar la extensión del Plan de presentación. | &nbsp; |
| Presentación de extensión de las consultas de color de alta densidad, incluido el tema del editor de SSMS. | &nbsp; |
| Correcciones en las extensiones de importación, Profiler y Agente SQL Server. | &nbsp; |
| .Net Core de corregir la causa del problema de Socket KeepAlive quita conexiones inactivas en macOS. | &nbsp; |
| Servicio de las herramientas de actualización de SQL a.Net Core 2,2 Preview 3 (para la compatibilidad con AAD eventual). | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-november-2018"></a>Correcciones de errores, noviembre de 2018

- Corregir [emitir #2933](https://github.com/Microsoft/azuredatastudio/issues/2933): Conexión perdida a Azure SQL DB
- Corregir [emitir 2914 #](https://github.com/Microsoft/azuredatastudio/issues/2914): Nodo de base de datos de "Argumento no válido" excepción expansión OE
- Corregir [emitir #2935](https://github.com/Microsoft/azuredatastudio/pull/2935): Los mensajes de varias líneas se muestran correctamente en los resultados de consulta
- Corregir [emitir 2906 #](https://github.com/Microsoft/azuredatastudio/pull/2906): Corrija el nombre del documento editar datos al nombre de la tabla contiene caracteres especiales
- Corregir [emitir #2929](https://github.com/Microsoft/azuredatastudio/issues/2929): Integrado en la extensión de registro de cambios indica comprobar las notas de VSCode de cambios
- Corregir [emitir #2719](https://github.com/Microsoft/azuredatastudio/issues/2719): El tema de contraste alto dobles/triples iconos
- Corregir [emitir #3047](https://github.com/Microsoft/azuredatastudio/pull/3047): Agregar una interfaz de línea de comandos para conectarse a un servidor SQL Server
- Corregir [emitir #3031](https://github.com/Microsoft/azuredatastudio/pull/3031): Agregar compatibilidad de tema del plan de consulta

## <a name="october-2018"></a>Octubre de 2018

29 de octubre de 2018 &nbsp;  /  &nbsp; versión: 1.1.4

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Introducción a Azure Resource Explorer para examinar las bases de datos SQL de Azure. | &nbsp; |
| Mejorar la solidez de conectividad del explorador de objetos y el Editor de consultas. | &nbsp; |
| Mejoras de las extensiones de agente SQL. | &nbsp; |
| Actualizar a la extensión de la versión preliminar de SQL Server de 2019. | Consulte [extensión de versión preliminar de SQL Server de 2019](sql-server-2019-extension.md?view=sql-server-ver15). |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-october-2018"></a>Correcciones de errores, octubre de 2018

- Corregir [emitir 2717 #](https://github.com/Microsoft/azuredatastudio/issues/2717): Resultado de la columna XML, haga clic en formato
- Corregir [emitir #2993](https://github.com/Microsoft/azuredatastudio/issues/2993): Windows de resultado del ancho es incompleta
- Corregir [emitir 2999 #](https://github.com/Microsoft/azuredatastudio/issues/2999): No se pudo cargar el archivo System.Diagnostics.Tracing en Mac al conectarse a la base de datos
- Corregir [emitir 2851 #](https://github.com/Microsoft/azuredatastudio/issues/2851): Gráfico de serie temporal no se representará correctamente
- Corregir [emitir 2996 #](https://github.com/Microsoft/azuredatastudio/issues/2996): Pérdida de la tabla temporal debido a cambios repentinos de sesión

Para obtener información detallada, consulte el [registro de cambios](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), y [versiones](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="september-2018-ga-release"></a>(Versión de GA) de septiembre de 2018

24 de septiembre de 2018 &nbsp;  /  &nbsp; versión: 1.0 &nbsp;  /  &nbsp; versión GA

Versión de disponibilidad general de Azure Data Studio (anteriormente SQL Operations Studio).

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Rendimiento de la cuadrícula de resultados y las mejoras de la experiencia de usuario de gran número de conjuntos de resultados de consulta. | &nbsp; |
| Actualizar código fuente de Visual Studio Code desde 1,23 a 1.26.1 con el diseño de cuadrícula y ha mejorado el Editor de configuración (versión preliminar). | &nbsp; |
| Mejoras de accesibilidad para el lector de pantalla, navegación mediante el teclado y alto contraste. | &nbsp; |
| Agregar `Connection name` opción para proporcionar un nombre alternativo en la vista de servidores-let. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="announcing-the-sql-server-2019-preview-extension"></a>Anuncio de la extensión de la versión preliminar de SQL Server de 2019

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Admite las características de vista previa de SQL Server 2019, incluidas [clúster de macrodatos](../big-data-cluster/big-data-cluster-overview.md) admite. | Conectarse a la puerta de enlace de Spark o HDFS se incluye con la versión preliminar de SQL Server 2019.<br/><br/>Examinar HDFS, cargar archivos, guardar archivos e iniciar acciones útiles como analizar en el Bloc de notas para los archivos CSV.<br/><br/>Envío de trabajos de Spark desde el panel o haga doble clic en una conexión de Spark o HDFS en el Explorador de objetos. |
| Datos de Azure Studio blocs de notas. | Crear o Abrir Bloc de notas con un visor integrado del Bloc de notas. En esta versión, el Bloc de notas Visor admite la conexión a locales kernels y solo el clúster de macrodatos de SQL Server 2019.<br/><br/>Usar las bibliotecas de Acelerador de código de PROSE en el Bloc de notas para obtener información sobre los tipos de datos y formato de archivo para la preparación de datos rápida. |
| Explorador de recursos de Azure. | La vista del explorador de recursos de Azure le permite examinar los puntos de conexión relacionados con los datos para las cuentas de Azure y crear conexiones en ellos en el Explorador de objetos. En esta versión se admiten servidores y bases de datos de SQL Azure. |
| SQL Server PolyBase crear Asistente para la tabla externa. | Crear una tabla externa y sus estructuras de metadatos compatibles con un asistente fácil de usar. En esta versión, se admiten servidores remotos de SQL Server y Oracle. |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-september-2018"></a>Correcciones de errores, septiembre de 2018

- Corregir [emitir #2647](https://github.com/Microsoft/azuredatastudio/issues/143): Los gráficos dio un gran paso hacia atrás.
- Corregir [emitir #2648](https://github.com/Microsoft/azuredatastudio/issues/143): SELECT que devuelve toda la columna de los hipervínculos JSON.

Para obtener información detallada, consulte el [registro de cambios](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md), y [versiones](https://github.com/Microsoft/azuredatastudio/releases).

## <a name="august-2018"></a>Agosto de 2018

30 de agosto de 2018 &nbsp;  /  &nbsp; versión: 0.32.8 &nbsp;  /  &nbsp; versión preliminar pública

El *versión preliminar pública de agosto* se centra en correcciones de errores, la estabilización de producto y rellenando los huecos en los escenarios existentes.

_0.32.8 contiene correcciones para un par regresiones se encuentra en 0.32.7 ([#1971](https://github.com/Microsoft/azuredatastudio/issues/1971), [2372 #](https://github.com/Microsoft/azuredatastudio/issues/2372))_

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Anuncio de la extensión de importación SQL Server. | &nbsp; |
| Administración de la sesión de SQL Server Profiler. | &nbsp; |
| Compatibilidad con plantillas de sesión de SQL Server Profiler. | &nbsp; |
| Mejoras en el Agente SQL Server. | &nbsp; |
| Nueva extensión de la Comunidad: Kit de primer servicio de respuesta. | &nbsp; |
| Mejoras de calidad de vida: Cadenas de conexión | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-august-2018"></a>Correcciones de errores, agosto de 2018

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

### <a name="known-issues-august-2018"></a>Problemas conocidos, agosto de 2018

- [Problema #2371](https://github.com/Microsoft/azuredatastudio/issues/2371) Guardar como sólo guarda primera fila de datos de Excel
- [Problema #2150](https://github.com/Microsoft/azuredatastudio/issues/2150): No se puede conectar en Ubuntu 16.04 para SQL en un contenedor

## <a name="july-2018"></a>Julio de 2018

19 de julio de 2018 &nbsp;  /  &nbsp; versión: 0.31.4 &nbsp;  /  &nbsp; versión preliminar pública

El *versión preliminar pública de julio* se centra en los siguientes elementos:

- La versión inicial de los escenarios de configuración del Agente SQL Server.
- Mejoras de plantilla de sesión y la vista de SQL Server Profiler.
- Continuas correcciones de errores para el cliente notifica problemas de GitHub.

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| [Agente SQL Server para la extensión de SQL Operations Studio](sql-server-agent-extension.md) mejoras. | Se ha agregado la vista de alertas, operadores y los servidores proxy y los iconos en el panel izquierdo.<br/><br/>Cuadros de diálogo se ha agregado de nuevo trabajo, nuevo paso de trabajo, nueva alerta y New (operador).<br/><br/>Se ha agregado Eliminar trabajo, eliminar alertas y operador Delete (ratón).<br/><br/>Visualización de ejecuciones anteriores se ha agregado.<br/><br/>Filtros agregados para cada nombre de columna. |
| [SQL Server Profiler para la extensión de SQL Operations Studio](sql-server-profiler-extension.md) mejoras. | Se ha agregado 5 plantillas predeterminadas para ver los eventos extendidos.<br/><br/>Nombre de conexión de servidor y base de datos se ha agregado.<br/><br/>Se agregó compatibilidad para las instancias de Azure SQL Database.<br/><br/>Sugerencia agregada para salir a Profiler cuando se cierra la pestaña cuando Profiler aún se está ejecutando. |
| Versión de extensión de Scripts de combinación. | &nbsp; |
| Puntos de extensibilidad de cuadro de diálogo y Asistente para agregados para los autores de extensiones. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-july-2018"></a>Correcciones de errores, julio de 2018

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

## <a name="june-2018"></a>Junio de 2018

20 de junio de 2018 &nbsp;  /  &nbsp; versión: 0.30.6 &nbsp;  /  &nbsp; versión preliminar pública

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| **SQL Server Profiler para SQL Operations Studio _Preview_**  versión inicial de extensión. | &nbsp; |
| El nuevo **SQL Data Warehouse** extensión incluye widgets de panel personalizable completo muestra información para el almacenamiento de datos. | Esto desbloquea escenarios clave en torno a la administración y ajuste el almacenamiento de datos para asegurarse de que está optimizado para rendimiento coherente. |
| **Editar datos "Filtrado y ordenación"** admite. | &nbsp; |
| **Agente SQL Server de SQL Operations Studio _Preview_**  mejoras de extensión para los trabajos y el historial de trabajos vistas. | &nbsp; |
| Mejorado **Asistente & marco de generador de IU de cuadro de diálogo** API de extensibilidad. | &nbsp; |
| Actualizar código de fuente de la plataforma de código de VS. | Integra las versiones siguientes:<br/>&bull; &nbsp; [Marzo de 2018 (1.22)](https://code.visualstudio.com/updates/v1_22)<br/>&bull; &nbsp; [Abril de 2018 (1,23)](https://code.visualstudio.com/updates/v1_23) |
| &nbsp; | &nbsp; |

### <a name="github-issues-fixes-june-2018"></a>Corrige los problemas de GitHub, junio de 2018

- Solicitud de característica ([emitir 1204](https://github.com/Microsoft/azuredatastudio/issues/1204)): Asegúrese de ancho de columna ajusta automáticamente la cuadrícula los resultados a los datos y recuerde los cambios manuales si la misma consulta se vuelve a ejecutar.
- Corregir [emitir 1398](https://github.com/Microsoft/azuredatastudio/issues/1398): Debe mostrar Agregar mensaje y botón Agregar cuenta cuenta cuando la cuenta vinculada está vacía.
- Corregir [emitir 1399](https://github.com/Microsoft/azuredatastudio/issues/1399): Ficha cuenta vinculada se interrumpe cuando se contrae la vista.
- Corregir [emitir 1374](https://github.com/Microsoft/azuredatastudio/issues/1374): Herramientas de servicio de SQL se bloquea al abrir el archivo .sql desde el disco.
- Corregir [emitir 1372](https://github.com/Microsoft/azuredatastudio/issues/1372): Falta la palabra clave SQL "BETWEEN".
- Corregir [emitir 1395](https://github.com/Microsoft/azuredatastudio/issues/1395): Palabra clave 'MATCH' bloquea el servicio de herramientas de SQL.
- Corregir [emitir 1496](https://github.com/Microsoft/azuredatastudio/issues/1496): "Nuevo Profiler" opción de menú contextual en el Explorador de objetos no hace nada.
- Corregir [emitir 1495](https://github.com/Microsoft/azuredatastudio/issues/1495): Plan de consulta de "Explicación" editor de consultas se interrumpe.

## <a name="may-2018"></a>Mayo de 2018

7 de mayo de 2018 &nbsp;  /  &nbsp; versión: 0.29.3 &nbsp;  /  &nbsp; versión preliminar pública

El *versión preliminar pública puede* se centra en la estabilización y correcciones de errores.

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Anuncio de extensión de búsqueda de SQL disponible en el Administrador de extensiones. | &nbsp; |
| Localización de comunidad disponible en 10 idiomas. | Alemán, español, francés, italiano, japonés, coreano, portugués, ruso, chino simplificado y chino tradicional. |
| Cambios de la colección de telemetría. | &bull; &nbsp; Colección de telemetría reducida.<br/>&bull; &nbsp; Experiencia mejorada de participar.<br/>&bull; &nbsp; Vínculos en el producto a la declaración de privacidad. |
| Administrador de extensiones tiene Marketplace mejorada experiencia. | Detectar más fácilmente las extensiones de la Comunidad. |
| Extensión del Agente SQL. | &bull; &nbsp; Trabajos.<br/>&bull; &nbsp; Mejora de la vista de historial de trabajos. |
| Actualizaciones de whoisactive y extensiones de los informes de servidor. | &nbsp; |
| Mejora el desplazamiento de administrar las propiedades de panel. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues"></a>Solucionar problemas de GitHub

- Corregir [emitir 703](https://github.com/Microsoft/azuredatastudio/issues/703): Escritura de texto de estilo HTML en datos de edición hace que el valor no se muestran correctamente hasta que la actualización
- Corregir [emitir 821](https://github.com/Microsoft/azuredatastudio/issues/821): azuredatastudio.deb dependencia del paquete
- Corregir [emitir 1260](https://github.com/Microsoft/azuredatastudio/issues/1260): Palabra clave 'distinct' no resaltado
- Corregir [emitir 1332](https://github.com/Microsoft/azuredatastudio/issues/1332): Editar datos revertir fila no funciona
- Corregir [emitir 1215](https://github.com/Microsoft/azuredatastudio/issues/1215): Extensión del Agente SQL y la barra de estado
- Corregir [emitir 1316](https://github.com/Microsoft/azuredatastudio/issues/1316): Cambio de tamaño no de agente SQL después de cambiar el tamaño de windows

## <a name="april-2018"></a>Abril de 2018

25 de abril de 2018 &nbsp;  /  &nbsp; versión: 0.28.6 &nbsp;  /  &nbsp; versión preliminar pública

El *versión preliminar pública de abril* contiene correcciones de errores y mejoras.

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Mejoras en la extensión de la versión preliminar del agente de SQL: | &nbsp; |
| &nbsp; &nbsp; &nbsp; Compatibilidad mejorada para los archivos. | &bull; &nbsp; Archivos de gran tamaño.<br/>&bull; &nbsp; Los archivos protegidos, para guardar administrador protegido.<br/>&bull; &nbsp; Almacenar \>256 millones de archivos dentro de SQL Operations Studio. |
| &nbsp; &nbsp; &nbsp; Terminal integrado de división. | Trabajar con varios terminales abiertos simultáneamente. |
| &nbsp; &nbsp; &nbsp; Instalaciones más rápidas y tiempos de inicio. | Instalación reducido de archivos en disco recuento foot impresión. |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues-april-2018"></a>Solucionar problemas de GitHub, abril de 2018

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

### <a name="visual-studio-code-121-platform"></a>Plataforma de Visual Studio 1.21 de código

Un resaltado para la versión preliminar pública de abril es la actualización del código fuente para la plataforma 1.21 de código de Visual Studio. Esto aporta varias actualizaciones para el editor de núcleo y workbench desde el punto de 1.19 sincronización anterior. Algunos ejemplos incluyen lo siguiente:

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| [Interfaz de usuario de nuevas notificaciones](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui). | Administre fácilmente y revisar las notificaciones de SQL Operations Studio. |
| [Integra la división Terminal](https://code.visualstudio.com/updates/v1_21#_split-terminals). | Trabajar con varios terminales abiertos al mismo tiempo. |
| [Guardar los archivos protegidos y grandes](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges). | Guardar administrador protegido y \>256 millones de archivos dentro de SQL Operations Studio. |
| [Ha mejorado la compatibilidad con archivos grandes](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements). | Optimizaciones de búfer de texto para archivos de gran tamaño. |
| [Búsqueda mejorada de configuración](https://code.visualstudio.com/updates/v1_20#_settings-search). | Encuentre fácilmente la configuración correcta con búsqueda en lenguaje natural. |
| [Fragmentos de código globales](https://code.visualstudio.com/updates/v1_20#_global-snippets). | Crear fragmentos de código que se puede usar en todos los tipos de archivo. |
| [Selección múltiple de explorador](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer). | Realizar acciones en varios archivos a la vez. |
| [Errores y advertencias en el Explorador de](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer). | Navegue rápidamente a los errores en la base de código. |
| [Arrastrar y colocar, copiar y pegar a través de windows](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support). | Mover archivos entre ventanas abiertas de SQL Operations Studio. |
| [Soporte técnico de submódulo de GIT](https://code.visualstudio.com/updates/v1_20#_git-submodules). | Realizar operaciones de Git en repositorios Git anidados. |
| [Compatibilidad con lectores de pantalla de Terminal](https://code.visualstudio.com/updates/v1_20#_screen-reader-support). | Ahora tiene el Terminal integrado **optimizado de lector de pantalla** modo. |
| [Diseño del editor centrado](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout). | Maximice el código de espacio en pantalla de visualización. |
| [Resultados de búsqueda horizontal (versión preliminar)](https://code.visualstudio.com/updates/v1_21#_horizontal-search). | Ahora puede ver resultados de búsqueda en un panel horizontal. |
| &nbsp; | &nbsp; |

Para obtener más detalles, desproteger el [notas de versión de febrero de código de Visual Studio](https://code.visualstudio.com/updates/v1_21)y el [notas de versión de enero de código de Visual Studio](https://code.visualstudio.com/updates/v1_20).

Para obtener más información, consulte el [registro de cambios](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md).

## <a name="march-2018"></a>Marzo de 2018

28 de marzo de 2018 &nbsp;  /  &nbsp; versión: 0.27.3 &nbsp;  /  &nbsp; versión preliminar pública

El *versión preliminar pública de marzo* continúa abordar los principales problemas de GitHub y se centra en mejorar nuestra historia de extensibilidad. Activar específicamente el Administrador de extensiones, mejorar la administración del panel y proporcione el Agente SQL y las extensiones de insights. Esta versión incluye las siguientes mejoras:

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Mejorar el modelo de extensibilidad de panel para admitir información con pestañas y paneles de configuración. | Administrador de extensiones permite simple adquisición de extensiones.<br/><br/>Las extensiones del panel para sp\_whoisactive desde [whoisactive.com](http://www.whoisactive.com).<br/><br/>Para obtener más información, consulte [amplían la funcionalidad de SQL Operations Studio](extensions.md). |
| Agregar más [API de extensibilidad para la conexión y el objeto explorer](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API) administración. | &nbsp; |
| Seguir corrigiendo clientes importantes que afectan a [problemas de GitHub](https://github.com/Microsoft/azuredatastudio/issues). | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="february-2018"></a>Febrero de 2018

15 de febrero de 2018 &nbsp;  /  &nbsp; versión: 0.26.7 &nbsp;  /  &nbsp; versión preliminar pública

El *versión preliminar pública de febrero* incluye algunas sugerencias de características y correcciones de errores de alta prioridad. Esta versión incluye las siguientes mejoras:

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Introducción a la instalación de actualización automática, que proporciona una notificación cuando esté disponible para descargar una nueva versión. | &nbsp; |
| El cuadro de diálogo de conexión **base de datos** campo ahora es una lista desplegable rellena dinámicamente que contendrá una lista de bases de datos que se rellena desde el servidor especificado. | &nbsp; |
| Introducir la API de extensibilidad de conexión. | &nbsp; |
| Integración de VS 1.19 del Editor de código. | &nbsp; |
| Actualizar componente JustinPealing/html--plan de consulta para la recogida varias mejoras del Visor de Plan de consulta. | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixed-issues-february-2018"></a>Problemas corregidos, febrero de 2018

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

## <a name="january-2018"></a>Enero de 2018

17 de enero de 2018 &nbsp;  /  &nbsp; versión: 0.25.4 &nbsp;  /  &nbsp; versión preliminar pública

El *versión preliminar pública de enero* incluye algunas sugerencias de características y correcciones de errores de alta prioridad. Esta versión incluye las siguientes mejoras:

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Guardado de las conexiones de servidor están disponibles en el cuadro de diálogo de conexión. | &nbsp; |
| Habilitar salida activo. Salida activo está desactivada de forma predeterminada, al habilitar vea [configuración activa exit](settings.md#hot-exit). | &nbsp; |
| Según el grupo de servidores de colores de pestaña. Color de ficha está desactivada de forma predeterminada, al habilitar vea [pestaña Configuración de color](settings.md#tab-color). | &nbsp; |
| Cambio *nombre del servidor* a *Server* en el cuadro de diálogo de conexión. | &nbsp; |
| Corrección dividida *ejecutar la consulta actual* comando. | &nbsp; |
| Corregir errores de secuencias de comandos de separación de arrastrar y colocar. | &nbsp; |
| Corregir incorrectos de los iconos anclados menú Inicio. | &nbsp; |
| Falta la cuenta de Azure icono de personalización de marca de corregir. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="december-2017"></a>Diciembre de 2017

19 de diciembre de 2017 &nbsp;  /  &nbsp; versión: 0.24.1 &nbsp;  /  &nbsp; versión preliminar pública

El *versión preliminar pública de diciembre* incluye varias correcciones de errores en todas las áreas de características, así como las siguientes mejoras:

&nbsp;

| Cambiar | Detalles |
| :----- | :------ |
| Crear cuadro de diálogo de regla de Firewall ahora está disponible para ayudar a conectar a Azure SQL Database y Azure SQL Data Warehouse. | &nbsp; |
| Se ha agregado el programa de instalación de Windows y Linux DEB y RPM paquetes de instalación. | &nbsp; |
| Administrar el editor de diseño visual del panel. | &nbsp; |
| *Secuencia de comandos como Alter* y *como la ejecución del Script* comandos. | &nbsp; |
| *Ejecutar la consulta actual con el Plan real* comando. | &nbsp; |
| Integración de plataforma del editor de VS Code 1.18.1. | &nbsp; |
| Habilitar los archivos de instalación de prueba de la extensión VSIX. | &nbsp; |
| Admite la sintaxis de iteración de "N GO" por lotes. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="november-2017"></a>Noviembre de 2017

15 de noviembre de 2017 &nbsp;  /  &nbsp; versión: 0.23.6

- Versión inicial del [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="next-steps"></a>Pasos siguientes

Consulte uno de los siguientes tutoriales para empezar a trabajar:

- [Conectar y consultar SQL Server](quickstart-sql-server.md)
- [Conectar y consultar la base de datos SQL Azure](quickstart-sql-database.md)
- [Conectar y consultar el almacén de datos de Azure](quickstart-sql-dw.md)

Contribuir a [!INCLUDE[name-sos](../includes/name-sos-short.md)]:

- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
