---
title: sp_help_spatial_geography_index_xml (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_index_xml_TSQL
- sp_help_spatial_geography_index_xml
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_index_xml procedure
ms.assetid: 821d4127-3ce5-4474-8561-043404a20d81
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eba6e9c6fe0d979d9e07a7023d1746a1e0cfb2cd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpspatialgeographyindexxml-transact-sql"></a>sp_help_spatial_geography_index_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve el nombre y valor para un conjunto específico de propiedades sobre un **geography** índice espacial. Puede decidir devolver un conjunto básico de propiedades o todas las propiedades del índice.  
  
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
 Vea [procedimientos almacenan de argumentos y las propiedades del índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="properties"></a>Propiedades  
 Vea [procedimientos almacenan de argumentos y las propiedades del índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="permissions"></a>Permissions  
 El usuario debe tener asignado un rol PUBLIC para tener acceso al procedimiento. Requiere el permiso READ ACCESS en el servidor y el objeto.  
  
## <a name="remarks"></a>Comentarios  
 Las propiedades que contienen valores NULL están incluidas en el conjunto que se devuelve.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se utiliza `sp_help_spatial_geography_index_xml` para investigar el índice espacial **SIndx_SpatialTable_geography_col2** definido en la tabla **geography_col** para el ejemplo de consulta determinado en  **@qs**. En este ejemplo se devuelven las propiedades básicas del índice especificado en un fragmento XML que muestra el nombre y valor de las propiedades seleccionadas.  
  
 Un [XQuery](../../xquery/xquery-basics.md) , a continuación, se ejecuta en el conjunto de resultados, devolver una propiedad concreta.  
  
```  
declare @qs geography  
        ='POLYGON((-90.0 -180, -90 180.0, 90 180.0, 90 -180, -90 -180.0))';  
declare @x xml;  
exec sp_help_spatial_geography_index_xml 'geography_col', 'SIndx_SpatialTable_geography_col2', 0, @qs, @x output;  
select @x.value('(/Primary_Filter_Efficiency/text())[1]', 'float');  
```  
  
 Similar a [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md), este procedimiento almacenado proporciona acceso mediante programación más sencillo a las propiedades de un **geography** índice espacial y notifica el conjunto de resultados en XML.  
  
 El cuadro de límite de un **geography** es toda la tierra.  
  
## <a name="requirements"></a>Requisitos  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de índice espacial](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)   
 [Información general sobre los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Datos espaciales &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [Conceptos básicos de XQuery](../../xquery/xquery-basics.md)   
 [Referencia del lenguaje de XQuery](../../xquery/xquery-language-reference-sql-server.md)  
  
  
