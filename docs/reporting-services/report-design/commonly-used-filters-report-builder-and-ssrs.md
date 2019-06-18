---
title: Filtros de uso frecuente (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- multivalued parameters [Reporting Services]
- single-valued parameters [Reporting Services]
- parameters [Reporting Services], multivalued
- valid values [Reporting Services]
ms.assetid: cb70d0cd-707b-4de5-b39f-e4eb57d316aa
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0757982d8e1e758a771d7ccdf880c88576f980f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581591"
---
# <a name="commonly-used-filters-report-builder-and-ssrs"></a>Filtros de uso frecuente (Generador de informes y SSRS)
  Para crear un filtro, debe especificar una o varias ecuaciones de filtro. Una ecuación de filtro incluye una expresión, un tipo de datos, un operador y un valor. En este tema, se proporcionan ejemplos de filtros usados habitualmente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="filter-examples"></a>Ejemplos de filtros  
 En la tabla siguiente, se muestran ejemplos de ecuaciones de filtro que usan tipos de datos y operadores diferentes. El elemento de informe para el que se define un filtro determina el ámbito de la comparación. Por ejemplo, para un filtro definido en un conjunto de datos, **TOP % 10** es el 10 por ciento de los valores más altos del conjunto de datos; para un filtro definido en un grupo, **TOP% 10** es el 10 por ciento de los valores más altos del grupo.  
  
|Expresión simple|Tipo de datos|Operador|Valor|Descripción|  
|-----------------------|---------------|--------------|-----------|-----------------|  
|`[SUM(Quantity)]`|**Integer**|**>**|`7`|Incluye valores de datos que son mayores que 7.|  
|`[SUM(Quantity)]`|**Integer**|**TOP N**|`10`|Incluye los 10 valores de datos más altos.|  
|`[SUM(Quantity)]`|**Integer**|**TOP %**|`20`|Incluye el 20% de los valores de datos más altos.|  
|`[Sales]`|**Texto**|**>**|`=CDec(100)`|Incluye todos los valores de tipo System.Decimal (tipos de datos "money" de SQL) mayores que $100.|  
|`[OrderDate]`|**DateTime**|**>**|`2088-01-01`|Incluye todas las fechas desde el 1 de enero de 2008 hasta la fecha actual.|  
|`[OrderDate]`|**DateTime**|**BETWEEN**|`2008-01-01`<br /><br /> `2008-02-01`|Incluye las fechas desde el 1 de enero de 2008 hasta el 1 de febrero de 2008, inclusive.|  
|`[Territory]`|**Texto**|**LIKE**|`*east`|Todos los nombres de territorios que terminan en "east".|  
|`[Territory]`|**Texto**|**LIKE**|`%o%th*`|Todos los nombres de territorios que incluyen North y South al principio del nombre.|  
|`=LEFT(Fields!Subcat.Value,1)`|**Texto**|**IN**|`B, C, T`|Todos los valores de subcategoría que comienzan con las letras B, C o T.|  
  
## <a name="examples-with-report-parameters"></a>Ejemplos con parámetros de informe  
 En la tabla siguiente, se proporcionan ejemplos de expresiones de filtro que incluyen una referencia a un parámetro con un solo valor o con varios valores.  
  
|Tipo de parámetro|Expresión (Filtro)|Operador|Valor|Tipo de datos|  
|--------------------|---------------------------|--------------|-----------|---------------|  
|Un solo valor|`[EmployeeID]`|=|`[@EmployeeID]`|Integer|  
|Varios valores|`[EmployeeID]`|IN|`[@EmployeeID]`|Integer|  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)  
  
  
