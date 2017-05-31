---
title: 'SQL Server Management Studio: Registro de cambios (SSMS) | Microsoft Docs'
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
caps.latest.revision: 72
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2144751277bb10897e0ed39ee24dbad8a32b4ce
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio - Changelog (SSMS)

## <a name="ssms-1653-release"></a>Versión de SSMS 16.5.3
Disponible con carácter general | Número de compilación: 13.0.16106.4

Se han corregido los problemas siguientes en esta versión:

* Se ha corregido un problema detectado en SSMS 16.5.2 que provocaba la expansión del nodo "Tabla" cuando la tabla tenía más de una columna dispersa.

* Los usuarios pueden implementar paquetes SSIS que contienen el Administrador de conexiones OData que se conectan a un recurso de Microsoft Dynamics AX/CRM Online en el catálogo de SSIS. Para obtener más información, vea [Administrador de conexiones OData](https://msdn.microsoft.com/library/dn584133.aspx).

* La configuración de Always Encrypted en una tabla existente produce errores en los objetos relacionados. [Id. de Connect 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* La Configuración de Always Encrypted para una base de datos existente con varios esquemas no funciona. [Id. de Connect 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* El Asistente para columnas cifradas de Always Encrypted produce un error debido a la base de datos que contiene vistas que hacen referencia a vistas del sistema. [Id. de Connect 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* Cuando se cifra mediante Always Encrypted, los errores al actualizar los módulos después del cifrado se tratan incorrectamente.

* El menú *Abrir recientes* no muestra los archivos guardados recientemente. [Id. de Connect 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* SSMS funciona con lentitud cuando se hace clic con el botón derecho en el índice de una tabla (a través de una conexión remota de Internet). [Id. de Connect 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* Se ha corregido un problema de la barra de desplazamiento del Diseñador de SQL. [Id. de Connect 3114856](http://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* El menú contextual de las tablas se bloquea momentáneamente. 
 
* En algunas ocasiones, SSMS produce excepciones en el Monitor de actividad y se bloquea. [Id. de Connect 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* SSMS 2016 se bloquea con error "El proceso terminó debido a un error interno en el runtime de .NET en la dirección IP 71AF8579 (71AE0000) con el código de salida 80131506".


## <a name="ssms-1651-release"></a>Versión de SSMS 16.5.1
Disponible con carácter general | Número de compilación: 13.0.16100.1

* Se ha corregido un problema por el que Invoke-Sqlcmd insertaba erróneamente varias filas cuando se produce la restricción Check. [Microsoft Connect, n.º 811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

* Se ha corregido un problema en versiones de idiomas diferentes de ESN que no funcionaban completamente al crear Grupos de disponibilidad.

* Se ha corregido un problema por el que al hacer clic en el plan de consulta XML no se abría la IU de SSMS adecuada.


## <a name="ssms-165-release"></a>Versión de SSMS 16.5
Disponible con carácter general | Número de compilación: 13.0.16000.28

* Se ha corregido un problema de bloqueo que se producía al hacer clic en una base de datos con un nombre de tabla que contenía ";:".
* Se ha corregido un problema que ocasionaba que los cambios realizados en la página Modelo en la ventana de propiedades de base de datos tabular de AS creasen scripts fuera de la definición original. 
[Microsoft Connect, elemento n.º 3080744](https://connect.microsoft.com/SQLServer/feedback/details/3080744) 
* Se ha corregido el problema por el que los archivos temporales se agregan a la lista de "Archivos recientes".  
[Microsoft Connect, elemento n.º 2558789](https://connect.microsoft.com/SQLServer/feedback/details/2558789)
* Corregido el problema por el que se deshabilitaba el elemento del menú "Administrar compresión" para los nodos de la tabla de usuario en el árbol del explorador de objetos.  
[Microsoft Connect, elemento n.º 3104616](https://connect.microsoft.com/SQLServer/feedback/details/3104616)

* Se ha corregido el problema por el que el usuario no es capaz de establecer el tamaño de fuente para el explorador de objetos, el explorador del servidor registrado, el explorador de plantillas y los detalles del explorador de objetos. La fuente para los exploradores utilizada será la fuente del entorno.  
[Microsoft Connect, elemento n.º 691432](https://connect.microsoft.com/SQLServer/feedback/details/691432)

* Se ha corregido el problema por el que SSMS se vuelve a conectar siempre a la base de datos predeterminada cuando se pierde la conexión.  
[Microsoft Connect, elemento n.º 3102337](https://connect.microsoft.com/SQLServer/feedback/details/3102337)

* Se han corregido muchos de los problemas de valores de ppp altos en la ventana del editor de consultas y de administración de directivas, incluidos los iconos de los planes de ejecución.

* Se ha corregido el problema por el que faltaba la opción de configuración de color y fuente para eventos extendidos.

* Se ha corregido el problema de bloqueos de SSMS que se producían al cerrar la aplicación o al intentar mostrar el cuadro de diálogo de error.


## <a name="ssms-1641-september-2016-release"></a>SSMS 16.4.1, versión de septiembre de 2016
Disponible con carácter general | Número de compilación: 13.0.15900.1

*  Se ha corregido un problema que producía un error al alterar o modificar un procedimiento almacenado:  
[Microsoft Connect, n.º 3103831](https://connect.microsoft.com/SQLServer/feedback/details/3103831)

* Nuevos cmdlets 'Read-SqlTableData', 'Read-SqlViewData' y 'Write-SqlTableData' para ver y escribir datos mediante PowerShell.  
[Trello Read-SqlTableData Card](https://trello.com/c/FXVUNJ8x/131-read-sqltabledata)  
[Microsoft Connect, nº 2685363](https://connect.microsoft.com/SQLServer/feedback/details/2685363)
    
* Nuevo cmdlet 'Add-SqlLogin' para permitir nuevos escenarios de administración de inicio de sesión mediante PowerShell.  
[Microsoft Connect, nº 2588952](https://connect.microsoft.com/SQLServer/feedback/details/2588952)
    
*  Compatibilidad y usabilidad mejoradas para usuarios que se conectan a varias nubes nacionales.
    
    
*  Se corrigió un problema donde se iniciaban excepciones de memoria agotada.  
[Microsoft Connect, nº 3062914](https://connect.microsoft.com/SQLServer/feedback/details/3062914)  
[Microsoft Connect, nº 3074856](https://connect.microsoft.com/SQLServer/feedback/details/3074856)
    
*  Se corrigió un problema donde el filtrado por esquema no era una opción de filtro válida.  
[Microsoft Connect, nº 3058105](https://connect.microsoft.com/SQLServer/feedback/details/3058105)  
[Microsoft Connect, nº 3101136](https://connect.microsoft.com/SQLServer/feedback/details/3101136)
    
*  Se corrigió un problema donde la ventana Monitor para una base de datos ajustada no estaría accesible.
    
*  Se corrigió un problema donde la Ayuda F1 siempre abría contenido en línea. Los usuarios ahora pueden seleccionar si prefieren ayuda en línea o sin conexión a través de la opción "Establecer preferencias de la Ayuda" en el menú Ayuda.   
[Microsoft Connect, nº 2826366](https://connect.microsoft.com/SQLServer/feedback/details/2826366)
    
*  Se corrigió un problema donde un modelo tabular de Analysis Services de 1200 niveles no generaría scripts de la contraseña para scripting, aunque la versión del servidor tuviera [objeto de modelo de cliente está ahora sincronizado antes de aplicar el script].
    
*  Se corrigió un problema donde opción “SELECT TOP N ROWS” generaba una sintaxis en desuso para el operador TOP.  
[Microsoft Connect, nº 3065435](https://connect.microsoft.com/SQLServer/feedback/details/3065435)
    
*  Se corrigieron varios problemas de diseño a lo largo de SSMS, incluida la página Propiedades de inicio de sesión y las opciones de ejecución de consultas avanzadas.   
[Microsoft Connect, nº 3058199](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect, nº 3079122](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect, nº 3071384](https://connect.microsoft.com/SQLServer/feedback/details/3071384)
    
*  Se corrigió un problema donde una solución se creaba automáticamente cada vez que un usuario abría una nueva ventana de consulta.   
[Microsoft Connect, nº 2924667](https://connect.microsoft.com/SQLServer/feedback/details/2924667)    
[Microsoft Connect, nº 2917742](https://connect.microsoft.com/SQLServer/feedback/details/2917742)   
[Microsoft Connect, nº 2612635](https://connect.microsoft.com/SQLServer/feedback/details/2612635)
    
*  Se corrigió un problema donde las tablas temporales no se podrían expandir en el Explorador de objetos en las bases de datos del sistema.  
[Microsoft Connect, nº 2551649](https://connect.microsoft.com/SQLServer/feedback/details/2551649)
    
*  Se ha corregido un problema por el que SSMS ejecutaba una consulta en SELECT @@trancount después de ejecutar un lote.    
[Microsoft Connect, nº 3042364](https://connect.microsoft.com/SQLServer/feedback/details/3042364)
    
*  Se ha corregido un problema en Analysis Services que producía que, al crear un script desde la página de propiedades de un servidor, se crease un cuadro de diálogo de conexión oculto.
    
*  Se corrigió un problema donde Ctrl+Q no seleccionaría la barra de herramientas Inicio rápido.
    
*  Se corrigió un problema donde el cambio de MaxSize de una base de datos mediante el cuadro de diálogo Propiedades del servidor se rompía para bases de datos > 2 TB.  
[Microsoft Connect, n.º 1231091](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  Se corrigió un problema en el asistente Restaurar base de datos no aceptaría nombres de archivo con espacios en blanco iniciales:   
[Microsoft Connect, n.º 2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="ssms-163-august-2016-release"></a>Versión de SSMS 16.3 (agosto de 2016)
Disponible con carácter general | Número de versión: 13.0.15700.28

* Las versiones mensuales de SSMS ahora se marcan numéricamente.

* [Nueva opción de autenticación **'Autenticación universal de Active Directory'**](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Se trata de un mecanismo de autenticación basado en token impulsado por Azure Active Directory que es compatible con mecanismos de autenticación integrados, contraseñas y multifactor.

* Nuevas plantillas de eventos extendidos que coinciden con la funcionalidad de las plantillas de SQL Server Profiler [(Microsoft Connect, n.º 2543925)](https://connect.microsoft.com/SQLServer/feedback/details/2543925/sql-server-extended-events-profiler-tool). Obtenga más información acerca de las [plantillas de SQL Server Profiler](https://msdn.microsoft.com/library/ms190176.aspx).

* Nuevos cuadros de diálogo Crear base de datos y propiedades de bases de datos para Bases de datos SQL de Azure.

* Nuevos cmdlets 'Get-SqlLogin' y 'Remove-SqlLogin' para ayuda a realizar la administración de inicio de sesión de SQL Server con PowerShell.  
*Solicitudes de error de clientes vinculadas:*   
[Microsoft Connect, n.º 2588952.](https://connect.microsoft.com/SQLServer/feedback/details/2588952/)

* Nuevo cmdelt de PowerShell 'New-SqlColumnMasterKeySettings' que proporciona soporte para la creación de claves maestra de columna para proveedores arbitrarios y rutas de acceso de claves.

* Nuevo cuadro de diálogo 'Crear base de datos' para mejorar la creación de las bases de datos SQL de Azure en SSMS>

* Compatibilidad con el filtrado en el nodo 'Databases' del Explorador de objetos SSMS. Desplácese hasta el nodo 'Databases' en el Explorador de objetos y haga clic en el icono de filtro en la barra de herramientas del Explorador de objetos para filtrar la lista de bases de datos.

* Compatibilidad con cuentas de almacenamiento de tipo Azure-Resource Manager (ARM) en los asistentes de copia de seguridad y restauración.

* [Compatibilidad con la versión beta inicial para pantallas de alta resolución](https://blogs.msdn.microsoft.com/sqlreleaseservices/ssms-highdpi-support/).  
*Solicitudes de error de clientes vinculadas:*   
[Microsoft Connect, n.º 1129301](https://connect.microsoft.com/SQLServer/feedback/details/1129301/management-studio-is-unusable-on-a-4k-display), [Microsoft Connect, n.º 1858763](https://connect.microsoft.com/SQLServer/feedback/details/1858763/), [Microsoft Connect, n.º 1852671](https://connect.microsoft.com/SQLServer/feedback/details/1852671/), [Microsoft Connect, n.º 1487643](https://connect.microsoft.com/SQLServer/feedback/details/1487643/),  [Microsoft Connect, n.º 1355641](https://connect.microsoft.com/SQLServer/feedback/details/1355641/), [Microsoft Connect, n.º 2161595](https://connect.microsoft.com/SQLServer/feedback/details/2161595/), [Microsoft Connect, n.º 1854041](https://connect.microsoft.com/SQLServer/feedback/details/1854041/), [Microsoft Connect, n.º 1055617](https://connect.microsoft.com/SQLServer/feedback/details/1055617/), [Microsoft Connect, n.º 2448774](https://connect.microsoft.com/SQLServer/feedback/details/2448774/), [Microsoft Connect, n.º 1521405](https://connect.microsoft.com/SQLServer/feedback/details/1521405/), [Microsoft Connect, n.º 2117853](https://connect.microsoft.com/SQLServer/feedback/details/2117853/), [Microsoft Connect, n.º 2014256](https://connect.microsoft.com/SQLServer/feedback/details/2014256/), [Microsoft Connect, n.º 2162218](https://connect.microsoft.com/SQLServer/feedback/details/2162218/), [Microsoft Connect, n.º 2344551](https://connect.microsoft.com/SQLServer/feedback/details/2344551/), [Microsoft Connect, n.º 1664436](https://connect.microsoft.com/SQLServer/feedback/details/1664436/), [Microsoft Connect, n.º 2554043](https://connect.microsoft.com/SQLServer/feedback/details/2554043/), [Microsoft Connect, n.º 2983216](https://connect.microsoft.com/SQLServer/feedback/details/2983216/), [Microsoft Connect, n.º 2021706](https://connect.microsoft.com/SQLServer/feedback/details/2021706/)

* Mejoras del Asistente para la optimización de motor de base de datos para admitir una carga de trabajo de lectura automáticamente desde el almacén de consultas de SQL Server.

* Mejoras del Asistente para la optimización de motor de base de datos para mostrar las recomendaciones de índices para los índices de almacén de columnas en el clúster, índices de almacén de columnas que no están en el clúster e índices de almacenamiento de filas.

* Compatibilidad para enviar comandos de consola de base de datos (DBCC) mediante cmdlets de PowerShell de SQL Server Analysis Services.

* Corrección de errores para ver el texto no cifrado de columnas de objetos grandes (LOB) de descifrado AlwaysEncrypted en SSMS.  
*Solicitudes de error de clientes vinculadas:*   
[Microsoft Connect, n.º 2413024](https://connect.microsoft.com/SQLServer/feedback/details/2413024/cannot-view-cleartext-of-alwaysencrypted-lob-columns-in-ssms)

* Corrija los errores en el cuadro de diálogo de Always Encrypted para corregir bloqueos cuando los estilos visuales de Windows no estén habilitados (por ejemplo, habilitar la visualización de contraste alto).

* Corrección de errores para el error 'No se encontró el método', que impide la conexión con instancias de SQL Server.

* Corrección de errores de bloqueo SSMS al crear una función de partición con el desplazamiento de fecha y hora.

* Corrección de errores para agregar/quitar el requisito de Microsoft .NET 3.5 para iniciar la herramienta de administración de Distributed Replay (DReplay.exe).

* Corrección de errores en el Asistente para implementación de Analysis Services para admitir nombres de servidor completos.

* Corrección de errores en SSMS para mostrar las particiones en los modelos tabulares de Analysis Services con un modelo de compatibilidad de 2016.  
*Solicitudes de error de clientes vinculadas:*   
[Microsoft Connect, n.º 2845053](https://connect.microsoft.com/SQLServer/feedback/details/2845053/ssms-cannot-display-partitions-in-tabular-models-in-2016-compatibility-level) 

* Mejoras de rendimiento y correcciones de errores en los modelos tabulares de Analysis Services y objetos de administración compartida de SQL Server (SMO). 


---
## <a name="ssms-july-2016-hotfix-update-release"></a>Versión de actualización de revisión SSMS, julio de 2016 
Disponible con carácter general | Número de versión: 13.0.15600.2

* **Corrija los errores en SSMS para habilitar elementos de menú de clic con el botón derecho que faltan**.  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2883440](https://connect.microsoft.com/SQLServer/feedback/details/2883440/lost-table-design-and-edit-top-n-rows-in-tables-context-menu)  
[Microsoft Connect, n.º 2909644](https://connect.microsoft.com/SQLServer/feedback/details/2909644/ssms-2016-is-missing-edit-options-against-sql-express-2014)  
[Microsoft Connect, n.º 2924345](https://connect.microsoft.com/SQLServer/feedback/details/2924345/some-ssms-object-explorer-right-click-menu-options-missing-in-july-update)

---
## <a name="ssms-july-2016-release"></a>Versión SSMS, julio de 2016 
Disponible con carácter general | Número de versión: 13.0.15500.91

* *Edición, 5 de julio:*  **compatibilidad mejorada para bases de datos tabulares de SQL Server 2016 (nivel de compatibilidad de 1200) en el cuadro de diálogo del proceso de Analysis Services y el Asistente para la implementación de Analysis Service**.

* *Edición, 5 de julio:*  **opción nueva en el cuadro de diálogo de opciones de ejecución de consulta de SSMS para establecer 'XACT_ABORT'. Esta opción está habilitada de forma predeterminada en esta versión de SSMS e indica a SQL Server que revierta la transacción completa y anule el lote si se produce un error de tiempo de ejecución**.

* **Compatibilidad con Almacenamiento de datos SQL de Azure en SSMS.**

* **Actualizaciones importantes para el módulo de PowerShell de SQL Server. Esto incluye un nuevo [módulo de PowerShell de SQL y nuevos CMDLET para Always Encrypted, Agente SQL y los registros de error de SQL](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update)**.

* **Compatibilidad con la generación de scripts de PowerShell en el asistente para Always Encrypted**.

* **Tiempos de conexión significativamente mejorados para las bases de datos SQL de Azure.**

* **Nuevo cuadro de diálogo de copia de seguridad en la dirección URL para admitir la creación de credenciales de Almacenamiento de Azure para copias de seguridad de la base de datos de SQL Server 2016. Esto proporciona una experiencia más sencilla para almacenar las copias de seguridad de la base de datos en una cuenta de almacenamiento de Azure.**
 
* **Nuevo cuadro de diálogo de restauración para simplificar la restauración de una copia de seguridad de una base de datos de SQL Server 2016 desde el servicio de almacenamiento de Microsoft Azure.**
 
* **Corrección de errores en el diseñador de consultas SSMS para permitir agregar tablas al diseñador si un usuario no tiene permisos SELECT sobre ellos.**

* **Corrección de errores para agregar compatibilidad con IntelliSense para las funciones "TRY_CAST()" y "TRY_CONVERT()".**  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, elemento n.º 2453461](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast).

* **Corrección de errores del módulo de PowerShell para habilitar la carga de la extensión Analysis Services de "SQLAS".**  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2544902](https://connect.microsoft.com/SQLServer/feedback/details/2544902/ssms-march-2016-refresh-sqlps-failed-to-load-the-sqlas-extension).

* **Corrección de errores en la ventana del editor de SSMS para permitir arrastrar y colocar archivos abiertos de SQL.**  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2690658](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios).

* **Corrección de errores en el generador de perfiles para corregir el bloqueo del generador de perfiles al salir.**  
*Solicitudes de error de clientes vinculadas:*  
[(Microsoft Connect, n.º 2616550)](https://connect.microsoft.com/SQLServer/feedback/details/2616550/sql-server-2016-rc2-profiler-version-13-0-1300-275-wont-close-after-trace-is-started-even-after-trace-is-stopped).  
[(Microsoft Connect, n.º 2319968)](https://connect.microsoft.com/SQLServer/Feedback/Details/2319968).

* **Corrección de errores en SSMS para evitar el bloqueo al intentar editar un vínculo de unión en el diseñador de tablas de SSMS.**  
*Solicitudes de error de clientes vinculadas:*  
[(Microsoft Connect, n.º 2721052)](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms).

* **Corrección de errores en SSMS para habilitar la generación de scripts de base de datos para los miembros del rol db_owner.**  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2869241](https://connect.microsoft.com/SQLServer/feedback/details/2869241/error-with-script-database-as-create-to-in-ssms-2008r2-and-ssms-2016-june).

* **Corrección de errores en el editor de SSMS para quitar el retraso al cerrar una pestaña de consulta si el servidor se ha desconectado.**  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2656058](https://connect.microsoft.com/SQLServer/feedback/details/2656058/ssms-2014-2016-query-tab-takes-significantly-longer-to-close-if-the-instance-it-was-connected-to-is-now-offline).

* **Corrección de errores para habilitar la opción de copia de seguridad de bases de datos de SQL Server Express.**  
*Solicitudes de error de clientes vinculadas:*  
[(Microsoft Connect, n.º 2801910)](https://connect.microsoft.com/SQLServer/feedback/details/2801910/ssms-2016-backup-option-not-appearing-in-tasks).  
[(Microsoft Connect, n.º 2874434)](https://connect.microsoft.com/SQLServer/feedback/details/2874434/backup-missing-from-tasks-context-menu-in-ssms-2016-when-you-are-connected-to-an-express-instance).

* **Corrección de errores en Analysis Services para mostrar correctamente el proveedor de fuente de datos para modelos multidimensionales de Analysis Services.**

----
## <a name="ssms-june-2016-generally-available-release"></a>Versión de disponibilidad general SSMS de junio de 2016
Disponible con carácter general | Número de versión: 13.0.15000.23

* **SSMS está generalmente disponible a partir de la versión de junio de 2016.**

* **Nuevo cuadro de diálogo de búsqueda rápida en SSMS que se integra mejor en el documento actual y permite realizar búsquedas mediante expresiones regulares.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/>

* **Mejoras en el instalador de SSMS para que pueda realizar un seguimiento de los códigos de salida de proceso y progreso de instalación para instalaciones desatendidas mediante secuencias de comandos.**

* **Corrección de errores en la ayuda F1 contextual de SSMS para ver correctamente los artículos y documentos de ayuda.**

* **Corrección de errores en la vista "Consultas con regresión" del almacén de datos de consulta que provocaban que SSMS se bloquease al desplazarse.** 

* **Corrección de errores en el conector OLEDB de Excel Analysis Services para permitir las conexiones de Excel 2016 a SQL Server Analysis Services.**

* **Corrección de errores en el cuadro de diálogo de conexión de SSMS para mostrar el cuadro de diálogo de conexión en el mismo monitor que la ventana principal de SSMS en sistemas de varios monitores.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/>
<https://connect.microsoft.com/SQLServer/feedback/details/755689/sql-server-management-studio-connect-to-server-popup-dialog/>  
<https://connect.microsoft.com/SQLServer/feedback/details/389165/sql-server-management-studio-gets-confused-dealing-with-multiple-displays/>

* **Correcciones de errores en la experiencia de Always Encrypted. Se ha corregido en el que la opción de menú de Always Encrypted no estaba habilitada correctamente para las bases de datos de Stretch. También se ha corregido el error en el asistente de Always Encrypted por el que no se ha utilizaba correctamente el proveedor HSM de SafeNet (Luna SA).**

---
## <a name="ssms-april-2016-preview"></a>Versión preliminar de SafeNet, abril de 2016 
Número de versión: 13.0.14000.36
  
* **Mejora en el instalador de SSMS para agregar mensajes de error legibles.**  
  
* **Mejora en el Asistente para la base de datos de Stretch para agregar compatibilidad con predicados**.  
  
* **Mejora en el cmdlet de AlwaysEncrypted Powershell para agregar las API de cifrado de clave**.  
  
* **Corrección de errores para desactivar IntelliSense en la barra de herramientas SSMS si se ha deshabilitado en el cuadro de diálogo Opciones, Herramientas.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2555163/sql-2016-rc2-turning-off-intellisense-from-options-does-not-turn-it-off-on-toolbar/>  
    
* **Las mejoras y correcciones de errores en la interfaz de usuario de comparación de Showplan para reducir el espacio utilizado por los planes de consulta largos**.  
  
* **Correcciones de errores en SSMS para corregir los problemas que causaron que SSMS se bloqueara al salir**.   
  
* **Correcciones de errores en el asistente de Always Encrypted para conservar los permisos de usuario durante el cifrado y para permitir que la base de datos separara las operaciones una vez completado el asistente**.  
  
* **Corrección de errores en el cuadro de diálogo de nueva clave maestra de columna de Always Encrypted para proporcionar comentarios sobre el intento de generar una clave mediante un proveedor de algoritmo criptográfico (CNG) no admitido.**  
  
---  
## <a name="ssms-march-2016-preview-refresh"></a>Actualización de versión preliminar de SSMS, marzo de 2016
Número de versión: 13.0.13000.55
  
* **SSMS utiliza el shell aislado de Visual Studio 2015.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2390544/update-ssms-to-use-visual-studio-2015-dependencies/>  
  
* **Nueva barra de herramientas de inicio rápido que le ayuda a encontrar rápidamente elementos del menú y opciones. (VS 2015, shell aislado)**  
  
* **Mejoras en las opciones de temas de SSMS para agregar compatibilidad para un tema claro de SSMS. (VS 2015, shell aislado)**  
  
* **Corrección de errores en la opción del menú de herramientas de SSMS para restablecer correctamente los accesos directos de consulta si se presiona el botón "Restablecer valores predeterminados".**  
  
* **Corrección de errores en las nuevas plantillas de proyecto de SSMS para mostrar los nombres de plantilla fácilmente legibles.**  
  
* **Error resuelto con la visualización del historial de trabajos del Agente SQL en SSMS.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2458860/error-viewing-job-history-microsoft-datawarehouse-sqm/>  
    
* **Corrección de errores para permitir la instalación sin conexión de SSMS. Esto le permite instalar sin necesidad de una conexión a Internet. (VS 2015, shell aislado)**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2497178/cannot-install-ssms-when-server-has-no-internet-access/>  
    
* **Corrección de errores para conservar el directorio actual del usuario cuando se importa el módulo de SQL Server PowerShell (SQLPS).**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2434605/loading-sqlps-module-changes-current-directory-to-ps-sqlserver/>  
    
* **Corrección de errores en el módulo de SQL Server PowerShell (SQLPS) para usar los verbos de PowerShell aprobados.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2432891/sqlps-module-uses-unapproved-powershell-verbs/>  
    
* **Corrección de errores en el módulo de SQL Server PowerShell (SQLPS) para cargar el módulo más rápido.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2429153/sqlps-module-is-slow-to-load/>  
    
* **Corrección de errores en los pasos de trabajo del Agente SQL para permitir la modificación del paso de trabajo.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2453996/issues-with-agent-in-ssms-2016-rc0-13-0-12000-65/>  
    
* **Corrección de errores en el Explorador de objetos de SSMS para enumerar las tablas alfabéticamente.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2424718/sql-server-2016-ssms-table-list-confusing/>  
    
* **Corrección de errores en la lista desplegable "bases de datos disponibles" para mostrar la lista exacta de los nombres de base de datos cuando se modifica una conexión de SQL Server.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2513420/available-databases-drop-down-box-does-not-update-when-connection-changes-in-ssms/>  
    
* **Corrección de errores en los métodos abreviados de teclado de SSMS para centrarse en la lista desplegable "bases de datos disponibles" con la pulsación de tecla "CTRL+U"**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2534820/ssms-ctrl-u-doesnt-work/>  
  
---  
## <a name="ssms-march-2016-preview"></a>Versión preliminar de SSMS, marzo de 2016 
Número de versión: 13.0.12500.29 
  
* **Mejora en el instalador web de SSMS para permitir la navegación utilizando las teclas del teclado.**  
  
* **Mejora en el Asistente de AlwaysEncrypted para admitir tipos de datos de alias para el cifrado.**  
  
* **Corrección de errores en el asistente "Nuevo grupo de disponibilidad" de AlwaysOn para mostrar el número correcto de destinos máximos de conmutación por error automática.**  
*Solicitudes de error de clientes vinculadas:* <https://connect.microsoft.com/SQLServer/feedback/details/2333670/ssms-is-showing-the-wrong-number-of-maximum-automatic-failover-targets/>  
    
* **Corrección de errores en el instalador web de SSMS para corregir los errores que afectan a la instalación.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2181548/sql-server-2016-ctp-3-2-management-studio-setup/>  
    
* **Corrección de errores en la versión de versión preliminar de SSMS para habilitar el guardado de planes de mantenimiento en SQL Server 2012 y versiones inferiores.**  
      
* **Correcciones de errores en el Asistente para la copia de seguridad para permitir varios nombres de copia de seguridad personalizados para las copias de seguridad seccionadas y para mostrar el nombre de archivo de copia de seguridad adecuado si se escribe un nombre nuevo después de seleccionar una credencial de almacenamiento.**  
  
---  
## <a name="ssms-february-2016-preview"></a>Versión preliminar de SSMS, febrero de 2016 
Número de versión: 13.0.12000.65
  
* **Mejora en el monitor de actividad para mostrar las opciones de texto cuando se habilita la configuración de alto contraste en SSMS.**  
  
* **Mejora en el cuadro de diálogo del asistente de Always Encrypted para mostrar una advertencia si se va a cambiar la intercalación de una columna durante el proceso de cifrado.**  
  
* **Mejora en la administración de directivas para agregar compatibilidad para la creación de condiciones en las claves de cifrado de columnas, los valores de clave de cifrado de columnas y las claves maestras de columnas.**  
  
* **Corrección de errores para mejorar el uso del cuadro de diálogo de limpieza de clave maestra de Always Encrypted y mensajes de error de Always Encrypted.**  
  
* **Corrección de errores para deshabilitar la rotación de claves maestras de la columna de Always Encrypted si solo existe una clave.**  
  
* **Corrección de errores para el error "inicializador de tipo" que se produce si el cuadro de diálogo de Always Encrypted se inicia mediante la versión de enero de SSMS o la versión de SSMS incluida en el medio de RC0 de SQL Server.**  
  
---  
## <a name="ssms-january-2016-preview"></a>Versión preliminar de SSMS, enero de 2016 
Número de versión: 13.0.11000.78 
  
* **Corrección de errores en SSMS para permitir que se eliminen las sesiones de eventos extendidos (XEvent).**  
  
* **Corrección de errores para poder abrir el cuadro de diálogo Propiedades de un grupo de disponibilidad de SQL Server 2014.**  
 *Solicitudes de error de clientes vinculadas:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/1609719/>  
     
* **Corrección de errores para poder agregar una réplica de Azure a un grupo de disponibilidad.**  
 *Solicitudes de error de clientes vinculadas:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2029135/>  
     
* **Corrección de errores para poder abrir el cuadro de diálogo Propiedades de las bases de datos de SQL Server 2014.**  
 *Solicitudes de error de clientes vinculadas:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2080209/>  
     
* **Corrección de errores destinada a quitar las columnas duplicadas que aparecen para cada tabla cuando se conectan a una base de datos de SQL Azure.**  
 *Solicitudes de error de clientes vinculadas:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2103116/>  
---  
## <a name="ssms-december-2015-preview"></a>Versión preliminar de SSMS, diciembre de 2015 
Número de versión: 13.0.900.73
  
* **Mejoras en la comparación de plan de presentación para habilitar la comparación del plan de ejecución de consulta actual con uno guardado en un archivo.**  
  
* **Compatibilidad con IntelliSense mejorada para los índices de almacén de columnas insertados en SSMS.**  
  
* **Corrección de errores en el asistente para la sesión de Eventos extendidos para habilitar la selección de plantillas cuando se conecte a un servidor Azure V12.**  
  
* **Nuevas tabulaciones en los cuadros de diálogo "Crear auditoría" y "Nuevo inicio de sesión" de la carpeta de seguridad para permitir una navegación más sencilla mediante el teclado.**  
  
* **Corrección de errores para habilitar la funcionalidad para "Cambiar a la pestaña de resultados tras la ejecución de la consulta" si SSMS está establecido para mostrar los resultados en formato de cuadrícula.**   
 *Solicitudes de error de clientes vinculadas:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1390296/switch-to-results-tab-after-query-execution-grid-mode-in-ssms-2016>  
  
* **Corrección de errores para mostrar los encabezados de columna sin truncar si SSMS se establece para mostrar los resultados en formato de cuadrícula.**  
 *Solicitudes de error de clientes vinculadas:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/2004111/bugbash-column-headers-in-grid-mode-truncated-with-courier-new-8>  
      
* **Correcciones de errores para permitir la correcta instalación del instalador web SSMS.**  
 *Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2003865/ssms-october-preview-incoherent-error-message>  
<https://connect.microsoft.com/SQLServer/feedback/details/2079557/unable-to-instal-sql-server-update-13-0-800-111-over-13-0-700-242-error-code-2711>  
  
---  
## <a name="ssms-november-2015-preview"></a>Versión preliminar de SSMS, noviembre de 2015
Número de versión: 13.0.800.111
  
* **Compatibilidad con el ajuste de escala de mapa de bits para las pantallas con valores altos de PPP en SSMS.**  
  
* **Mejoras en la interfaz de usuario de asistentes y cuadros de diálogo de AlwaysEncrypted para simplificar el proceso de creación de claves de cifrado de base de datos.**  
  
* **Nueva opción del menú contextual en la lista de "Procesos" del monitor de actividad para ver las estadísticas de consultas dinámicas.**  
  
* **Corrección de errores para habilitar la correcta desinstalación de las versiones preliminares de SSMS en equipos cliente.**  
  *Solicitudes de error de clientes vinculadas:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1868474/ssms-2016-preview-can-be-installed-but-not-uninstalled>  
  
* **Corrección de errores para permitir la edición de pasos de trabajo en el agente de trabajo SQL incluso cuando falta un archivo**.  
  *Solicitudes de error de clientes vinculadas:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
    <https://connect.microsoft.com/SQLServer/feedback/details/1502100/ssms-preview-error>  
      
* **Corrección de errores en la opción de menú "Ver datos de destino" para una sesión de Eventos extendidos en una base de datos que se ejecuta en una máquina virtual de Azure.**  
  *Solicitudes de error de clientes vinculadas*:  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
***  

## <a name="ssms-october-2015-preview"></a>Versión preliminar de SSMS, octubre de 2015 
Número de versión: 13.0.700.242  
* **Nuevo instalador web ligero y modernizado que simplifica el proceso de instalación y descarga de SSMS.**  
  
* **Nuevo asistente para el cifrado de columnas Always Encrypted que permite el cifrado en el cliente y el descifrado de las columnas seleccionadas.**  
  
* **Nuevo cuadro de diálogo de rotación de claves maestras de columna (CMK) para bases de datos Always Encrypted que simplifica el proceso de rotación de claves de cifrado con el fin de proteger los datos.**  
  
* **Nuevo monitor de Stretch Database que permite solucionar problemas y supervisar el estado de la migración de los datos a la nube de Azure.**  
  
* **Mejoras en el asistente para Stretch Database para admitir la elección de un servidor de Microsoft Azure que no esté en la suscripción predeterminada de Microsoft Azure.**  
  *Solicitudes de error de clientes vinculadas:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1687063/cannot-choose-from-multiple-microsoft-azure-subscriptions>  
* **Corrección de errores para permitir la visualización adecuada del plan de ejecución activo en SSMS.**  
  *Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1774446/viewing-live-execution-plan-from-activity-monitor-crashes-ssms>    
* **Corrección de errores para quitar opciones no válidas de scripting de SSMS de las instantáneas de la base de datos**  
  *Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1515168/ssms-scripting-of-database-snapshots-includes-invalid-options>  
* **Corrección de errores en la interfaz de usuario del almacén de datos de consulta para mostrar detalles en el panel "Consultas que más recursos consumen".**  
  *Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1737185/sql-server-2016-overall-resource-consumption-query-store-pane-issue>  
***  

## <a name="ssms-september-2015-preview"></a>Versión preliminar de SSMS, septiembre de 2015 
Número de versión: 13.0.600.65  
* **Nuevo cuadro de diálogo para la regla de firewall que agiliza el proceso de conexión a una base de datos de SQL Azure.**      
    
* **Se ha actualizado el cuadro de diálogo "Nuevo índice" que permite la creación de los índices de almacén de filas no agrupados cuando hay un índice de almacén de columnas agrupado presente. Esta funcionalidad está disponible para SQL 2016 y versiones superiores.**      
  *Solicitudes de error de clientes vinculadas:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1552617/creation-of-nc-index-when-clustered-columnstore-index>  
      
* **Corrección de errores para poder ver y editar los pasos del trabajo del Agente SQL en las versiones preliminares de SSMS que se ejecutan en Windows 7.**      
  *Solicitudes de error de clientes vinculadas:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1548140/cannot-view-or-edit-any-sql-agent-job-step>,    
  <https://connect.microsoft.com/SQLServer/feedback/details/1626895/unable-to-load-dll-dts>,    
  <https://connect.microsoft.com/SQLServer/feedback/details/1576662/error-creating-new-job-step>     
      
* **Corrección de errores para mostrar los nodos de desencadenador en SSMS para SQL Server 2014 y versiones posteriores.**      
  *Solicitudes de error de clientes vinculadas:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1617533/trigger-node-missing>   
      
* **Correcciones de errores en la interfaz de usuario para informes estándar del servidor y la base de datos para excluir la información de la versión del encabezado.**      
  *Solicitudes de error de clientes vinculadas:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1387471/report-headings-wrongly-named>  
      
* **Corrección de errores para evitar que se muestre un nodo de estadísticas de consultas activas como completado si está incompleto.**      
  *Solicitudes de error de clientes vinculadas:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1589096/live-query-statistics-node-shows-as-completed>  
  
***      
## <a name="ssms-august-2015-preview"></a>Versión preliminar de SSMS, agosto de 2015 
Número de versión: 13.0.500.53
  
* **Actualizaciones del explorador de objetos para reducir el retraso de la carga cuando hay un gran número de bases de datos.**  
  
* **Mejoras para la instalación de SSMS en equipos con Windows 10.**  
  
* **Correcciones de errores y actualizaciones para el administrador de configuración de SQL Server y la interfaz de usuario de informes de usuario de SSMS**    
***  
  
## <a name="ssms-july-2015-preview"></a>Versión preliminar de SSMS, julio de 2015
Número de versión: 13.0.400.91
  
* **Diagramas de base de datos para la Base de datos SQL de Azure (V12).**  
  
* **Se ha mejorado la compatibilidad de IntelliSense con la nueva sintaxis de tabla temporal.**  
  
* **Se ha actualizado la biblioteca de DacFx para admitir las características más recientes de las bases de datos SQL de Azure, como la seguridad de nivel de fila y la autenticación de Azure Active Directory.**  
  
* **Correcciones de errores (se ha actualizado la interfaz de usuario para "buscar actualizaciones", se ha corregido la interfaz de usuario en la lista "nivel de compatibilidad", etc.).**  
***  
  
## <a name="ssms-june-2015-preview"></a>Versión preliminar de SSMS, junio de 2015 
Número de versión: 13.0.300.44
  
* **Nuevo instalador web ligero de SSMS.**  
  
* **Búsqueda automática de actualizaciones.**  
  
* **SSMS es ahora compatible con la búsqueda de texto completo de la Base de datos SQL de Azure (V12).**  
  
* **Principales solicitudes de cliente tratadas:**  
  * Se ha habilitado "Editar las primeras 200 filas" para las tablas y vistas del Explorador de objetos.  
  * Se ha habilitado el diseñador de tablas de la Base de datos SQL de Azure (V12).  
  * Se han habilitado cuadros de diálogos de propiedades de la base de datos y de las tablas para la Base de datos SQL de Azure (V12).  
    
 * **Nueva opción para omitir la pregunta de si desea guardar los archivos de T-SQL.**  
   
 * **Compatibilidad del asistente para importación y exportación con los nuevos niveles de servicio de Base de datos SQL de Azure (Basic, Standard, Premium).**  
   
 * **Numerosas correcciones de errores (escenarios de scripting, habilitación del seguimiento de cambios para bases de datos SQL, etc.).**   
     
  
  
  
  
  
  
    

