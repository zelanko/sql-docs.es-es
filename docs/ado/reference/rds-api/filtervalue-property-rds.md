---
title: Propiedad FilterValue (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterValue property [ADO]
ms.assetid: 28f17186-b842-4cf9-b320-a9bb941c481b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a30e3058c86c3250942238b3cd98a0cfd6e0a6de
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606805"
---
# <a name="filtervalue-property-rds"></a>Propiedad FilterValue (RDS)
Indica el valor con el que se va a filtrar los registros.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.FilterValue = String  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Una variable de objeto que representa un [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *String*  
 Un **cadena** valor que representa un valor de datos con el que se va a filtrar registros (por ejemplo, `'Programmer'` o `125`).  
  
## <a name="remarks"></a>Comentarios  
 El [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), **FilterValue**, [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), y [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)propiedades proporcionan ordenar y filtrar la funcionalidad en la caché del lado cliente. La funcionalidad de ordenación ordena los registros por valores de una columna. La funcionalidad de filtrado muestra un subconjunto de registros basándose en criterios de búsqueda, mientras el completo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se mantiene en la memoria caché. El [restablecer](../../../ado/reference/rds-api/reset-method-rds.md) método ejecutará los criterios y reemplazará la actual **Recordset** con actualizable **Recordset**.  
  
 Los valores NULL producen un error de coincidencia de tipo.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn y propiedades SortDirection y ejemplo del método Reset (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Propiedad FilterColumn (RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [Propiedad FilterCriterion (RDS)](../../../ado/reference/rds-api/filtercriterion-property-rds.md)   
 [Propiedad SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Propiedad SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)






















