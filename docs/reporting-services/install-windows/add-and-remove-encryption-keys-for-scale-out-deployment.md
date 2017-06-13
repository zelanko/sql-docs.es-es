---
title: "Agregar y quitar claves de cifrado para la implementación de ampliación horizontal | Documentos de Microsoft"
ms.custom: 
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- encryption keys [Reporting Services]
- deleting encryption keys
- removing encryption keys
- adding encryption keys
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 2da86fb3-4b4d-407f-9825-74dcc42486f5
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ffe0a7ea7f46ed7b1ae5d1e5070d58afa0540b12
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="add-and-remove-encryption-keys-for-scale-out-deployment"></a>Agregar y quitar claves de cifrado para implementaciones escaladas
  Puede ejecutar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en un modelo de implementación escalada; para ello, configure varios servidores de informes para que utilicen una base de datos del servidor de informes compartida. La pertenencia a una implementación escalada se basa en si el servidor de informes almacena una clave de cifrado en la base de datos del servidor de informes. Se puede controlar la pertenencia a una implementación escalada agregando y quitando claves de cifrado para instancias de servidor de informes específicas. Si va a quitar nodos de la implementación, puede hacerlo en cualquier orden. Si va a agregar nodos, debe incluir cualquier nueva instancia de servidor de informes que forme parte de la implementación.  
  
## <a name="using-the-reporting-services-configuration-tool-to-configure-scale-out-deployment"></a>Usar la herramienta de configuración de Reporting Services para configurar una implementación escalada  
 La manera más sencilla de configurar una implementación escalada es utilizar la herramienta de configuración de Reporting Services. Para obtener más información e instrucciones paso a paso, vea [Configurar una implementación escalada horizontalmente del servidor de informes en modo nativo &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md).  
  
## <a name="using-rskeymgmt-to-configure-scale-out-deployment"></a>Usar Rskeymgmt para configurar una implementación escalada  
 Emplee la utilidad **rskeymgmt** para inicializar una instancia de servidor de informes de forma que utilice una base de datos de servidor de informes compartida. Para agregar un servidor de informes a una implementación escalada, es necesario inicializar el servidor de informes. La inicialización requiere permisos de administrador. Debe disponer de credenciales de administrador del equipo remoto que hospeda el servidor de informes que va a combinar en la implementación.  
  
### <a name="how-to-join-a-report-server-to-a-scale-out-deployment-rskeymgmt"></a>Cómo combinar un servidor de informes en una implementación escalada (rskeymgmt)  
  
1.  Ejecute **rskeymgmt.exe** localmente en el equipo que hospeda un servidor de informes que ya pertenece a la implementación escalada del servidor de informes.  
  
2.  Use el argumento **-j** para unir un servidor de informes a la base de datos del servidor de informes. Use la **-m** y  **-n**  argumentos para especificar el servidor de informes remoto instancia que desea agregar a la implementación. Use los argumentos **-u** y **-v** para especificar una cuenta de administrador en el equipo remoto. Si va a crear una implementación escalada utilizando varias instancias de servidor de informes en el mismo equipo, la sintaxis cambiará ligeramente. Para obtener más información sobre la sintaxis que debe usar, vea [rskeymgmt (utilidad) &#40;SSRS&#41;](../../reporting-services/tools/rskeymgmt-utility-ssrs.md).  
  
     El siguiente ejemplo muestra los argumentos que debe especificar si va a incluir un servidor de informes remoto en una implementación escalada (si tiene permisos de administrador en el equipo remoto, puede omitir las credenciales):  
  
    ```  
    rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
    ```
3. Reinicie el servicio Reporting Services de Windows.
  
### <a name="how-to-remove-a-report-server-from-a-scale-out-deployment-rskeymgmt"></a>Cómo quitar un servidor de informes de una implementación escalada (rskeymgmt)  
  
1.  Abra el archivo rsreportserver.config del servidor de informes que desea quitar y busque el identificador de instalación. De forma predeterminada, este archivo se encuentra en archivos de programa\Microsoft SQL Server\MSSQL.  *n* \Reporting).  
  
     Si ha instalado una única instancia, solo habrá un archivo rsreportserver.config en el equipo. Si ha instalado varias instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , utilice la página Estado del servidor de la herramienta de configuración de Reporting Services para buscar el identificador de instancia (p. ej., MSSQL.2) para el servidor de informes que desea quitar. El nombre de la carpeta que almacena los archivos de programa para la instancia de servidor de informes se basará en el identificador de la instancia (p. ej., Archivos de programa\Microsoft SQL Server\MSSQL.2).  
  
2.  Ejecute **rskeymgmt.exe**. Puede hacerlo en cualquier servidor de informes que forme parte de la implementación escalada de servidores de informes.  
  
3.  Use el argumento **-r** para liberar la instancia de servidor de informes de la implementación escalada. El siguiente ejemplo ilustra los argumentos que debe especificar:  
  
    ```  
    rskeymgmt -r <installation ID>  
    ```  
4. Reinicie el servicio Reporting Services de Windows.
  
 En estos pasos se explica cómo quitar el servidor de informes de una implementación escalada, pero con ellos no se desinstala la instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] del servidor de informes. Después de quitar el servidor de informes de la implementación escalada, puede desinstalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] del servidor si ya no necesita [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en ese servidor. Para obtener información, vea [Desinstalar una instancia existente de SQL Server &#40;programa de instalación&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md) en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)  
  
  

