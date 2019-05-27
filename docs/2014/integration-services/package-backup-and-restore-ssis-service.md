---
title: Copia de seguridad y restauración de paquetes (servicio SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, backup and restore
- backing up packages [Integration Services]
- packages [Integration Services], backup and restore
- SQL Server Integration Services packages, backup and restore
- restoring packages [Integration Services]
- Integration Services packages, backup and restore
ms.assetid: c67d3b83-a6c8-40de-920f-9236de4ac87f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b5c775393f7815084e8a79aae4be7f0974886f3e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66056930"
---
# <a name="package-backup-and-restore-ssis-service"></a>Copias de seguridad y restauración de paquetes (servicio SSIS)
    
> [!IMPORTANT]  
>  En este tema se describe el servicio de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , un servicio Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] admite el servicio para mantener la compatibilidad con versiones anteriores de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. A partir de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], puede administrar objetos como paquetes en el servidor de Integration Services.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] paquetes se pueden guardar en el sistema de archivos o en msdb, una base de datos del sistema de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Se puede crear una copia de seguridad de los paquetes guardados en msdb y restaurarlos con las características de copia de seguridad y restauración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Para más información sobre la copia de seguridad y la restauración de la base de datos msdb, haga clic en uno de los temas siguientes:  
  
-   [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye la utilidad del símbolo del sistema **dtutil** (dtutil.exec), que puede usarse para administrar paquetes. Para más información, consulte [dtutil Utility](dtutil-utility.md).  
  
## <a name="configuration-files"></a>Archivos de configuración  
 Todos los archivos de configuración incluidos en los paquetes se almacenan en el sistema de archivos. Estos archivos no se incluyen en la copia de seguridad de la base de datos msdb; por lo tanto, debe crear periódicamente una copia de seguridad de los archivos de configuración como parte del plan para proteger los paquetes guardados en msdb. Para incluir las configuraciones en la copia de seguridad de la base de datos msdb, puede usar el tipo de configuración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , en lugar de las configuraciones basadas en archivos.  
  
## <a name="packages-stored-in-the-file-system"></a>Paquetes almacenados en el sistema de archivos  
 La copia de seguridad de los paquetes guardados en el sistema de archivos debe incluirse en el plan de copia de seguridad del sistema de archivos del servidor. El archivo de configuración del servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , que tiene el nombre predeterminado MsDtsSrvr.ini.xml, contiene una lista de las carpetas del servidor que supervisa el servicio. Debe asegurarse de que se cree la copia de seguridad de estas carpetas. Además, los paquetes se pueden almacenar en otras carpetas del servidor y debe asegurarse de incluir estas carpetas en la copia de seguridad.  
  
  
