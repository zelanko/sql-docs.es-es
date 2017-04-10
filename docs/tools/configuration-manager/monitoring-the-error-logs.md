---
title: "Supervisar los registros de errores | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "registros [SQL Server]"
  - "rendimiento de base de datos [SQL Server], errores"
  - "Windows, registros de aplicación [SQL Server]"
  - "supervisar el rendimiento [SQL Server], errores"
  - "rendimiento de servidor [SQL Server], errores"
  - "comparar los resultados del registro de errores y del registro de aplicación"
  - "errores [SQL Server], registros"
  - "optimizar bases de datos [SQL Server], errores"
  - "supervisión de base de datos [SQL Server], errores"
  - "registro de errores de SQL Server"
  - "registros [SQL Server], registros de errores de SQL Server"
  - "registros de errores [SQL Server]"
  - "registros [SQL Server], registros de aplicación de Windows"
ms.assetid: e250336b-0695-44f6-a42f-23222f94e377
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Supervisar los registros de errores
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registra ciertos eventos del sistema y definidos por el usuario en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y en el registro de aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Ambos registros marcan automáticamente el tiempo de todos los eventos registrados. Utilice la información del registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para solucionar problemas relacionados con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El registro de aplicación Windows proporciona una visión global de los eventos que tienen lugar en el sistema operativo Windows, así como de los eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Utilice el Visor de eventos de Windows para ver el registro de aplicación Windows y filtrar la información. Por ejemplo, puede filtrar eventos, como información, advertencia, error, auditoría de éxito y auditoría de error.  
  
## Comparar los resultados del registro de errores y del registro de aplicación  
 Puede utilizar tanto el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como el registro de aplicación Windows para identificar la causa de los problemas. Por ejemplo, mientras supervisa el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , puede encontrar mensajes de error que no contienen información de la causa. Se puede acotar la lista de causas probables si se comparan las fechas y horas de los eventos en ambos registros. El Visor del archivo de registros de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] permite integrar los registros de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Windows en una sola lista, facilitando así la comprensión de eventos de servidor y eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relacionados. Para obtener más información, consulte el tema "Visor del archivo de registros" en los Libros en pantalla de SQL Server.  
  
## En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Ver el registro de errores de SQL Server](../../tools/configuration-manager/viewing-the-sql-server-error-log.md)|Contiene información acerca del registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y cómo verlo.|  
|[Ver el registro de la aplicación Windows](../../tools/configuration-manager/viewing-the-windows-application-log.md)|Contiene información acerca del registro de aplicación Windows y cómo verlo.|  
  
  