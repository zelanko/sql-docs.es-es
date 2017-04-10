---
title: "Propiedades de SQL Server Browser (pesta&#241;a Avanzadas) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ba79137a-cb72-4bf3-a650-e11d02cfce10
caps.latest.revision: 19
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 19
---
# Propiedades de SQL Server Browser (pesta&#241;a Avanzadas)
  El programa Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta como un servicio en el servidor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser escucha las solicitudes entrantes de recursos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y proporciona información acerca de las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas en el equipo.  
  
## Opciones  
 **Agrupado**  
 Indica si este servicio está instalado como un recurso de un servidor en clúster.  
  
 **Informes de comentarios de clientes**  
 Indica si se ha habilitado la supervisión de la calidad del servicio en este servicio. Para obtener más información acerca de los informes de comentarios de clientes, busque el tema sobre la configuración de informes de errores y uso en los Libros en pantalla.  
  
 **Volcar directorio**  
 Ubicación de los volcados de memoria si se produce un error.  
  
 **Informes de errores**  
 Cuando se establece en **Yes**, el programa Dr. Watson envía información a [!INCLUDE[msCoName](../../includes/msconame-md.md)] o a su servidor de errores si se produce un error grave. Para obtener más información acerca de Informes de errores, busque el tema sobre la configuración de informes de errores y uso en los Libros en pantalla.  
  
 **Id. de instancia**  
 Indica la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ha usado esta instancia del Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La instancia predeterminada es **MSSQL10_50.MSSQLSERVER**.  
  
## Vea también  
 [Servicio SQL Server Browser](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  