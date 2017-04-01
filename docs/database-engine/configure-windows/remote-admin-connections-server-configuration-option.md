---
title: "remote admin connections (opci&#243;n de configuraci&#243;n del servidor) | Microsoft Docs"
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
  - "conexiones de administrador [SQL Server]"
  - "DAC"
  - "conexiones [SQL Server], de administrador dedicadas"
  - "remote admin connections [opción]"
  - "conexiones de administrador dedicadas [SQL Server]"
ms.assetid: bf32b60a-7a48-401f-b6be-b5e2e46c413f
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# remote admin connections (opci&#243;n de configuraci&#243;n del servidor)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona una conexión de administrador dedicada (DAC). La conexión DAC permite a los administradores tener acceso al servidor en ejecución a fin de realizar funciones de diagnóstico o ejecutar instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)], o para solucionar problemas del servidor incluso cuando está bloqueado o se ejecuta en un estado anormal, y no responde a ninguna conexión de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. De forma predeterminada, la conexión DAC solo está disponible en un cliente del servidor. Para habilitar las aplicaciones cliente en equipos remotos de modo que usen la DAC, utilice la opción remote admin connections de sp_configure.  
  
 De forma predeterminada, la DAC solo escucha en la dirección IP de bucle invertido (127.0.0.1) a través del puerto 1434. Si el puerto TCP 1434 no está disponible, se asigna dinámicamente un puerto TCP al iniciarse [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Cuando haya más de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada en un equipo, compruebe en el registro de errores el número de puerto TCP.  
  
 En la siguiente tabla se muestran los posibles valores para la opción remote admin connections.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0|Indica que solo se permiten conexiones locales mediante la DAC.|  
|1|Indica que la DAC permite las conexiones remotas.|  
  
## Ejemplo  
 El siguiente ejemplo permite utilizar una DAC desde un equipo remoto.  
  
```  
sp_configure 'remote admin connections', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## Vea también  
 [Conexión de diagnóstico para administradores de bases de datos](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
  