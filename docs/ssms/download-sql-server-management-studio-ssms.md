---
title: Descargar SQL Server Management Studio (SSMS) | Microsoft Docs
ms.custom: 
ms.date: 04/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "instalar ssms, descargar ssms, versiones de ssms más recientes"
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- "instalación de sql management studio"
- descargar sql management studio
- ms sql management studio
- instalar sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
caps.latest.revision: 145
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cc827737cec19c11d2102f968dc2b8bc638bda86
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="download-sql-server-management-studio-ssms"></a>Descarga de SQL Server Management Studio (SSMS)
SQL Server Management Studio (SSMS) es un entorno integrado para acceder, configurar, administrar y desarrollar todos los componentes de SQL Server. SSMS combina un amplio grupo de herramientas gráficas con una serie de editores de scripts enriquecidos que permiten a los desarrolladores y administradores de todos los niveles acceder a SQL Server. Esta versión presenta una compatibilidad mejorada con las versiones anteriores de SQL Server, un instalador web independiente y notificaciones del sistema dentro de SSMS a medida que nuevas versiones estén disponibles.  

    
| ![descarga](../ssdt/media/download.png) Descarga de SQL Server Management Studio (SSMS)  |  |
|:---|:---|
|**[Descargar SQL Server Management Studio (16.5.3)](https://go.microsoft.com/fwlink/?LinkID=840946)**|Versión actual para su uso en producción.|
|**[Descargar SQL Server Management Studio: versión candidata para lanzamiento (17.0 RC3)](../ssms/sql-server-management-studio-ssms-release-candidate.md)**|Incluye compatibilidad con SQL Server vNext CTP1.3 y funciona en paralelo con 16.x, aunque no se recomienda para su uso en producción.| 


> [!NOTE]
> Las versiones de SSMS ahora se marcan numéricamente, no por mes. SSMS es gratuito. No se requiere una licencia para instalar y usar.  


## <a name="sql-server-management-studio"></a>SQL Server Management Studio   
**Información de versión**  
  
Número de versión: 16.5.3  
Número de compilación para esta versión: 13.0.16106.4
  
**Versiones de SQL Server compatibles**  
  
* Esta versión de SSMS funciona con todas las [versiones compatibles de SQL Server (SQL Server 2008 - SQL Server 2016)](https://support.microsoft.com/en-us/lifecycle?C2=1044) y proporciona el mayor nivel de compatibilidad para trabajar con las últimas características de nube en Base de datos SQL de Azure y en Almacenamiento de datos SQL de Azure.  
* No hay ningún bloqueo explícito para SQL Server 2000 o SQL Server 2005, pero es posible que algunas características no funcionen correctamente.  
* Además, se puede instalar una versión 16.x de SSMS o SSMS 2016 en paralelo con versiones anteriores de SSMS 2014 y versiones anteriores. 
  
**Sistemas operativos admitidos**  
  
Esta versión de SSMS admite las siguientes plataformas cuando se usa con el Service Pack más reciente disponible:   
 Windows 10, Windows 8, Windows 8.1, Windows 7 (SP1), Windows Server 2012 (64 bits), Windows Server 2012 R2 (64 bits), Windows Server 2008 R2 (64 bits)  
   
 **Idiomas disponibles**  
> [!NOTE]  
> Las versiones localizadas de SSMS en idiomas diferentes al inglés requieren el [paquete de actualización de seguridad KB 2862966](https://support.microsoft.com/en-us/kb/2862966) si se instalan en Windows 8, Windows 7, Windows Server 2012 y Windows Server 2008 R2. 
  
 Esta versión de SSMS puede instalarse en los idiomas siguientes:  
[Chino (República Popular China)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804) | [Chino (Taiwán)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404) | [Inglés (Estados Unidos)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409) | [Francés](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c)  
[Alemán](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407) | [Italiano](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410) | [Japonés](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411) | [Coreano](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412) | [Portugués (Brasil)](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416) | [Ruso](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419) | [Español](http://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)  

 
## <a name="changelog"></a>Registro de cambios  

16.5.3

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





Para una lista completa de características, consulte   
                [SQL Server Management Studio - Changelog (SSMS)](../ssms/sql-server-management-studio-changelog-ssms.md)  
  
Para ver la lista de problemas conocidos y soluciones alternativas, consulte   
                [SQL Server Management Studio: notas de la versión](../ssms/sql-server-management-studio-release-notes.md)  
  
Para más información sobre la colección de datos de usuario, consulte   
                [Declaración de privacidad de SQL Server](http://www.microsoft.com/privacystatement/en-us/SQLServer/Default.aspx).  
  
## <a name="previous-releases"></a>Versiones anteriores  
[Versiones anteriores de SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  
  
## <a name="feedback"></a>Comentarios  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Foro de Herramientas de cliente de SQL](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Registre un problema o una sugerencia en Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Vea también  
[Tutorial: SQL Server Management Studio](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[Documentación de SQL Server Management Studio](https://msdn.microsoft.com/library/hh213248(v=sql.130).aspx)  
[Microsoft SQL Server](https://msdn.microsoft.com/library/bb545450.aspx)  
[Service Pack y actualizaciones adicionales](https://technet.microsoft.com/sqlserver/ff803383.aspx)  
[Descargar SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)  



