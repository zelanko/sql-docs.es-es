---
title: sys.dm_clr_loaded_assemblies (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_clr_loaded_assemblies
- sys.dm_clr_loaded_assemblies_TSQL
- dm_clr_loaded_assemblies_TSQL
- sys.dm_clr_loaded_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_loaded_assemblies dynamic management view
ms.assetid: 8523d8db-d8a0-4b1f-ae19-6705d633e0a6
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a5c24a05e1f33512234edafd3fb6d2672a8eee6a
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmclrloadedassemblies-transact-sql"></a>sys.dm_clr_loaded_assemblies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada ensamblado de usuario administrado cargado en el espacio de direcciones del servidor. Use esta vista para comprender y solucionar problemas de integración de CLR administra objetos de base de datos que se ejecutan en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Los ensamblados son archivos DLL que se utilizan para definir e implementar objetos de base de datos administrados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Siempre que un usuario ejecuta uno de estos objetos de base de datos administrados, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y CLR cargan el ensamblado en el que se define el objeto de base de datos administrado, así como sus referencias. El ensamblado permanece cargado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para aumentar el rendimiento, de modo que pueda llamarse en el futuro a los objetos de base de datos administrados incluidos en el ensamblado sin tener que volver a cargar el ensamblado. El ensamblado no se descarga hasta que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se encuentra bajo presión de la memoria. Para obtener más información acerca de la integración de CLR y ensamblados, vea [entorno hospedado de CLR](../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md). Para obtener más información acerca de los objetos de base de datos administrados, consulte [creación de objetos de base de datos con Common Language Runtime &#40; CLR &#41; Integración](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md).  

  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|Id. del ensamblado cargado. El **assembly_id** puede usarse para buscar más información sobre el ensamblado en el [sys.assemblies &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md) vista de catálogo. Tenga en cuenta que la [!INCLUDE[tsql](../../includes/tsql-md.md)] [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md) catálogo muestra los ensamblados de la base de datos actual. El **sqs.dm_clr_loaded_assemblies** vista muestra todos los ensamblados cargados en el servidor.|  
|**appdomain_address**|**int**|Dirección del dominio de aplicación (**AppDomain**) en que se carga el ensamblado. Todos los ensamblados que pertenecen a un solo usuario siempre se cargan en el mismo **AppDomain**. El **appdomain_address** puede utilizarse para buscar más información sobre la **AppDomain** en el [sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md) vista.|  
|**load_time**|**datetime**|Hora a la que se cargó el ensamblado. Tenga en cuenta que el ensamblado permanecerá cargado hasta que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está bajo presión de memoria y descarga el **AppDomain**. Puede supervisar **load_time** para saber con qué frecuencia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está bajo presión de memoria y descarga el **AppDomain**.|  
  
## <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="remarks"></a>Comentarios  
 El **dm_clr_loaded_assemblies.appdomain_address** vista tiene una relación de varios a uno con **dm_clr_appdomains.appdomain_address**. El **dm_clr_loaded_assemblies.assembly_id** vista tiene una relación de uno a varios con **sys.assemblies.assembly_id**.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra cómo ver información detallada de todos los ensamblados que están actualmente cargados en la base de datos activa.  
  
```  
 SELECT a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
FROM sys.dm_clr_loaded_assemblies AS l   
INNER JOIN sys.assemblies AS a  
ON l.assembly_id = a.assembly_id;  
```  
  
 En el ejemplo siguiente se muestra cómo ver los detalles de la **AppDomain** en que se carga un ensamblado determinado.  
  
```  
SELECT appdomain_id, creation_time, db_id, user_id, state  
FROM sys.dm_clr_appdomains AS a  
WHERE appdomain_address =   
(SELECT appdomain_address   
 FROM sys.dm_clr_loaded_assemblies  
 WHERE assembly_id = 555);  
```  
  
## <a name="see-also"></a>Vea también  
 [Common Language Runtime relacionadas con vistas de administración dinámica &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
