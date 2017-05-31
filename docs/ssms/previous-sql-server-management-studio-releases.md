---
title: Versiones anteriores de SQL Server Management Studio | Microsoft Docs
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 87f593c3-8b76-4c12-963a-31d35f2fb294
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0773be32343e4707503b4acb616e5a1c807fe32f
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="previous-sql-server-management-studio-releases"></a>Versiones anteriores de SQL Server Management Studio
  
Están disponibles las siguientes versiones anteriores de SQL Server Management Studio.


   
### <a name="downloadssdtmediadownloadpng-sql-server-management-studio-165-releasehttpgomicrosoftcomfwlinklinkid832812"></a>![descargar](../ssdt/media/download.png) [SQL Server Management Studio versión 16.5](http://go.microsoft.com/fwlink/?LinkID=832812)

**Información de versión**  
  
*Esta versión de SSMS utiliza el Shell aislado de Visual Studio 2015.*  
Número de versión: 16.5  
Número de compilación para esta versión: 13.0.16000.28

**Problemas conocidos de esta compilación**  

1. Invoke-Sqlcmd inserta por error varias filas cuando se produce la restricción Check. [Microsoft Connect, n.º 811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

2. Las versiones de idiomas diferentes de ESN no funcionan completamente al crear Grupos de disponibilidad.

3. Al hacer clic en el plan de consulta XML, no se abre la IU de SSMS adecuada.

**Registro de cambios**

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


   
### <a name="downloadssdtmediadownloadpng-sql-server-management-studio-1641-september-2016-releasehttpgomicrosoftcomfwlinklinkid828615"></a>![descargar](../ssdt/media/download.png) [SQL Server Management Studio 16.4.1 (versión de septiembre de 2016)](http://go.microsoft.com/fwlink/?LinkID=828615)

**Información de versión**  
  
*Esta versión de SSMS utiliza el Shell aislado de Visual Studio 2015.*  
Número de versión: 16.4.1  
Número de compilación para esta versión: 13.0.15900.1
  
**Problemas conocidos de esta compilación**  

1. **Una sola cuenta de Azure Active Directory puede iniciar sesión para una instancia de SSMS utilizando la autenticación universal de Active Directory.**  
    Esta restricción se limita a la autenticación universal de Active Directory. Puede iniciar sesión en servidores diferentes mediante la autenticación de contraseña de Active Directory, la autenticación integrada de Active Directory o la autenticación de SQL Server.
    
    Como alternativa, puede utilizar otra instancia de SSMS para iniciar sesión con otra cuenta de Azure Active Directory. 
    
2. **Los comandos del marco de aplicación de capa de datos (DacFx) y el Diseñador de esquemas en SSMS no admiten la autenticación universal de Active Directory.**  
    Los comandos que utiliza DacFx (por ejemplo, importar y exportar) y el Diseñador de esquemas en SSMS no admiten actualmente la autenticación universal de Active Directory.
    
    Como solución alternativa, puede usar las otras formas de autenticación proporcionada en SSMS - autenticación de contraseña de Active Directory, la autenticación integrada de Active Directory o la autenticación de SQL Server.

3. **SSMS solo puede conectarse a instancias de SQL Server 2016 Integrated Services (SSIS 2016).**  
    Hay una limitación de compatibilidad conocida con SQL Server Integration Services que impide la conexión a versiones anteriores.
    
    Como solución alternativa para este problema, puede conectarse a la instancia de SQL Server Integration Service mediante la [versión SSMS alineado con la instancia SSIS.](../ssms/previous-sql-server-management-studio-releases.md) 
  
4. **SSMS no guardará los planes de mantenimiento de SQL Server 2008 R2 y versiones anteriores de SQL Server.**  
    Se trata de una limitación conocida que esperamos solucionar en el futuro. Mientras tanto, puede usar la [versión de SSMS de 2014](../ssms/previous-sql-server-management-studio-releases.md) para guardar los planes de mantenimiento.  
    
5. **Las instalaciones de SSMS que no estén en inglés pueden requerir la instalación de un paquete de seguridad adicional.**  
Las versiones localizadas de SSMS en idiomas diferentes al inglés requieren el [paquete de actualización de seguridad KB 2862966](https://support.microsoft.com/en-us/kb/2862966) si se instalan en Windows 8, Windows 7, Windows Server 2012 y Windows Server 2008 R2.
  
6. **Administrador de configuración de SQL Server no se iniciará si no hay ningún servidor de SQL Server instalado en el equipo cliente**  
    Si no tiene SQL Server instalado en el equipo cliente e inicia el Administrador de configuración de SQL Server, verá el siguiente error:   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`,   
   
     * Si ha agregado instancias de SQL Server a la lista 'Servidores registrados' en SSMS:  
        1. Desplácese a la vista 'Servidores registrados' en SSMS.  
        2. Haga clic con el botón derecho en la instancia de SQL Server que desee configurar.  
        3. Seleccione 'Administrador de configuración de SQL Server' en el menú de clic con el botón derecho.    
          
      * Si no ha agregado una instancia de SQL Server a la lista 'Servidores registrados' en SSMS:  
        1. Abra un símbolo del sistema como administrador.  
        2. Ejecute la herramienta Mofcomp con el siguiente comando:  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. Después de ejecutar la herramienta Mofcomp, ejecute los comandos para reiniciar el servicio WMI para que los cambios surtan efecto:  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  

 
**Registro de cambios** 

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
[Microsoft Connect, nº 2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)

*  Se corrigió un problema en el asistente Restaurar base de datos no aceptaría nombres de archivo con espacios en blanco iniciales:   
[Microsoft Connect, nº 2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



### <a name="downloadssdtmediadownloadpng-sql-server-management-studio-163-august-2016-releasehttpgomicrosoftcomfwlinklinkid824938"></a>![descargar](../ssdt/media/download.png) [SQL Server Management Studio 16.3 versión de agosto de 2016](http://go.microsoft.com/fwlink/?LinkID=824938)
 15 de agosto de 2016 | Número de versión: 13.0.15700.28

**Características**  
1. Nueva opción de autenticación 'Autenticación universal de Active Directory'
2. Nuevos cmdlets para el módulo de PowerShell de SQL Server
3. Mejoras en las plantillas de Asistente para la optimización de motor de base de datos (DTA) y eventos extendidos
4. Compatibilidad en versión beta con [pantallas de alta resolución en SSMS](https://blogs.msdn.microsoft.com/sqlreleaseservices/ssms-highdpi-support/)

[Obtenga más información sobre las funciones disponibles en el registro de cambios de SSMS.](../ssms/sql-server-management-studio-changelog-ssms.md)

**Problemas conocidos**

A continuación indicamos los problemas y las limitaciones de esta versión de SQL Server Management Studio:  

1. **Una sola cuenta de Azure Active Directory puede iniciar sesión para una instancia de SSMS utilizando la autenticación universal de Active Directory.**  
    Esta restricción se limita a la autenticación universal de Active Directory. Puede iniciar sesión en servidores diferentes mediante la autenticación de contraseña de Active Directory, la autenticación integrada de Active Directory o la autenticación de SQL Server.
    
    Como alternativa, puede utilizar otra instancia de SSMS para iniciar sesión con otra cuenta de Azure Active Directory. 
    
2. **Los comandos del marco de aplicación de capa de datos (DacFx) y el Diseñador de esquemas en SSMS no admiten la autenticación universal de Active Directory.**  
    Los comandos que utiliza DacFx (por ejemplo, importar y exportar) y el Diseñador de esquemas en SSMS no admiten actualmente la autenticación universal de Active Directory.
    
    Como solución alternativa, puede usar las otras formas de autenticación proporcionada en SSMS - autenticación de contraseña de Active Directory, la autenticación integrada de Active Directory o la autenticación de SQL Server.

3. **SSMS solo puede conectarse a instancias de SQL Server 2016 Integrated Services (SSIS 2016).**  
    Hay una limitación de compatibilidad conocida con SQL Server Integration Services que impide la conexión a versiones anteriores.
    
    Como solución alternativa para este problema, puede conectarse a la instancia de SQL Server Integration Service mediante la [versión SSMS alineado con la instancia SSIS.](../ssms/previous-sql-server-management-studio-releases.md) 
  
4. **SSMS no guardará los planes de mantenimiento de SQL Server 2008 R2 y versiones anteriores de SQL Server.**  
    Se trata de una limitación conocida que esperamos solucionar en el futuro. Mientras tanto, puede usar la [versión de SSMS de 2014](../ssms/previous-sql-server-management-studio-releases.md) para guardar los planes de mantenimiento.  
    
5. **Las instalaciones de SSMS que no estén en inglés pueden requerir la instalación de un paquete de seguridad adicional.**  
Las versiones localizadas de SSMS en idiomas diferentes al inglés requieren el [paquete de actualización de seguridad KB 2862966](https://support.microsoft.com/en-us/kb/2862966) si se instalan en Windows 8, Windows 7, Windows Server 2012 y Windows Server 2008 R2.
  
6. **Administrador de configuración de SQL Server no se iniciará si no hay ningún servidor de SQL Server instalado en el equipo cliente**  
    Si no tiene SQL Server instalado en el equipo cliente e inicia el Administrador de configuración de SQL Server, verá el siguiente error:   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`,   
   
     * Si ha agregado instancias de SQL Server a la lista 'Servidores registrados' en SSMS:  
        1. Desplácese a la vista 'Servidores registrados' en SSMS.  
        2. Haga clic con el botón derecho en la instancia de SQL Server que desee configurar.  
        3. Seleccione 'Administrador de configuración de SQL Server' en el menú de clic con el botón derecho.    
          
      * Si no ha agregado una instancia de SQL Server a la lista 'Servidores registrados' en SSMS:  
        1. Abra un símbolo del sistema como administrador.  
        2. Ejecute la herramienta Mofcomp con el siguiente comando:  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. Después de ejecutar la herramienta Mofcomp, ejecute los comandos para reiniciar el servicio WMI para que los cambios surtan efecto:  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  


**Correcciones**
1. Corrección de errores para ver el texto no cifrado de columnas de objetos grandes (LOB) de descifrado AlwaysEncrypted en SSMS (Microsoft Connect, n.º 2413024).
2. Corrija los errores en el cuadro de diálogo de Always Encrypted para corregir bloqueos cuando los estilos visuales de Windows no estén habilitados (por ejemplo, habilitar la visualización de contraste alto).
3. Corrección de errores para el error 'No se encontró el método', que impide la conexión con instancias de SQL Server.
4. Corrección de errores de bloqueo SSMS al crear una función de partición con el desplazamiento de fecha y hora.
5. Corrección de errores para quitar el requisito de Microsoft .NET 3.5 para iniciar la herramienta de administración de Distributed Replay (DReplay.exe).
6. Corrección de errores en el Asistente para implementación de Analysis Services para admitir nombres de servidor completos.
7. Corrección de errores en SSMS para mostrar las particiones en los modelos tabulares de Analysis Services con un modelo de compatibilidad de 2016 (Microsoft Connect, n.º 2845053).

[Obtenga más información sobre las correcciones disponibles en el registro de cambios de SSMS.](../ssms/sql-server-management-studio-changelog-ssms.md)
 
---
### <a name="downloadssdtmediadownloadpng-sql-server-management-studio-july-2016-hotfix-update-releasehttpgomicrosoftcomfwlinklinkid822301"></a>![descargar](../ssdt/media/download.png) [Versión de actualización de la revisión de julio de 2016 de SQL Server Management Studio](http://go.microsoft.com/fwlink/?LinkID=822301)

13 de julio de 2016 | Número de versión: 13.0.15600.2

**Características**  
1. Compatibilidad con Almacenamiento de datos SQL de Azure en SSMS.   
2. Actualizaciones importantes para el módulo de PowerShell de SQL Server.   
3. Tiempos de conexión significativamente mejorados para las bases de datos SQL de Azure.  
4. Compatibilidad mejorada para bases de datos tabulares de SQL Server 2016 (nivel de compatibilidad de 1200) en el cuadro de diálogo del proceso de Analysis Services, etc.   

[Obtenga más información y conozca las funciones disponibles en el registro de cambios de SSMS.](../ssms/sql-server-management-studio-changelog-ssms.md)

**Problemas conocidos** 
1. **El instalador de la versión de revisión de SSMS de julio aparece como la versión de agosto de SSMS.**
La página de configuración para la revisión de la actualización de julio muestra Agosto debido a una configuración de versión interna. Este paquete realmente es una revisión de la versión de julio de SSMS. 
2. **SSMS no se puede conectar a instancias de SQL Server después de instalar la versión 'revisión de julio de 2016'.**
Somos conscientes de un problema con respecto a la actualización más reciente de SSMS cuando intenta conectarse a un resultado del servidor en el mensaje de error siguiente: 
   ```
    "Method not found: 'Void Microsoft.SqlServer.Management.Common.SqlConnectionInfo.set_ApplicationIntent(System.String)'"
    ```
  
    La corrección para este problema estará disponible en la próxima versión de SSMS. Como solución alternativa para este problema, puede desinstalar y reinstalar SSMS. Para obtener más detalles, [visite este subproceso de Microsoft Connect sobre el problema](https://connect.microsoft.com/SQLServer/feedback/details/2925257/not-able-to-connect-to-sql-server-instances-after-installing-ssms-2016-july-update).
    
3. **SSMS se bloquea al intentar seleccionar una cuenta de almacenamiento de Azure.**
La versión de SSMS de julio y la revisión de julio se bloquean si intenta seleccionar una cuenta de almacenamiento de Azure y no tiene una cuenta de almacenamiento 'clásico'.
La corrección para este problema estará disponible en una próxima versión de SSMS. Como solución alternativa para este problema, puede realizar una copia de seguridad o restaurar las bases de datos a una cuenta de almacenamiento de Azure creando una cuenta de almacenamiento clásico, o [usando T-SQL para realizar la copia de seguridad o restauración](https://msdn.microsoft.com/library/jj720552(v=sql.120).aspx).

4. **SSMS solo mostrará las cuentas de almacenamiento de Azure 'clásico' en los asistentes de copia de seguridad/restauración.**
La versión de SSMS de julio y la revisión de julio muestran solo las cuentas de almacenamiento de Azure 'clásico' para la creación de nuevas credenciales si está tratando de realizar la copia de seguridad o la restauración con los asistentes de copia de seguridad y restauración.
La corrección para este problema estará disponible en una próxima versión de SSMS. Como solución alternativa para este problema, puede realizar una copia de seguridad o restaurar las bases de datos a una cuenta de almacenamiento de Azure 'clásico' disponible o realizar una copia de seguridad de las cuentas de almacenamiento de 'tipo ARM' [con T-SQL para realizar la copia de seguridad o restauración](https://msdn.microsoft.com/library/jj720552(v=sql.120).aspx). 

5. **Las instalaciones de SSMS que no estén en inglés pueden requerir la instalación de un paquete de seguridad adicional.**
Las versiones localizadas de SSMS en idiomas diferentes al inglés requieren el [paquete de actualización de seguridad KB 2862966](https://support.microsoft.com/en-us/kb/2862966) si se instalan en Windows 8, Windows 7, Windows Server 2012 y Windows Server 2008 R2.
6. **SSMS solo puede conectarse a instancias de SQL Server 2016 Integrated Services (SSIS 2016).** Hay una limitación de compatibilidad conocida con SQL Server Integration Services que impide la conexión a versiones anteriores.
Como solución alternativa para este problema, puede conectarse a la instancia de SQL Server Integration Service mediante la versión SSMS alineado con la instancia SSIS.
7. **SSMS no guardará los planes de mantenimiento de SQL Server 2008 R2 y versiones anteriores de SQL Server.** Estamos trabajando en una solución para este problema. Mientras tanto, puede usar la versión de SSMS de 2014 siguiente para guardar los planes de mantenimiento.
8. **El Administrador de configuración de SQL Server no se iniciará si no hay ningún servidor de SQL Server instalado en el equipo cliente.** Si no tiene SQL Server instalado en el equipo cliente e inicia el Administrador de configuración de SQL Server, recibirá el siguiente error: 'No se puede conectar con el proveedor WMI'. Solución alternativa:
    * Abra un símbolo del sistema como administrador.
    * Ejecute la herramienta Mofcomp con el siguiente comando:  
      mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"
    * Después de ejecutar la herramienta Mofcomp, ejecute los comandos para reiniciar el servicio WMI para que los cambios surtan efecto:  
       net stop "Windows Management Instrumentation"  
       net start "Windows Management Instrumentation"

**Correcciones**  
1. Corrección de errores en el diseñador de consultas SSMS para permitir agregar tablas al diseñador si un usuario no tiene permisos SELECT sobre ellos.
2. Corrección de errores para agregar compatibilidad con IntelliSense para las funciones 'TRY_CAST()' y 'TRY_CONVERT()' [(Microsoft Connect, n.º 2453461)](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast).
3. Corrección de errores en la ventana del editor de SSMS para permitir arrastrar y colocar archivos abiertos de SQL [(Microsoft Connect, n.º 2690658)](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios).
4. Corrección de errores en Analysis Services para mostrar correctamente el proveedor de fuente de datos para modelos multidimensionales de Analysis Services.
5. Corrección de errores en SSMS para evitar el bloqueo al intentar editar un vínculo de unión en el diseñador de tablas de SSMS [(Microsoft Connect, n.º 2721052)](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms).  

[Obtenga más información y conozca las revisiones disponibles en el registro de cambios de SSMS.](../ssms/sql-server-management-studio-changelog-ssms.md)

---
### <a name="downloadssdtmediadownloadpng-sql-server-management-studio-june-2016-releasehttpgomicrosoftcomfwlinklinkid799832"></a>![descargar](../ssdt/media/download.png) [SQL Server Management Studio, versión de junio de 2016](http://go.microsoft.com/fwlink/?LinkID=799832)

1 de junio de 2016 | Número de versión: 13.0.15000.23

**Características**  
Nuevo instalador SSMS mejorado. Versiones independientes de SSMS. Búsqueda automática de actualizaciones. Un nuevo cuadro de búsqueda rápida. SSMS se basa en el shell de Visual Studio 2015 y mucho más.   
[Obtenga más información disponibles en el registro de cambios de SSMS.](../ssms/sql-server-management-studio-changelog-ssms.md)

**Problemas conocidos** 
1. **La generación de scripts de PowerShell en el asistente para Always Encrypted está deshabilitada actualmente.**
Una solución para este problema estará disponible en una posterior actualización mensual de SSMS.
2. **El elemento de menú contextual 'Cifrar columnas' en el Explorador de objetos está deshabilitado para las tablas y columnas cuando está conectado a Base de datos SQL de Azure.** Una solución para este problema estará disponible en una posterior actualización mensual de SSMS. Como alternativa, haga clic en la base de datos en el Explorador de objetos, seleccione 'Tareas' y elija 'Cifrar columnas' para cifrar tablas y columnas de Base de datos SQL de Azure.
3. **SSMS solo puede conectarse a instancias de SQL Server 2016 Integrated Services (SSIS 2016).** Hay una limitación de compatibilidad conocida con SQL Server Integration Services que impide la conexión a versiones anteriores.
Como solución alternativa para este problema, puede conectarse a la instancia de SQL Server Integration Service mediante la versión SSMS alineado con la instancia SSIS.
4. **SSMS no guardará los planes de mantenimiento de SQL Server 2008 R2 y versiones anteriores de SQL Server.** Estamos trabajando en una solución para este problema. Mientras tanto, puede usar la versión de SSMS de 2014 siguiente para guardar los planes de mantenimiento.
5. **El Administrador de configuración de SQL Server no se iniciará si no hay ningún servidor de SQL Server instalado en el equipo cliente.** Si no tiene SQL Server instalado en el equipo cliente e inicia el Administrador de configuración de SQL Server, recibirá el siguiente error: 'No se puede conectar con el proveedor WMI'. Solución alternativa:
    * Abra un símbolo del sistema como administrador.
    * Ejecute la herramienta Mofcomp con el siguiente comando:  
      mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"
    * Después de ejecutar la herramienta Mofcomp, ejecute los comandos para reiniciar el servicio WMI para que los cambios surtan efecto:  
       net stop "Windows Management Instrumentation"  
       net start "Windows Management Instrumentation"

**Correcciones**  
1. Cuadro de diálogo de búsqueda rápida en SSMS que se integra mejor en el documento actual y permite realizar búsquedas mediante expresiones regulares ([Microsoft Connect, n.º 2735513](https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/)).
2. Corrija los errores en la ayuda F1 contextual de SSMS para ver correctamente los artículos y documentos de ayuda.
3. Corrija los errores en la vista 'Consultas con regresión' del almacén de datos de consulta que creó que SSMS se bloqueara al desplazarse.
4. Corrija los errores en el conector OLEDB de Excel Analysis Services para permitir las conexiones de Excel 2016 a SQL Server Analysis Services.
5. Corrija los errores en el cuadro de diálogo de conexión de SSMS para mostrar el cuadro de diálogo de conexión en el mismo monitor que la ventana principal de SSMS en sistemas de varios monitores ([Microsoft Connect, n.º 724909)](https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/).
6. Correcciones de errores en la experiencia de Always Encrypted. Se ha corregido en el que la opción de menú de Always Encrypted no estaba habilitada correctamente para las bases de datos de Stretch. También se ha corregido el error en el asistente de Always Encrypted donde no se ha utilizado correctamente el proveedor HSM de SafeNet (Luna SA).

---
### <a name="downloadssdtmediadownloadpng-sql-server-management-studio-2014-sp1httpdownloadmicrosoftcomdownload156156992e6-f7c7-4e55-833d-249bd2348138enux86sqlmanagementstudiox86enuexe"></a>![descargar](../ssdt/media/download.png) [SQL Server Management Studio 2014 SP1](http://download.microsoft.com/download/1/5/6/156992E6-F7C7-4E55-833D-249BD2348138/ENU/x86/SQLManagementStudio_x86_ENU.exe)

14 de mayo de 2015 | Número de versión: 12.0.4100.1

**Características**  
Compatibilidad mejorada de Base de datos SQL de Azure con nuevo menú de apertura en el portal de administración, integración del diseñador de tablas y mucho más.   
[Obtenga más información disponible en las notas de la versión](https://support.microsoft.com/en-us/kb/3058865).

**Problemas conocidos**  
N/D

**Correcciones**
1. SSMS se bloquea durante el movimiento de las tareas del plan de mantenimiento si el nombre del plan de mantenimiento y el primer nombre SUB_PLAN son los mismos.
2. No puede depurar un procedimiento almacenado que llama a sp_executesql en SQL Server Management Studio (SSMS). Cuando presione F11, recibirá un mensaje de error 'Referencia a objeto no establecida para una instancia de objeto' ([Microsoft Connect, n.º 736509](https://connect.microsoft.com/SQLServer/feedback/details/736509/sql-server-2012-rtm-management-studio-cannot-debug-sp-executesql)).
3. SSMS no administra al completo el texto completo en SQL Server Express ([Microsoft Connect, n.º 740181](https://connect.microsoft.com/SQLServer/feedback/details/740181/management-studio-does-not-fully-manage-full-text-in-sql-server-express)).
4. SSMS controla los procedimientos almacenados numerados de forma incoherente [(Microsoft Connect, n.º 764197](https://connect.microsoft.com/SQLServer/feedback/details/764197/ssms-2012-inconsistently-handles-numbered-procedures)).
5. SSMS se bloquea a veces al cerrar, lo que, a continuación, hace que se reinicie automáticamente ([Microsoft Connect, n.º 774317](https://connect.microsoft.com/SQLServer/feedback/details/774317/sql-server-management-studio-2012-2014-crashes-when-closing)).
6. El script de creación duplica las instrucciones cuando se aplica el script a los permisos de nivel de columna en SSMS ([Microsoft Connect, n.º 797967](https://connect.microsoft.com/SQLServer/feedback/details/797967/ssms-create-script-duplicates-the-statements-for-grant-or-deny-column-permissions)).
7. SSMS puede bloquearse cuando intenta actualizar el icono de la ventana de SSMS en la barra de tareas ([Microsoft Connect, n.º 799430](https://connect.microsoft.com/SQLServer/feedback/details/799430/ssms-2012-sp-1-cu-5-installed-crash-when-enforce-refresh-on-connect)).

---
### <a name="downloadssdtmediadownloadpng-sql-server-management-studio-2012-sp3httpdownloadmicrosoftcomdownloadf67f673709c-d371-4a64-8bf9-c1dd73f60990enux86sqlmanagementstudiox86enuexe"></a>![descargar](../ssdt/media/download.png) [SQL Server Management Studio 2012 SP3](http://download.microsoft.com/download/F/6/7/F673709C-D371-4A64-8BF9-C1DD73F60990/ENU/x86/SQLManagementStudio_x86_ENU.exe)  
  
21 de noviembre de 2015 | Número de versión: 11.0.6020.0

**Características**  
Ediciones exprés de SSMS con todas las características. Fragmentos de código. Índices de almacén de columnas y mucho más.  
[Obtenga más información disponible en las notas de la versión.](https://support.microsoft.com/en-us/kb/3072779)
 
**Problemas conocidos**  
N/D

**Correcciones**
1. Las columnas que faltan no pueden indicarse en el mensaje de error cuando importa datos mediante el Asistente para importación y exportación.
2. "No se puede crear el plan de restauraciones debido a una interrupción en la cadena LSN" cuando restaura la copia de seguridad diferencial en SSMS

---
### <a name="additional-downloads"></a>Descargas adicionales  
Para obtener una lista de todas las descargas de SQL Server Management Studio, consulte el [Centro de descargas de Microsoft](https://www.microsoft.com/en-us/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending).  
  
Para obtener la versión más reciente de SQL Server Management Studio, vea [Descargar SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  

---  
## <a name="related-resources"></a>Recursos relacionados
[Centro de actualización para Microsoft SQL Server](https://technet.microsoft.com/sqlserver/ff803383.aspx)   
[Inicio rápido de SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[Foro de SQL Server Management Studio](https://social.msdn.microsoft.com/forums/en-us/home?forum=sqltools)  

  

