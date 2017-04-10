---
title: "clr enabled (opci&#243;n de configuraci&#243;n del servidor) | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ensamblados [integración de CLR], comprobar ejecución"
  - "clr enabled, opción"
ms.assetid: 0722d382-8fd3-4fac-b4a8-cd2b7a7e0293
caps.latest.revision: 36
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 36
---
# clr enabled (opci&#243;n de configuraci&#243;n del servidor)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Utilice la opción clr enabled para especificar si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede ejecutar ensamblados de usuario. La opción clr enabled proporciona los valores que se indican a continuación: 
  
|Value|Descripción|  
|-----------|-----------------|  
|0|Ejecución de ensamblado no permitida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|1|Ejecución de ensamblado permitida en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
Solo en WOW64. Reinicie los servidores de WOW64 para efectuar los cambios de la configuración. No se requiere el reinicio para otros tipos de servidor.  

Cuando se ejecuta RECONFIGURE y se cambia el valor de ejecución de la opción clr enabled de 1 a 0, se descargan inmediatamente todos los dominios de aplicación que incluyen ensamblados de usuario.  
  
>  **No se admite la ejecución de CLR con agrupación ligera**. Deshabilite una de las dos opciones: "clr enabled" o "lightweight pooling". Entre las características que dependen de CLR y que no funcionan correctamente en modo de fibra se encuentran el tipo de datos de **jerarquía**, la replicación y la administración basada en directivas.  
  
## Ejemplo  
 El ejemplo siguiente muestra primero la configuración actual de la opción clr enabled y después habilita la opción estableciendo su valor en 1. Para deshabilitar la opción, establezca el valor en 0.  
  
```tsql  
EXEC sp_configure 'clr enabled';  
EXEC sp_configure 'clr enabled' , '1';  
RECONFIGURE;    
```  
  
## Vea también  
 [lightweight pooling (opción de configuración del servidor)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [lightweight pooling (opción de configuración del servidor)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)  
  
  