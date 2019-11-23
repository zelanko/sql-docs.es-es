---
title: sp_help_spatial_geography_index_xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_index_xml_TSQL
- sp_help_spatial_geography_index_xml
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_index_xml procedure
ms.assetid: 821d4127-3ce5-4474-8561-043404a20d81
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c2503e5d3b94b5bc73d9bf2427e0162ba2eda2fe
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304902"
---
# <a name="sp_help_spatial_geography_index_xml-transact-sql"></a>sp_help_spatial_geography_index_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve el nombre y el valor de un conjunto especificado de propiedades sobre un índice espacial de **geografía** . Puede decidir devolver un conjunto básico de propiedades o todas las propiedades del índice.  
  
 Los resultados se devuelven en un fragmento XML que muestra el nombre y valor de las propiedades seleccionadas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_spatial_geography_index_xml [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput' ]   
     [ , [ @query_sample = ] 'query_sample' ]   
     [ ,.[ @xml_output = ] 'xml_output' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 Vea [argumentos y propiedades de procedimientos almacenados de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="properties"></a>Propiedades  
 Vea [argumentos y propiedades de procedimientos almacenados de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="permissions"></a>Permisos  
 El usuario debe tener asignado un rol PUBLIC para tener acceso al procedimiento. Requiere el permiso READ ACCESS en el servidor y el objeto.  
  
## <a name="remarks"></a>Remarks  
 Las propiedades que contienen valores NULL están incluidas en el conjunto que se devuelve.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se usa `sp_help_spatial_geography_index_xml` para investigar el índice espacial **SIndx_SpatialTable_geography_col2** definido en la tabla **geography_col** para el ejemplo de consulta determinado en **\@** . En este ejemplo se devuelven las propiedades básicas del índice especificado en un fragmento XML que muestra el nombre y valor de las propiedades seleccionadas.  
  
 Después, se ejecuta una consulta [XQuery](../../xquery/xquery-basics.md) en el conjunto de resultados, que devuelve una propiedad concreta.  
  
```  
declare @qs geography  
        ='POLYGON((-90.0 -180, -90 180.0, 90 180.0, 90 -180, -90 -180.0))';  
declare @x xml;  
exec sp_help_spatial_geography_index_xml 'geography_col', 'SIndx_SpatialTable_geography_col2', 0, @qs, @x output;  
select @x.value('(/Primary_Filter_Efficiency/text())[1]', 'float');  
```  
  
 De forma similar a [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md), este procedimiento almacenado proporciona acceso mediante programación más sencillo a las propiedades de un índice espacial de **geografía** y notifica el conjunto de resultados en XML.  
  
 El rectángulo de selección de una **geografía** es toda la tierra.  
  
## <a name="requirements"></a>Requisitos  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de índice espacial](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)   
 [Información general sobre los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Datos espaciales &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [Aspectos básicos de XQuery](../../xquery/xquery-basics.md)   
 [Referencia del lenguaje de XQuery](../../xquery/xquery-language-reference-sql-server.md)  
  
  
