---
title: Ejemplos de ecuaciones de filtro (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- filtering data [Reporting Services], filter equation examples
ms.assetid: 66bec93d-7c3b-4d4a-8cb6-7a7bb2f34ec6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 99ae4e35be51a96e449acbf099e7c04397457d16
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205855"
---
# <a name="filter-equation-examples-report-builder-and-ssrs"></a>Ejemplos de ecuaciones de filtro (Generador de informes y SSRS)
  Para crear un filtro, debe especificar una o varias ecuaciones de filtro. Una ecuación de filtro incluye una expresión, un tipo de datos, un operador y un valor. En este tema, se proporcionan ejemplos de filtros usados habitualmente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="filter-examples"></a>Ejemplos de filtros  
 En la tabla siguiente, se muestran ejemplos de ecuaciones de filtro que usan tipos de datos y operadores diferentes. El elemento de informe para el que se define un filtro determina el ámbito de la comparación. Por ejemplo, para un filtro definido en un conjunto de datos, **TOP % 10** es el 10 por ciento de los valores más altos del conjunto de datos; para un filtro definido en un grupo, **TOP% 10** es el 10 por ciento de los valores más altos del grupo.  
  
|Expresión simple|Tipo de datos|Operador|Valor|Descripción|  
|-----------------------|---------------|--------------|-----------|-----------------|  
|`[SUM(Quantity)]`|`Integer`|`>`|`7`|Incluye valores de datos que son mayores que 7.|  
|`[SUM(Quantity)]`|`Integer`|`TOP N`|`10`|Incluye los 10 valores de datos más altos.|  
|`[SUM(Quantity)]`|`Integer`|`TOP %`|`20`|Incluye el 20% de los valores de datos más altos.|  
|`[Sales]`|`Text`|`>`|`=CDec(100)`|Incluye todos los valores de tipo System.Decimal (tipos de datos "money" de SQL) mayores que $100.|  
|`[OrderDate]`|`DateTime`|`>`|`2008-01-01`|Incluye todas las fechas desde el 1 de enero de 2008 hasta la fecha actual.|  
|`[OrderDate]`|`DateTime`|`BETWEEN`|`2008-01-01`<br /><br /> `2008-02-01`|Incluye las fechas desde el 1 de enero de 2008 hasta el 1 de febrero de 2008, inclusive.|  
|`[Territory]`|`Text`|`LIKE`|`*east`|Todos los nombres de territorios que terminan en "east".|  
|`[Territory]`|`Text`|`LIKE`|`%o%th*`|Todos los nombres de territorios que incluyen North y South al principio del nombre.|  
|`=LEFT(Fields!Subcat.Value,1)`|`Text`|`IN`|`B, C, T`|Todos los valores de subcategoría que comienzan con las letras B, C o T.|  
  
## <a name="see-also"></a>Vea también  
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](report-parameters-report-builder-and-report-designer.md)   
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Usar expresiones en informes &#40;generador de informes y SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
