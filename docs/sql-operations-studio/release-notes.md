---
title: Notas de la versión de SQL Operations Studio (versión preliminar) | Documentos de Microsoft
description: Notas de la versión de SQL Operations Studio (versión preliminar)
ms.custom: tools|sos
ms.date: 07/19/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d5c331fc8b9e95940e0aaca29efbada78083340f
ms.sourcegitcommit: d80aaa52562d828f9bfb932662ad779432301860
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/20/2018
ms.locfileid: "39188961"
---
# <a name="sql-operations-studio-preview-release-notes"></a>Notas de la versión de SQL Operations Studio (versión preliminar)

**[Descargue la versión preliminar pública de julio](download.md)**

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
 - Corregir [emitir 728](https://github.com/Microsoft/sqlopsstudio/issues/728): ninguna respuesta al agregar conexión en macOS
 - Corregir [emitir 1612](https://github.com/Microsoft/sqlopsstudio/issues/1612): presentación del texto de cuadrícula de resultados está equivocada por caracteres internacionales
 - Corregir [emitir 1693](https://github.com/Microsoft/sqlopsstudio/issues/1693): cuadro de diálogo de copia de seguridad: se ha interrumpido la interfaz de usuario del explorador de archivos
 - Corregir [emitir 1713](https://github.com/Microsoft/sqlopsstudio/issues/1713): número de filas afectadas
 - Corregir [emitir 1718](https://github.com/Microsoft/sqlopsstudio/issues/1718): no se puede conectar a cualquier origen de datos
 - Corregir [emitir 1719](https://github.com/Microsoft/sqlopsstudio/issues/1719): TypeError al conectarse al servidor
 - Corregir [emitir 1724](https://github.com/Microsoft/sqlopsstudio/issues/1724): los cuadros de diálogo extensión han dejado de funcionar
 - Corregir [emitir 1749](https://github.com/Microsoft/sqlopsstudio/issues/1749): error: se interpretan los datos HTML en una columna
 - Corregir [emitir 1789](https://github.com/Microsoft/sqlopsstudio/issues/1789): extensibilidad: si agrega un proveedor de conexión desinstalar nunca quitará de la lista
 - Corregir [emitir 1791](https://github.com/Microsoft/sqlopsstudio/issues/1791): extensiones Sqlops: queryeditor.connect() se conecta a la base de datos de destino, pero no muestra la interfaz de usuario está conectado el editor
 - Corregir [emitir 1799](https://github.com/Microsoft/sqlopsstudio/issues/1799): gráfico de tamaño de base de datos de Top 10 no funciona en las instancias distingue mayúsculas de minúsculas
 - Corregir [emitir 1814](https://github.com/Microsoft/sqlopsstudio/issues/1814): definición de tipo de error de escritura sqlops.d.ts causando implícito 'any'
 - Corregir [emitir 1817](https://github.com/Microsoft/sqlopsstudio/issues/1817): Error de Ortografia
 - Corregir [emitir 1830](https://github.com/Microsoft/sqlopsstudio/issues/1830): establecer iconPath en ButtonComponent después de llamar a component() no cambia el icono
 - Corregir [emitir 1843](https://github.com/Microsoft/sqlopsstudio/issues/1843): organización de tablas mejor


Para obtener más información, consulte el [registro de cambios](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md), y [versiones](https://github.com/Microsoft/sqlopsstudio/releases).



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
  - Solicitud de característica ([emitir 1204](https://github.com/Microsoft/sqlopsstudio/issues/1204)): por favor, que los resultados de ancho de la cuadrícula de ajuste automático de columna a los datos o recordar los cambios manuales si se vuelve a ejecutar la misma consulta.
  - Corregir [emitir 1398](https://github.com/Microsoft/sqlopsstudio/issues/1398): debe agregar show del mensaje y el botón Agregar cuenta cuenta cuando la cuenta vinculada está vacía.
  - Corregir [emitir 1399](https://github.com/Microsoft/sqlopsstudio/issues/1399): ficha cuenta vinculada se interrumpe cuando se contrae la vista.
  - Corregir [emitir 1374](https://github.com/Microsoft/sqlopsstudio/issues/1374): servicio de las herramientas de SQL se bloquea al abrir el archivo .sql desde el disco.
  - Corregir [emitir 1372](https://github.com/Microsoft/sqlopsstudio/issues/1372): palabra clave de SQL que faltan "BETWEEN".
  - Corregir [emitir 1395](https://github.com/Microsoft/sqlopsstudio/issues/1395): palabra clave 'MATCH', bloquea el servicio de herramientas de SQL.
  - Corregir [emitir 1496](https://github.com/Microsoft/sqlopsstudio/issues/1496): opción de menú contextual de "Nueva Profiler" en el Explorador de objetos no hace nada.
  - Corregir [emitir 1495](https://github.com/Microsoft/sqlopsstudio/issues/1495): plan de consulta de "Explicación" editor de consultas se interrumpe.


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
   - Corregir [emitir 703](https://github.com/Microsoft/sqlopsstudio/issues/703): escritura de texto de estilo HTML en datos de edición hace que el valor no se muestran correctamente hasta que la actualización
   - Corregir [emitir 821](https://github.com/Microsoft/sqlopsstudio/issues/821): sqlopsstudio.deb dependencia del paquete
   - Corregir [emitir 1260](https://github.com/Microsoft/sqlopsstudio/issues/1260): palabra clave 'distinct' no resaltado
   - Corregir [emitir 1332](https://github.com/Microsoft/sqlopsstudio/issues/1332): reversión edición datos fila no funciona
   - Corregir [emitir 1215](https://github.com/Microsoft/sqlopsstudio/issues/1215): extensión del Agente SQL y la barra de estado
   - Corregir [emitir 1316](https://github.com/Microsoft/sqlopsstudio/issues/1316): cambiar el tamaño no de agente SQL después de cambiar el tamaño de windows




## <a name="april-2018-april-public-preview"></a>Abril de 2018 (abril Public Preview)

fecha de publicación: 25 de abril de 2018  
versión: 0.28.6

El *versión preliminar pública de abril* contiene correcciones de errores y mejoras. 

- Mejoras en la extensión de la versión preliminar del agente de SQL.
- Archivo protegido y gran compatibilidad mejorada para guardar administrador protegido y > 256 millones de archivos dentro de SQL Operations Studio.
- Terminal integrado de división para trabajar con varios terminales abiertos al mismo tiempo.
- Imprimir pies de recuento de archivo en disco de instalación reducido para instalaciones más rápidas y tiempos de inicio.
- Continuar solucionar problemas de GitHub:
   - Corregir [emitir 37](https://github.com/Microsoft/sqlopsstudio/issues/37): cuando el Visor gráfico produce un error, se produce un comportamiento inesperado.
   - Corregir [emitir 462](https://github.com/Microsoft/sqlopsstudio/issues/462): solicitud de característica: opción para grupos de servidores se expanda de forma predeterminada.
   - Corregir [emitir 606](https://github.com/Microsoft/sqlopsstudio/issues/606): intellisense - propuesta no válida para el comando 'update'.
   - Corregir [emitir 967](https://github.com/Microsoft/sqlopsstudio/issues/967): esperar el plan de consulta cuando selecciona el plan de presentación XML en la cuadrícula de resultados.
   - Corregir [emitir 1023](https://github.com/Microsoft/sqlopsstudio/issues/1023): agregar corchetes para llamada ms_foreachdb desde flyfishingdba.
   - Corregir [emitir 1048](https://github.com/Microsoft/sqlopsstudio/issues/1048): error de protocolo de enlace de inicio de sesión previo SSL/TLS.
   - Corregir [emitir 1050](https://github.com/Microsoft/sqlopsstudio/issues/1050): ver información clara antes de mostrar el error.
   - Corregir [emitir 1057](https://github.com/Microsoft/sqlopsstudio/issues/1057): nuevas acciones de consulta en el Explorador de widget y restauración se interrumpen.
   - Corregir [emitir 1068](https://github.com/Microsoft/sqlopsstudio/issues/1068): panel Salida windows pop-up con mensaje de error para la base de datos de SQL Azure.
   - Corregir [emitir 1069](https://github.com/Microsoft/sqlopsstudio/issues/1069): error de servidor necesario cuando se muestra inicialmente se muestra el cuadro de diálogo conexión.
   - Corregir [emitir 1070](https://github.com/Microsoft/sqlopsstudio/issues/1070): grupos de servidores requieren ahora un doble clic para expandir.
   - Corregir [emitir 1072](https://github.com/Microsoft/sqlopsstudio/issues/1072): es parcialmente transparente en segundo plano de control de selección.
   - Corregir [emitir 1115](https://github.com/Microsoft/sqlopsstudio/issues/1115): Corregir contraste alto todos los problemas de accesibilidad en SQL Operations Studio.
   - Corregir [emitir 1101](https://github.com/Microsoft/sqlopsstudio/issues/1101): se produce un error de extensión al vínculo de actualización "descargar manualmente" se dirige a una ubicación incorrecta.
   - Corregir [emitir 1103](https://github.com/Microsoft/sqlopsstudio/issues/1103): desplazamiento V no está trabajando en la ficha Inicio.
   - Corregir [emitir 1104](https://github.com/Microsoft/sqlopsstudio/issues/1104): fichas de la extensión SQL dejó de funcionar.


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

Para obtener más información, consulte el [registro de cambios](https://github.com/Microsoft/sqlopsstudio/blob/master/CHANGELOG.md).

## <a name="march-2018-march-public-preview"></a>Marzo de 2018 (versión preliminar pública de marzo)

fecha de lanzamiento: 28 de marzo de 2018  
versión: 0.27.3

El *versión preliminar pública de marzo* continúa abordar los principales problemas de GitHub y se centra en mejorar nuestra historia de extensibilidad. Activar específicamente el Administrador de extensiones, mejorar la administración del panel y proporcione el Agente SQL y las extensiones de insights. Esta versión incluye las siguientes mejoras:

- Mejorar el modelo de extensibilidad de panel para admitir información con pestañas y paneles de configuración.
   - Administrador de extensiones permite simple adquisición de extensiones.
   - Las extensiones del panel para sp_whoisactive desde [whoisactive.com](http://www.whoisactive.com).
   - Para obtener más información, consulte [amplían la funcionalidad de SQL Operations Studio](extensions.md).
- Agregar más [API de extensibilidad para la conexión y el objeto explorer](https://github.com/Microsoft/sqlopsstudio/wiki/Extensibility-API) administración.
- Seguir corrigiendo clientes importantes que afectan a [problemas de GitHub](https://github.com/Microsoft/sqlopsstudio/issues).


## <a name="february-2018-february-public-preview"></a>Febrero de 2018 (versión preliminar pública de febrero)

fecha de lanzamiento: 15 de febrero de 2018  
versión: 0.26.7

El *versión preliminar pública de febrero* incluye algunas sugerencias de características y correcciones de errores de alta prioridad. Esta versión incluye las siguientes mejoras:

- Introducción a la instalación de actualización automática, que proporciona una notificación cuando esté disponible para descargar una nueva versión 
- El campo de cuadro de diálogo de conexión 'Database' es ahora una lista desplegable rellena dinámicamente que contendrá una lista de bases de datos que se rellena desde el servidor especificado.
- Corregir [emitir 6](https://github.com/Microsoft/sqlopsstudio/issues/6): mantener la conexión y la base de datos seleccionada al abrir nuevas pestañas de consulta.
- ¿Corregir [emitir 22](https://github.com/Microsoft/sqlopsstudio/issues/22): 'Server Name' y 'Nombre de base de datos -' estos pueden ser listas desplegables en lugar de los cuadros de texto?
- Corregir [emitir 549](https://github.com/Microsoft/sqlopsstudio/issues/549): instalación silenciosa de muy/Silent da como resultado de apertura después de la instalación de aplicación.
- Corregir [emitir 481](https://github.com/Microsoft/sqlopsstudio/issues/481): agregar la opción "Buscar actualizaciones".
- Editor SQL coloración y correcciones de finalización automática:
   - Corregir [emitir 584](https://github.com/Microsoft/sqlopsstudio/issues/584): palabra clave "FULL" no resaltado por IntelliSense.
   - Corregir [emitir 345](https://github.com/Microsoft/sqlopsstudio/issues/345): funciones SQL colorear dentro del editor.
   - Corregir [emitir 300](https://github.com/Microsoft/sqlopsstudio/issues/300): [#tempData] más reciente "]" se mostrará de color verde.
   - Corregir [emitir 225](https://github.com/Microsoft/sqlopsstudio/issues/225): error de coincidencia de color de palabra clave.
   - Corregir [emitir 60](https://github.com/Microsoft/sqlopsstudio/issues/60): sql no válido color resaltado de sintaxis cuando se usa una tabla temporal en cláusula from.
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
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio)
