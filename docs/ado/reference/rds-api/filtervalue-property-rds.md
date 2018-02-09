---
title: Propiedad FilterValue (RDS) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- FilterValue property [ADO]
ms.assetid: 28f17186-b842-4cf9-b320-a9bb941c481b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 35bba17546393a5d1339ab2c8fe8d5a8222c4396
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="filtervalue-property-rds"></a>Propiedad FilterValue (RDS)
Indica el valor con el que se va a filtrar los registros.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.FilterValue = String  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Una variable de objeto que representa un [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *String*  
 A **cadena** valor que representa un valor de datos con el que se va a filtrar registros (por ejemplo, `'Programmer'` o `125`).  
  
## <a name="remarks"></a>Comentarios  
 El [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), **FilterValue**, [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), y [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)propiedades proporcionan ordenar y filtrar la funcionalidad en la caché del cliente. La funcionalidad de ordenación ordena los registros por valores de una columna. La funcionalidad de filtrado muestra un subconjunto de registros basándose en criterios de búsqueda, mientras el completo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se mantiene en la memoria caché. El [restablecer](../../../ado/reference/rds-api/reset-method-rds.md) método ejecutará los criterios y reemplazará la actual **Recordset** con un actualizables **conjunto de registros**.  
  
 Los valores NULL producen un error de coincidencia de tipo.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn, SortDirection y propiedades ejemplo del método Reset (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Propiedad FilterColumn (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [Propiedad FilterCriterion (RDS)](../../../ado/reference/rds-api/filtercriterion-property-rds.md)   
 [Propiedad SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Propiedad SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)






















