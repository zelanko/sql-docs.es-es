---
description: Propiedad SortColumn (RDS)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9e8ae929c5606de2a0f58981affb403948e81b4b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438637"
---
# <a name="sortcolumn-property-rds"></a>Propiedad SortColumn (RDS)
Indica la columna por la que se ordenarán los registros.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.SortColumn = String  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Variable de objeto que representa un objeto [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
 *String*  
 Valor de **cadena** que representa el nombre o el alias de la columna por la que se van a ordenar los registros.  
  
## <a name="remarks"></a>Observaciones  
 Las propiedades **SortColumn**, [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), [FilterCriterion](../../../ado/reference/rds-api/filtercriterion-property-rds.md)y [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md) proporcionan funcionalidad de ordenación y filtrado en la memoria caché del lado cliente. La funcionalidad de ordenación ordena los registros por los valores de una columna. La funcionalidad de filtrado muestra un subconjunto de registros basados en criterios de búsqueda, mientras que el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) completo se mantiene en la memoria caché. El método [RESET](../../../ado/reference/rds-api/reset-method-rds.md) ejecutará los criterios y reemplazará el **conjunto de registros** actual por un **conjunto de registros**actualizable.  
  
 Para ordenar por un **conjunto de registros**, primero debe guardar los cambios pendientes. Si utiliza **RDS. DataControl**, puede utilizar el método [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) . Por ejemplo, si el **objeto RDS. DataControl** se denomina ADC1, el código sería `ADC1.SubmitChanges` . Si está utilizando un conjunto de **registros**ADO, puede utilizar su método [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) . El uso de **UpdateBatch** es el método recomendado para los objetos de **conjunto de registros** creados con el método [CreateRecordset](../../../ado/reference/rds-api/createrecordset-method-rds.md) . Por ejemplo, el código podría ser `myRS.UpdateBatch` o `ADC1.Recordset.UpdateBatch` .  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades FilterColumn, FilterCriterion, FilterValue, SortColumn y SortDirection y el método Reset (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [Propiedad Sort](../../../ado/reference/ado-api/sort-property.md)   
 [Propiedad SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)





