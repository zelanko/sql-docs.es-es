---
title: Propiedad SortDirection (RDS) | Documentos de Microsoft
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: SortDirection property [RDS]
ms.assetid: 1d9d8715-e4ad-4ff3-bf7f-f1dc0532d8c2
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4e2bc3372e360debd15fa33b6badd4bd6bdc61fa
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="sortdirection-property-rds"></a>Propiedad SortDirection (RDS)
Indica si un criterio de ordenación es ascendente o descendente.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.SortDirection = value  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Una variable de objeto que representa un [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *Value*  
 A **booleano** valor que, cuando se establece en **True**, indica la dirección de ordenación es ascendente. **False** indica un orden descendente.  
  
## <a name="remarks"></a>Comentarios  
 El [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), **SortDirection**, [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), y [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)propiedades proporcionan ordenar y filtrar la funcionalidad en la caché del cliente. La funcionalidad de ordenación ordena los registros mediante el uso de valores de una columna. La funcionalidad de filtrado muestra un subconjunto de registros basándose en criterios de búsqueda, mientras el completo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se mantiene en la memoria caché. El [restablecer](../../../ado/reference/rds-api/reset-method-rds.md) método ejecutará los criterios y reemplazará la actual **Recordset** con un actualizables **conjunto de registros**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn, SortDirection y propiedades ejemplo del método Reset (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Propiedad de ordenación](../../../ado/reference/ado-api/sort-property.md)   
 [Propiedad SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)


