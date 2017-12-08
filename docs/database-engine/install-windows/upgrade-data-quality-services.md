---
title: Actualizar Data Quality Services | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f396666b-7754-4efc-9507-0fd114cc32d5
caps.latest.revision: "12"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: bc1b70a3c4707976539d13222b088bd744e2d436
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="upgrade-data-quality-services"></a>Actualizar Data Quality Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En este tema encontrará información sobre cómo actualizar la instalación existente de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Data Quality Services (DQS). Como parte de la actualización de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Data Quality Server, debe actualizar también el esquema de bases de datos de DQS.  
  
> [!IMPORTANT]  
>  -   Debe hacer una copia de seguridad de las bases de datos de DQS antes de actualizar DQS para impedir la pérdida accidental de datos durante la actualización del esquema. Para obtener información sobre la copia de seguridad de bases de datos de DQS, vea [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
> -   Puede conectarse a [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Data Quality Server a través de la versión actual o una versión anterior de Data Quality Client o la [transformación Limpieza de DQS](../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md) de Integration Services para realizar tareas de calidad de datos.  
> -   Después de actualizar Data Quality Services y Master Data Services, ya no funcionará ninguna versión anterior del complemento Master Data Services para Excel. Puede descargar la versión [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] del complemento Master Data Services para Excel [aquí](http://go.microsoft.com/fwlink/?LinkID=506665).  
  
##  <a name="Prerequisites"></a> Requisitos previos  
  
-   Debe haber iniciado sesión como miembro del grupo Administradores en el equipo con [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
-   La cuenta de usuario de Windows debe ser miembro del rol fijo de servidor sysadmin en la instancia de SQL Server donde está instalado [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
##  <a name="Upgrade"></a> Actualizar DQS  
 Para actualizar DQS:  
  
1.  Haga una copia de seguridad de las bases de datos de DQS antes de iniciar el proceso de actualización. Para obtener información sobre la copia de seguridad de bases de datos de DQS, vea [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
  
2.  Actualice la instancia de SQL Server donde DQS esté instalado.  
  
    1.  Ejecute el Asistente para la instalación de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] .  
  
    2.  En el panel izquierdo, haga clic en **Instalación**.  
  
    3.  En el panel derecho, haga clic en **Actualizar desde...** una versión anterior de SQL Server.  
  
    4.  Complete el Asistente para la instalación.  
  
        > [!NOTE]  
        >  Esto actualizará la instancia de SQL Server a [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] y también instalará la versión más reciente de Data Quality Client, si Data Quality Client estaba instalado previamente en este equipo. Si tiene Data Quality Client instalado en otros equipos, debe ejecutar los subpasos del paso 2 en dichos equipos para instalar la versión actual de Data Quality Client. El Asistente para la instalación instala la versión actual de Data Quality Client junto con la versión existente de Data Quality Client. Después de actualizar el esquema de bases de datos de DQS, puede conectarse a la versión de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] de Data Quality Server mediante la versión actual o una versión anterior de Data Quality Client.  
  
3.  Actualice el esquema de bases de datos de DQS.  
  
    1.  Inicie Símbolo del sistema como administrador.  
  
    2.  En el símbolo del sistema, cambie el directorio a la ubicación donde DQSInstaller.exe esté disponible. El archivo DQSInstaller.exe correspondiente a la instancia predeterminada de SQL Server se encuentra en C:\Archivos de programa\Microsoft SQL Server\MSSQL[nn].MSSQLSERVER\MSSQL\Binn:  

      >[!NOTE]
      >En la ruta de acceso de carpeta, reemplace [nn] por el número de versión de [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)].
      >- Si es SQL Server 2016: 13
      >- Si es SQL Server 2017: 14

        ```  
        cd C:\Program Files\Microsoft SQL Server\MSSQL[nn].MSSQLSERVER\MSSQL\Binn  
        ```  
  
    3.  En el símbolo del sistema, escriba el siguiente comando y presione ENTRAR:  
  
        ```  
        dqsinstaller.exe -upgrade  
        ```  
  
    4.  El instalador le pregunta si desea realizar la copia de seguridad de las bases de datos DQS antes de continuar. Si aún no la ha hecho, escriba **Y** o **Yes**y presione ENTRAR para continuar con la actualización.  
  
    5.  Se muestra un mensaje para indicar que la actualización del esquema de las bases de datos DQS se realizó.  
  
##  <a name="Verify"></a> Comprobar la actualización del esquema de bases de datos de DQS  
 Para comprobar que el esquema de bases de datos de DQS se ha actualizado correctamente, puede comprobar la versión actual de las bases de datos DQS_MAIN y DQS_PROJECTS consultando la tabla A_DB_VERSION en cada base de datos. Para ello:  
  
1.  Inicie SQL Server Management Studio y conéctese a la instancia de SQL Server que contiene el esquema de bases de datos de DQS actualizado.  
  
2.  Ejecute la siguiente consulta:  
  
    ```  
    SELECT * FROM DQS_MAIN.dbo.A_DB_VERSION WHERE STATUS=2;  
    SELECT * FROM DQS_PROJECTS.dbo.A_DB_VERSION WHERE STATUS=2;  
    ```  
  
3.  La salida mostrará una entrada para cada actualización junto con la fecha de la actualización. El valor máximo de VERSION_ID y ASSEMBLY_VERSION de la fecha más reciente es la versión actual. Un valor 2 en la columna ESTADO indica que la actualización se ha realizado correctamente. Si se ha producido algún error, este aparecerá en la columna ERROR. He aquí una salida de ejemplo:  
  
    |ID|UPGRADE_DATE|VERSION_ID|ASSEMBLY_VERSION|USER_NAME|STATUS|ERROR|  
    |--------|-------------------|-----------------|-----------------------|----------------|------------|-----------|  
    |1000|2013-08-11 05:26:39.567|1200|11.0.3000.0|\<DOMINIO\nombreDeUsuario>|2||  
    |1001|2013-09-19 15:09:37.750|1600|12.0.xxxx.0|\<DOMINIO\nombreDeUsuario>|2||  
  
## <a name="see-also"></a>Vea también  
 [Instalar Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Quitar objetos del servidor de calidad de datos](../../sql-server/install/remove-data-quality-server-objects.md)   
 [Actualizar SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
  
  
