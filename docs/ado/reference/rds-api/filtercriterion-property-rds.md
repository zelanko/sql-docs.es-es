---
title: Propiedad FilterCriterion (RDS) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterCriterion property [RDS]
ms.assetid: 24eb03ba-ccfd-4353-b6af-03586b2da6fd
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6e59f14e531753bbdf4ce8ffb921424b983bbd94
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="filtercriterion-property-rds"></a>Propiedad FilterCriterion (RDS)
Indica que el operador de evaluación para usar en el valor de filtro.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Una variable de objeto que representa un [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *String*  
 A **cadena** valor que especifica el operador de evaluación de la [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md) a los registros. Puede ser cualquiera de las acciones siguientes: <, \<=, >, > =, =, o <>.  
  
## <a name="remarks"></a>Comentarios  
 El [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), **FilterCriterion**, y [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)propiedades proporcionan ordenar y filtrar la funcionalidad en la caché del cliente. La funcionalidad de ordenación ordena los registros por valores de una columna. La funcionalidad de filtrado muestra un subconjunto de registros basándose en criterios de búsqueda, mientras el completo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se mantiene en la memoria caché. El [restablecer](../../../ado/reference/rds-api/reset-method-rds.md) método ejecutará los criterios y reemplazará la actual **Recordset** con un actualizables **conjunto de registros**.  
  
 El "! =" operador no es válido para **FilterCriterion**; en su lugar, use "<>".  
  
 Si se establecen las propiedades de filtro y de ordenación y se llama a la **restablecer** método, primero se filtra el conjunto de filas y, a continuación, se ordena. Para ascendente, los valores null están en la parte superior; para descendente, los valores null son en la parte inferior (ascendente es el comportamiento predeterminado).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn, SortDirection y propiedades ejemplo del método Reset (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Propiedad FilterColumn (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [Propiedad FilterValue (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [Propiedad SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Propiedad SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


