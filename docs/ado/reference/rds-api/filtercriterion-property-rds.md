---
title: FilterCriterion (propiedad, RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- FilterCriterion property [RDS]
ms.assetid: 24eb03ba-ccfd-4353-b6af-03586b2da6fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5b14e042c7566b6b6f8559e9dc371028a509979
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964069"
---
# <a name="filtercriterion-property-rds"></a>Propiedad FilterCriterion (RDS)
Indica el operador de evaluación que se va a usar en el valor de filtro.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataControl.FilterCriterion = String  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataControl*  
 Variable de objeto que representa un objeto [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) .  
  
 *String*  
 Valor de **cadena** que especifica el operador de evaluación de [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md) en los registros. Puede ser cualquiera de los siguientes: <, \<=, >, >=, = o <>.  
  
## <a name="remarks"></a>Observaciones  
 Las propiedades [SortColumn](../../../ado/reference/rds-api/sortcolumn-property-rds.md), [SortDirection](../../../ado/reference/rds-api/sortdirection-property-rds.md), [FilterValue](../../../ado/reference/rds-api/filtervalue-property-rds.md), **FilterCriterion**y [FilterColumn](../../../ado/reference/rds-api/filtercolumn-property-rds.md) proporcionan funcionalidad de ordenación y filtrado en la memoria caché del lado cliente. La funcionalidad de ordenación ordena los registros por los valores de una columna. La funcionalidad de filtrado muestra un subconjunto de registros basados en criterios de búsqueda, mientras que el [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) completo se mantiene en la memoria caché. El método [RESET](../../../ado/reference/rds-api/reset-method-rds.md) ejecutará los criterios y reemplazará el **conjunto de registros** actual por un **conjunto de registros**actualizable.  
  
 El operador "! =" no es válido para **FilterCriterion**; en su lugar, use "<>".  
  
 Si se establecen las propiedades Filter y Sort y se llama al método **RESET** , primero se filtra el conjunto de filas y, a continuación, se ordena. En el caso de las ordenaciones ascendentes, los valores NULL se encuentran en la parte superior; en el caso de las ordenaciones descendentes, los valores NULL están en la parte inferior (el comportamiento predeterminado es ascendente).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades FilterColumn, FilterCriterion, FilterValue, SortColumn y SortDirection y el método Reset (VBScript)](../../../ado/reference/rds-api/filter-column-criterion-value-sortcolumn-sortdirection-example-vbscript.md)   
 [FilterColumn (propiedad, RDS)](../../../ado/reference/rds-api/filtercolumn-property-rds.md)   
 [Propiedad FilterValue (RDS)](../../../ado/reference/rds-api/filtervalue-property-rds.md)   
 [Propiedad SortColumn (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [Propiedad SortDirection (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)


