---
title: Propiedad SortColumn (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SortColumn property [RDS]
ms.assetid: f6f80f67-f0fb-4e63-a5f5-8fdf312aac63
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e11588900c963576d4fec31545b27c6fdb480ab8
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602485"
---
# <a name="sortcolumn-property-rds"></a>Propiedad SortColumn (RDS)
Indica por qué columna para ordenar los registros.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.SortColumn = String  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Una variable de objeto que representa un [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *String*  
 Un **cadena** valor que representa el nombre o alias de la columna por la que se va a ordenar los registros.  
  
## <a name="remarks"></a>Comentarios  
 El **SortColumn**, [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md), y [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md)propiedades proporcionan ordenar y filtrar la funcionalidad en la caché del lado cliente. La funcionalidad de ordenación ordena los registros por valores de una columna. La funcionalidad de filtrado muestra un subconjunto de registros basándose en criterios de búsqueda, mientras el completo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) se mantiene en la memoria caché. El [restablecer](../../../ado/reference/rds-api/reset-method-rds.md) método ejecutará los criterios y reemplazará la actual **Recordset** con actualizable **Recordset**.  
  
 Para ordenar en un **Recordset**, primero debe guardarlos cambios pendientes. Si usas el **RDS. DataControl**, puede usar el [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) método. Por ejemplo, si su **RDS. DataControl** es denomina ADC1, el código sería `ADC1.SubmitChanges`. Si está utilizando ADO **Recordset**, puede usar su [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método. Uso de **UpdateBatch** es el método recomendado para **Recordset** objetos creados con la [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) método. Por ejemplo, el código podría ser `myRS.UpdateBatch` o `ADC1.Recordset.UpdateBatch`.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [FilterColumn, FilterCriterion, FilterValue, SortColumn y propiedades SortDirection y ejemplo del método Reset (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Propiedad de ordenación](../../../ado/reference/ado-api/sort-property.md)   
 [Propiedad SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)





