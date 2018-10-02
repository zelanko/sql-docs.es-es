---
title: ad hoc distributed queries (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- OPENROWSET function, ad hoc distributed queries option
- Ad Hoc Distributed Queries option
- ad hoc distributed queries
- 7415 (Database Engine Error)
- OPENDATASOURCE function, ad hoc distributed queries option
- ad hoc access
ms.assetid: 5b982015-e196-44c3-83b8-275fb9d769b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ddef6de92c0bb5329e84011f9996368ef6b452dc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47690154"
---
# <a name="ad-hoc-distributed-queries-server-configuration-option"></a>ad hoc distributed queries (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite consultas ad hoc distribuidas que utilicen OPENROWSET y OPENDATASOURCE. Cuando esta opción está establecida en 1, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite el acceso ad hoc. Si esta opción no esta establecida o está establecida en 0, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite el acceso ad hoc.  
  
 Las consultas distribuidas ad hoc utilizan las funciones OPENROWSET y OPENDATASOURCE para conectarse a los orígenes de datos remotos que utilizan OLE DB. Las funciones OPENROWSET y OPENDATASOURCE solo se deben utilizar para hacer referencia a orígenes de datos OLE DB a los que rara vez se obtiene acceso. Para los orígenes de datos cuyo acceso es más frecuente, defina un servidor vinculado.  
  
> [!IMPORTANT]  
>  Habilitar el uso de nombres ad hoc significa que cualquier inicio de sesión autenticado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede obtener acceso al proveedor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben habilitar esta característica para los proveedores a los que cualquier inicio de sesión local pueda tener acceso de forma segura.  
  
## <a name="remarks"></a>Notas  
 El intento de realizar una conexión ad hoc con la opción **Ad Hoc Distributed Queries** no habilitada tiene como resultado el error: mensaje 7415, nivel 16, estado 1, línea 1  
  
 Denegado el acceso ad hoc al proveedor OLE DB 'Microsoft.ACE.OLEDB.12.0'. El acceso debe realizarse mediante un servidor vinculado.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente habilita las consultas distribuidas ad hoc y, a continuación, consulta un servidor denominado `Seattle1` mediante la función `OPENROWSET` .  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;
GO 
sp_configure 'Ad Hoc Distributed Queries', 1;  
RECONFIGURE;  
GO  
  
SELECT a.*  
FROM OPENROWSET('SQLNCLI', 'Server=Seattle1;Trusted_Connection=yes;',  
     'SELECT GroupName, Name, DepartmentID  
      FROM AdventureWorks2012.HumanResources.Department  
      ORDER BY GroupName, Name') AS a;  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Servidores vinculados &#40;motor de base de datos&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
  
