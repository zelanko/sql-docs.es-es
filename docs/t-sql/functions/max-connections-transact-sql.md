---
title: '@@MAX_CONNECTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@MAX_CONNECTIONS'
- '@@MAX_CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- simultaneous connections [SQL Server]
- maximum number of simultaneous user connections
- '@@MAX_CONNECTIONS function'
- connections [SQL Server], simultaneous
- number of simultaneous user connections
ms.assetid: 57eb9f4b-548f-4212-9684-a11d831c4732
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: de4460e3f5dbc0ff2aba83f4c3794528f9100a2e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40maxconnections-transact-sql"></a>&#x40;&#x40;MAX_CONNECTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el número máximo de conexiones de usuario simultáneas que se permiten en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El número devuelto no es necesariamente el número configurado actualmente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
@@MAX_CONNECTIONS  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **integer**  
  
## <a name="remarks"></a>Notas  
 El número real de conexiones de usuario permitidas depende también de la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está instalada y de los límites de las aplicaciones y del hardware.  
  
 Para volver a configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de modo que admita menos conexiones, use **sp_configure**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo devolver el número máximo de conexiones de usuario simultáneas en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En el ejemplo se considera que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se ha configurado de nuevo para utilizar menos conexiones de usuario.  
  
```  
SELECT @@MAX_CONNECTIONS AS 'Max Connections';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Max Connections  
---------------  
32767            
```  
  
## <a name="see-also"></a>Ver también  
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Funciones de configuración](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Establecer la opción de configuración del servidor Conexiones de usuario](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
  
  
