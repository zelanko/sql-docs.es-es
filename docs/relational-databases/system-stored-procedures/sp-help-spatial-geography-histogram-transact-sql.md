---
title: sp_help_spatial_geography_histogram (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_histogram_TSQL
- sp_help_spatial_geography_histogram
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_histogram
ms.assetid: 5c5bd319-055d-4cd6-8c5a-06354cc056cc
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: a6fa55cd5359c64f2a124ff85429745c995fae96
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538167"
---
# <a name="sphelpspatialgeographyhistogram-transact-sql"></a>sp_help_spatial_geography_histogram (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Facilita la escritura de parámetros de cuadrícula para un índice espacial.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_spatial_geography_histogram [ @tabname =] 'tabname'   
     [ , [ @colname = ] 'columnname' ]   
     [ , [ @resolution = ] 'resolution' ]  
     [ , [ @sample = ] 'tablesample' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @tabname = ] 'tabname'` Es el nombre completo o incompleto de la tabla para la que se ha especificado el índice espacial.  
  
 Se requieren comillas únicamente si se especifica una tabla certificada. Si se proporciona un nombre completo, incluido el nombre de la base de datos, el nombre de la base de datos debe ser el de la base de datos actual. *TabName* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @colname = ] 'columnname'` Es el nombre de la columna espacial especificada. *ColumnName* es un **sysname**, no tiene ningún valor predeterminado.  
  
`[ @resolution = ] 'resolution'` Es la resolución del cuadro de límite. Los valores válidos van del 10 al 5000. *resolución* es un **tinyint**, no tiene ningún valor predeterminado.  
  
`[ @sample = ] 'sample'` Es el porcentaje de la tabla que se utiliza. Los valores válidos son de 0 a 100. *TABLESAMPLE* es un **float**. Valor predeterminado es 100.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad y valor devuelto  
 Se devuelve un valor de tabla. En la siguiente cuadrícula se describe el contenido de la columna de la tabla.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**cellid**|**int**|Representa el identificador único de cada celda, con el contador inicial igual a 1.|  
|**cell**|**geography**|Es un polígono rectangular que representa cada celda. La forma de la celda es idéntica a la de la celda usada para los índices espaciales.|  
|**row_count**|**bigint**|Indica el número de objetos espaciales que tocan la celda o que están contenidos en ella.|  
  
## <a name="permissions"></a>Permisos  
 Usuario debe ser un miembro de la **pública** rol. Requiere el permiso READ ACCESS en el servidor y el objeto.  
  
## <a name="remarks"></a>Comentarios  
 La pestaña Resultados espaciales de SSMS muestra una representación gráfica de los resultados. Puede consultar los resultados en la ventana espacial para obtener un número aproximado de elementos de resultados.  
  
> [!NOTE]  
>  Los objetos de la tabla pueden ocupar más de una celda. Por tanto, la suma de las celdas de la tabla puede ser mayor que el número de objetos reales.  
  
 El cuadro de límite para el **geography** tipo es todo el mundo.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente se llama **sp_help_spatial_geography_histogram** en el `Person.Address` tabla el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos.  
  
```  
EXEC sp_help_spatial_geography_histogram @tabname = Person.Address, @colname = SpatialLocation, @resolution = 64, @sample = 30;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados de índice espacial &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)  
  
  
