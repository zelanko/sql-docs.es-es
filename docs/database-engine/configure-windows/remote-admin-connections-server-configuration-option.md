---
title: remote admin connections (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- administrator connections [SQL Server]
- DAC
- connections [SQL Server], dedicated administrator
- remote admin connections option
- dedicated administrator connections [SQL Server]
ms.assetid: bf32b60a-7a48-401f-b6be-b5e2e46c413f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fa577f1d2e995e870ab1ec3fabcd64266427dc7c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47788165"
---
# <a name="remote-admin-connections-server-configuration-option"></a>remote admin connections (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona una conexión de administrador dedicada (DAC). La conexión DAC permite a los administradores tener acceso al servidor en ejecución a fin de realizar funciones de diagnóstico o ejecutar instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] , o para solucionar problemas del servidor incluso cuando está bloqueado o se ejecuta en un estado anormal, y no responde a ninguna conexión de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . De forma predeterminada, la conexión DAC solo está disponible en un cliente del servidor. Para habilitar las aplicaciones cliente en equipos remotos de modo que usen la DAC, utilice la opción remote admin connections de sp_configure.  
  
 De forma predeterminada, la DAC solo escucha en la dirección IP de bucle invertido (127.0.0.1) a través del puerto 1434. Si el puerto TCP 1434 no está disponible, se asigna dinámicamente un puerto TCP al iniciarse [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Cuando haya más de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada en un equipo, compruebe en el registro de errores el número de puerto TCP.  
  
 En la siguiente tabla se muestran los posibles valores para la opción remote admin connections.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0|Indica que solo se permiten conexiones locales mediante la DAC.|  
|1|Indica que la DAC permite las conexiones remotas.|  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo permite utilizar una DAC desde un equipo remoto.  
  
```  
sp_configure 'remote admin connections', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Conexión de diagnóstico para administradores de bases de datos](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
  
