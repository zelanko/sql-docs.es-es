---
title: Ejemplos de ecuaciones de filtro (Generador de informes) | Microsoft Docs
description: Obtenga información sobre cómo crear un filtro de informe. Tenga en cuenta estos ejemplos de filtros usados con frecuencia para crear los suyos propios.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
helpviewer_keywords:
- filtering data [Reporting Services], filter equation examples
ms.assetid: 66bec93d-7c3b-4d4a-8cb6-7a7bb2f34ec6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 074a7d7b300d9ae55776199479b229407b2ba3a1
ms.sourcegitcommit: 5b7457c9d5302f84cc3baeaedeb515e8e69a8616
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2020
ms.locfileid: "83689741"
---
# <a name="filter-equation-examples-report-builder-and-ssrs"></a>Ejemplos de ecuaciones de filtro (Generador de informes y SSRS)
  Para crear un filtro, debe especificar una o varias ecuaciones de filtro. Una ecuación de filtro incluye una expresión, un tipo de datos, un operador y un valor. En este tema, se proporcionan ejemplos de filtros usados habitualmente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="filter-examples"></a>Ejemplos de filtros  
 En la tabla siguiente, se muestran ejemplos de ecuaciones de filtro que usan tipos de datos y operadores diferentes. El elemento de informe para el que se define un filtro determina el ámbito de la comparación. Por ejemplo, para un filtro definido en un conjunto de datos, **TOP % 10** es el 10 por ciento de los valores más altos del conjunto de datos; para un filtro definido en un grupo, **TOP% 10** es el 10 por ciento de los valores más altos del grupo.  
  
|Expresión simple|Tipo de datos|Operator|Value|Descripción|  
|-----------------------|---------------|--------------|-----------|-----------------|  
|`[SUM(Quantity)]`|**Entero**|**>**|`7`|Incluye valores de datos que son mayores que 7.|  
|`[SUM(Quantity)]`|**Entero**|**TOP N**|`10`|Incluye los 10 valores de datos más altos.|  
|`[SUM(Quantity)]`|**Entero**|**TOP %**|`20`|Incluye el 20% de los valores de datos más altos.|  
|`[Sales]`|**Texto**|**>**|`=CDec(100)`|Incluye todos los valores de tipo System.Decimal (tipos de datos "money" de SQL) mayores que $100.|  
|`[OrderDate]`|**DateTime**|**>**|`2008-01-01`|Incluye todas las fechas desde el 1 de enero de 2008 hasta la fecha actual.|  
|`[OrderDate]`|**DateTime**|**BETWEEN**|`2008-01-01`<br /><br /> `2008-02-01`|Incluye las fechas desde el 1 de enero de 2008 hasta el 1 de febrero de 2008, inclusive.|  
|`[Territory]`|**Texto**|**LIKE**|`*east`|Todos los nombres de territorios que terminan en "east".|  
|`[Territory]`|**Texto**|**LIKE**|`%o%th*`|Todos los nombres de territorios que incluyen North y South al principio del nombre.|  
|`=LEFT(Fields!Subcat.Value,1)`|**Texto**|**IN**|`B, C, T`|Todos los valores de subcategoría que comienzan con las letras B, C o T.|  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
