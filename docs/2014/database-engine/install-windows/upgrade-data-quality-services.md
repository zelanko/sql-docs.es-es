---
title: Actualizar Data Quality Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: f396666b-7754-4efc-9507-0fd114cc32d5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bfcac13965456203cbdea0fdad55fd83f8f5fae1
ms.sourcegitcommit: 87f29b23d5ab174248dab5d558830eeca2a6a0a4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2018
ms.locfileid: "51018160"
---
# <a name="upgrade-data-quality-services"></a>Actualizar Data Quality Services
  Este tema proporciona información sobre cómo actualizar la instalación existente de Data Quality Services (DQS) a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. Como parte de la actualización de Data Quality Server de DQS a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], debe actualizar también el esquema de bases de datos de DQS.  
  
> [!IMPORTANT]  
>  -   Debe hacer una copia de seguridad de las bases de datos de DQS antes de actualizar DQS para impedir la pérdida accidental de datos durante la actualización del esquema. Para obtener información sobre la copia de seguridad de bases de datos de DQS, vea [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
> -   Puede conectarse a la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de Data Quality Server a través de la versión actual o una versión anterior de Data Quality Client o la [transformación Limpieza de DQS](../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md) de Integration Services para realizar tareas de calidad de datos.  
> -   Puede continuar con la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 de servicios del complemento Master Data Services para Excel después de actualizar Quality Data Services y Master Data Services a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. Sin embargo, las versiones anteriores del complemento de Master Data Services para Excel no funcionarán después de actualizar a SQL Server 2014 CTP2. Puede descargar la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 del complemento de Master Data Services para Excel [aquí](http://go.microsoft.com/fwlink/?LinkId=328664).  
  
##  <a name="Prerequisites"></a> Requisitos previos  
  
-   Debe haber iniciado sesión como miembro del grupo Administradores en el equipo con [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
-   La cuenta de usuario de Windows debe ser miembro del rol fijo de servidor sysadmin en la instancia de SQL Server donde está instalado [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] .  
  
##  <a name="Upgrade"></a> Actualizar DQS  
 Para actualizar DQS:  
  
1.  Haga una copia de seguridad de las bases de datos de DQS antes de iniciar el proceso de actualización. Para obtener información sobre la copia de seguridad de bases de datos de DQS, vea [Backing Up and Restoring DQS Databases](../../data-quality-services/backing-up-and-restoring-dqs-databases.md).  
  
2.  Actualice a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]la instancia de SQL Server donde está instalado DQS.  
  
    1.  Ejecute el Asistente para la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
    2.  En el panel izquierdo, haga clic en **Instalación**.  
  
    3.  En el panel derecho, haga clic en **actualizar desde SQL Server 2005, SQL Server 2008, SQL Server 2008 R2 o SQL Server 2012**.  
  
    4.  Complete el Asistente para la instalación.  
  
        > [!NOTE]  
        >  Esto actualizará la instancia de SQL Server a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y también instalará la versión más reciente de Data Quality Client, si Data Quality Client estaba instalado previamente en este equipo. Si tiene Data Quality Client instalado en otros equipos, debe ejecutar los subpasos del paso 2 en dichos equipos para instalar la versión actual de Data Quality Client. El Asistente para la instalación instala la versión actual de Data Quality Client junto con la versión existente de Data Quality Client. Después de actualizar el esquema de bases de datos de DQS, puede conectarse a la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de Data Quality Server mediante la versión actual o una versión anterior de Data Quality Client.  
  
3.  Actualice el esquema de bases de datos de DQS.  
  
    1.  Inicie Símbolo del sistema como administrador.  
  
    2.  En el símbolo del sistema, cambie el directorio a la ubicación donde DQSInstaller.exe esté disponible. Para la instancia predeterminada de SQL Server, el archivo DQSInstaller.exe se encuentra en C:\Archivos de programa\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn:  
  
        ```  
        cd C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn  
        ```  
  
    3.  En el símbolo del sistema, escriba el siguiente comando y presione ENTRAR:  
  
        ```  
        dqsinstaller.exe -upgrade  
        ```  
  
    4.  El instalador le pregunta si desea realizar la copia de seguridad de las bases de datos DQS antes de continuar. Si aún no ha hecho copia de las bases de datos DQS, escriba `Y` o `Yes`, y, a continuación, presione ENTRAR para continuar con la actualización.  
  
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
  
    |Id.|UPGRADE_DATE|VERSION_ID|ASSEMBLY_VERSION|USER_NAME|STATUS|error|  
    |--------|-------------------|-----------------|-----------------------|----------------|------------|-----------|  
    |1000|2013-08-11 05:26:39.567|1200|11.0.3000.0|\<DOMINIO\nombreDeUsuario>|2||  
    |1001|2013-09-19 15:09:37.750|1600|12.0.xxxx.0|\<DOMINIO\nombreDeUsuario>|2||  
  
## <a name="see-also"></a>Vea también  
 [Instalar Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)   
 [Quitar objetos del servidor de calidad de datos](../../sql-server/install/remove-data-quality-server-objects.md)   
 [Actualizar a SQL Server 2014](upgrade-sql-server.md)  
  
  
