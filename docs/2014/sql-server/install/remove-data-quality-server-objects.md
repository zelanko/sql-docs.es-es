---
title: Quitar objetos del servidor de calidad de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 1b7c6dbb-b40e-4822-9caa-608e1056af8e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2a90b7c7aac9ad7f5f0398951e1d4e39ae810a8e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134132"
---
# <a name="remove-data-quality-server-objects"></a>Quitar objetos del servidor de calidad de datos
  La desinstalación de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o la eliminación completa de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tiene [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] no elimina algunos objetos de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] , incluidas las bases de datos de DQS. Esto implica que no pierde los datos de DQS si desinstala el [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] mediante el programa de instalación de SQL Server. Debe eliminar manualmente estos objetos de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] después de completarse el proceso de desinstalación.  
  
> [!NOTE]  
>  -   Antes de desinstalar [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], considere la posibilidad de realizar una copia de seguridad de todas las bases de conocimientos mediante su exportación a un archivo .dqsb y use dicho archivo posteriormente para importar todas las bases de conocimientos a una nueva instalación de [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] . La exportación e importación de todas las bases de conocimientos de DQS solo se puede realizar mediante la ejecución de DQSInstaller.exe con los parámetros de línea de comandos adecuados desde el símbolo del sistema. Para más información, consulte [Export and Import DQS Knowledge Bases Using DQSInstaller.exe](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md).  
> -   Antes de eliminar las bases de datos de DQS, considere la posibilidad de hacer copias de seguridad de las bases de datos si desea mantenerlas y usarlas posteriormente para restaurar los datos. Para obtener más información sobre cómo hacerlo, vea [Administrar bases de datos de DQS](../../../2014/data-quality-services/manage-dqs-databases.md).  
  
## <a name="uninstall-data-quality-server-from-a-sql-server-instance"></a>Desinstalar el Servidor de calidad de datos de una instancia de SQL Server  
 Si acaba de desinstalar el [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe eliminar manualmente los siguientes objetos del [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] una vez completado el proceso de desinstalación del [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] :  
  
-   Bases de datos DQS_MAIN, DQS_PROJECTS y DQS_STAGING_DATA.  
  
-   \#Los inicios de sesión #MS_dqs_db_owner_login## y ##MS_dqs_service_login##.  
  
-   El procedimiento almacenado DQInitDQS_MAIN de la base de datos maestra.  
  
 Para eliminar estos objetos en SQL Server Management Studio, haga clic con el botón derecho en el objeto y haga clic en **Eliminar** en el menú contextual.  
  
> [!IMPORTANT]  
>  Si acaba de desinstalar el [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] desde una instancia de SQL Server mediante el parámetro de la línea de comandos `–uninstall` en el símbolo del sistema, todos los objetos de DQS se eliminarán como parte del proceso de desinstalación. No es necesario eliminarlos manualmente después de desinstalar el [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]. Para desinstalar [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] desde el símbolo del sistema, escriba el siguiente comando en el símbolo del sistema y presione ENTRAR:   
> `dqsinstaller.exe -uninstall`  
  
## <a name="uninstall-sql-server-instance-containing-data-quality-server"></a>Desinstalar la instancia de SQL Server que contiene el Servidor de calidad de datos  
 Si va a desinstalar por completo la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tiene el [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)], debe eliminar manualmente las bases de datos DQS_MAIN, DQS_PROJECTS y DQS_STAGING_DATA del equipo una vez completado el proceso de desinstalación. En el caso de una instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predeterminada, los archivos de las bases de datos DQS_MAIN, DQS_PROJECTS y DQS_STAGING_DATA están disponibles en C:\Archivos de programa\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA.  
  
## <a name="see-also"></a>Vea también  
 [Desinstalar una instancia existente de SQL Server &#40;programa de instalación&#41;](../../../2014/sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)   
 [Desinstalar SQL Server 2014](uninstall-sql-server.md)  
  
  
