---
title: ad hoc distributed queries (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 04c2ea76808c2fa98e933021af93481c829baa21
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813488"
---
# <a name="ad-hoc-distributed-queries-server-configuration-option"></a>ad hoc distributed queries (opción de configuración del servidor)
  De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite consultas ad hoc distribuidas que utilicen OPENROWSET y OPENDATASOURCE. Cuando esta opción está establecida en 1, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite el acceso ad hoc. Si esta opción no esta establecida o está establecida en 0, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite el acceso ad hoc.  
  
 Las consultas distribuidas ad hoc utilizan las funciones OPENROWSET y OPENDATASOURCE para conectarse a los orígenes de datos remotos que utilizan OLE DB. Las funciones OPENROWSET y OPENDATASOURCE solo se deben utilizar para hacer referencia a orígenes de datos OLE DB a los que rara vez se obtiene acceso. Para los orígenes de datos cuyo acceso es más frecuente, defina un servidor vinculado.  
  
> [!IMPORTANT]  
>  Habilitar el uso de nombres ad hoc significa que cualquier inicio de sesión autenticado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede obtener acceso al proveedor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben habilitar esta característica para los proveedores a los que cualquier inicio de sesión local pueda tener acceso de forma segura.  
  
## <a name="remarks"></a>Comentarios  
 Intento de realizar una conexión ad hoc con **Ad Hoc Distributed Queries** no habilitada en los resultados de error: Mensaje 7415, nivel 16, estado 1, línea 1  
  
 Denegado el acceso ad hoc al proveedor OLE DB 'Microsoft.ACE.OLEDB.12.0'. El acceso debe realizarse mediante un servidor vinculado.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente habilita las consultas distribuidas ad hoc y, a continuación, consulta un servidor denominado `Seattle1` mediante la función `OPENROWSET` .  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
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
  
## <a name="see-also"></a>Vea también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [Servidores vinculados &#40;motor de base de datos&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](/sql/t-sql/functions/opendatasource-transact-sql)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)  
  
  
