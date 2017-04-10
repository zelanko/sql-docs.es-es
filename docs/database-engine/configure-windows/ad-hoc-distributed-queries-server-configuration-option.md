---
title: "ad hoc distributed queries (opci&#243;n de configuraci&#243;n del servidor) | Microsoft Docs"
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
  - "Función OPENROWSET, opción de consultas distribuidas ad hoc"
  - "Ad Hoc Distributed Queries, opción"
  - "consultas distribuidas ad hoc"
  - "7415 (error del motor de base de datos)"
  - "Función OPENDATASOURCE, opción de consultas distribuidas ad hoc"
  - "acceso ad hoc"
ms.assetid: 5b982015-e196-44c3-83b8-275fb9d769b2
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# ad hoc distributed queries (opci&#243;n de configuraci&#243;n del servidor)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite consultas ad hoc distribuidas que utilicen OPENROWSET y OPENDATASOURCE. Cuando esta opción está establecida en 1, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite el acceso ad hoc. Si esta opción no esta establecida o está establecida en 0, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite el acceso ad hoc.  
  
 Las consultas distribuidas ad hoc utilizan las funciones OPENROWSET y OPENDATASOURCE para conectarse a los orígenes de datos remotos que utilizan OLE DB. Las funciones OPENROWSET y OPENDATASOURCE solo se deben utilizar para hacer referencia a orígenes de datos OLE DB a los que rara vez se obtiene acceso. Para los orígenes de datos cuyo acceso es más frecuente, defina un servidor vinculado.  
  
> [!IMPORTANT]  
>  Habilitar el uso de nombres ad hoc significa que cualquier inicio de sesión autenticado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede obtener acceso al proveedor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben habilitar esta característica para los proveedores a los que cualquier inicio de sesión local pueda tener acceso de forma segura.  
  
## Comentarios  
 El intento de realizar una conexión ad hoc con la opción **Ad Hoc Distributed Queries** no habilitada tiene como resultado el error: mensaje 7415, nivel 16, estado 1, línea 1  
  
 Denegado el acceso ad hoc al proveedor OLE DB 'Microsoft.ACE.OLEDB.12.0'. El acceso debe realizarse mediante un servidor vinculado.  
  
## Ejemplos  
 El ejemplo siguiente habilita las consultas distribuidas ad hoc y, a continuación, consulta un servidor denominado `Seattle1` mediante la función `OPENROWSET`.  
  
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
  
## Vea también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Servidores vinculados &#40;motor de base de datos&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)  
  
  