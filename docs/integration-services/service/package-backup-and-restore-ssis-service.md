---
title: "Copias de seguridad y restauraci&#243;n de paquetes (servicio SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Paquetes de SSIS, copia de seguridad y restauración"
  - "copia de seguridad de los paquetes [Integration Services]"
  - "paquetes [Integration Services], copia de seguridad y restauración"
  - "Paquetes de SQL Server Integration Services, copia de seguridad y restauración"
  - "restaurar paquetes [Integration Services]"
  - "Paquetes de Integration Services, copia de seguridad y restauración"
ms.assetid: c67d3b83-a6c8-40de-920f-9236de4ac87f
caps.latest.revision: 44
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 44
---
# Copias de seguridad y restauraci&#243;n de paquetes (servicio SSIS)
    
> [!IMPORTANT]  
>  En este tema se describe el servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , un servicio Windows para administrar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] admite el servicio para mantener la compatibilidad con versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], puede administrar objetos como paquetes en el servidor de Integration Services.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquetes se pueden guardar en el sistema de archivos o en msdb, una base de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se puede crear una copia de seguridad de los paquetes guardados en msdb y restaurarlos con las características de copia de seguridad y restauración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para más información sobre la copia de seguridad y la restauración de la base de datos msdb, haga clic en uno de los temas siguientes:  
  
-   [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
-   [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye la utilidad del símbolo del sistema **dtutil** (dtutil.exec), que puede usarse para administrar paquetes. Para más información, consulte [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
## Archivos de configuración  
 Todos los archivos de configuración incluidos en los paquetes se almacenan en el sistema de archivos. Estos archivos no se incluyen en la copia de seguridad de la base de datos msdb; por lo tanto, debe crear periódicamente una copia de seguridad de los archivos de configuración como parte del plan para proteger los paquetes guardados en msdb. Para incluir las configuraciones en la copia de seguridad de la base de datos msdb, puede usar el tipo de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en lugar de las configuraciones basadas en archivos.  
  
## Paquetes almacenados en el sistema de archivos  
 La copia de seguridad de los paquetes guardados en el sistema de archivos debe incluirse en el plan de copia de seguridad del sistema de archivos del servidor. El archivo de configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , que tiene el nombre predeterminado MsDtsSrvr.ini.xml, contiene una lista de las carpetas del servidor que supervisa el servicio. Debe asegurarse de que se cree la copia de seguridad de estas carpetas. Además, los paquetes se pueden almacenar en otras carpetas del servidor y debe asegurarse de incluir estas carpetas en la copia de seguridad.  
  
  