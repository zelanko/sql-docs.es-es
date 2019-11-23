---
title: sp_help_spatial_geometry_index_xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_index_xml_TSQL
- sp_help_spatial_geometry_index_xml
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_index_xml procedure
ms.assetid: 9668ae6d-9ed5-418e-bb9a-9e7b66f7dd16
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9e7eb2e007191088a0259360924b2f5f931dec0a
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304898"
---
# <a name="sp_help_spatial_geometry_index_xml-transact-sql"></a>sp_help_spatial_geometry_index_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve los nombres y valores para un conjunto especificado de propiedades sobre un índice espacial de **geometría** . Puede decidir devolver un conjunto básico de propiedades o todas las propiedades del índice.  
  
 Los resultados se devuelven en un fragmento XML que muestra el nombre y valor de las propiedades seleccionadas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_spatial_geometry_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ]'{ 0 | 1 }]   
     [ , [ @query_sample = ] 'query_sample' ]   
     [ ,.[ @xml_output = ] 'xml_output' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 Vea [argumentos y propiedades de procedimientos almacenados de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="properties"></a>Propiedades  
 Vea [argumentos y propiedades de procedimientos almacenados de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="permissions"></a>Permisos  
 El usuario debe ser miembro del rol **Public** . Requiere el permiso READ ACCESS en el servidor y el objeto.  
  
## <a name="remarks"></a>Remarks  
 Las propiedades que contienen valores NULL están incluidas en el conjunto XML que se devuelve.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa `sp_help_spatial_geometry_index_xml` para investigar el índice espacial **SIndx_SpatialTable_geometry_col2** definido en la tabla **geometry_col** para el ejemplo de consulta determinado en **\@** . En este ejemplo se devuelven las propiedades básicas del índice especificado en un fragmento XML que muestra el nombre y valor de las propiedades seleccionadas.  
  
 Después, se ejecuta una consulta [XQuery](../../xquery/xquery-basics.md) en el conjunto de resultados, que devuelve una propiedad concreta.  
  
```  
DECLARE @qs geometry  
        ='POLYGON((-90.0 -180.0, -90.0 180.0, 90.0 180.0, 90.0 -180.0, -90.0 -180.0))';  
DECLARE @x xml;  
EXEC sp_help_spatial_geometry_index_xml 'geometry_col', 'SIndx_SpatialTable_geometry_col2', 0, @qs, @x output;  
SELECT @x.value('(/Primary_Filter_Efficiency/text())[1]', 'float');  
```  
  
 De forma similar a [sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md), este procedimiento almacenado proporciona acceso mediante programación más sencillo a las propiedades de un índice espacial y notifica el conjunto de resultados en XML.  
  
## <a name="requirements"></a>Requisitos  
  
## <a name="see-also"></a>Vea también  
 [Argumentos y propiedades de los procedimientos almacenados de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)   
 [Procedimientos almacenados de índice espacial](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [Información general sobre los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Datos espaciales &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [Aspectos básicos de XQuery](../../xquery/xquery-basics.md)   
 [Referencia del lenguaje de XQuery](../../xquery/xquery-language-reference-sql-server.md)  
  
  
