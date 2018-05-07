---
title: sp_help_spatial_geometry_index (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_index
- sp_help_spatial_geometry_index_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_index procedure
ms.assetid: f1bcefb1-09c8-4b49-8c51-5d471065849f
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2cd47f224f3e2d225fd58094ab11e4b64e78ec90
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sphelpspatialgeometryindex-transact-sql"></a>sp_help_spatial_geometry_index (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve los nombres y valores para un conjunto específico de propiedades sobre un **geometry** índice espacial. El resultado se devuelve en un formato de tabla. Puede decidir devolver un conjunto básico de propiedades o todas las propiedades del índice.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_spatial_geometry_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput'   
     [ , [ @query_sample = ] 'query_sample']   
```  
  
## <a name="arguments"></a>Argumentos  
 Vea [procedimientos almacenan de argumentos y las propiedades del índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Vea [procedimientos almacenan de argumentos y las propiedades del índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="permissions"></a>Permissions  
 El usuario debe tener asignado un rol PUBLIC para tener acceso al procedimiento. Requiere el permiso READ ACCESS en el servidor y el objeto.  
  
## <a name="remarks"></a>Comentarios  
 Las propiedades que contienen valores NULL están incluidas en el conjunto que se devuelve.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se utiliza `sp_help_spatial_geometry_index` para investigar el índice espacial **SIndx_SpatialTable_geometry_col2** definido en la tabla **geometry_col** para el ejemplo de consulta determinado en **@qs**. En este ejemplo se devuelven solo las propiedades básicas del índice especificado.  
  
```  
declare @qs geometry  
        ='POLYGON((-90.0 -180.0, -90.0 180.0, 90.0 180.0, 90.0 -180.0, -90.0 -180.0))';  
exec sp_help_spatial_geometry_index 'geometry_col', 'SIndx_SpatialTable_geometry_col2', 0, @qs;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de índice espacial](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index_xml](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)   
 [Información general sobre los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Datos espaciales &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
