---
title: Reduce (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Reduce_TSQL
- Reduce
dev_langs:
- TSQL
helpviewer_keywords:
- Reduce method
ms.assetid: c5dfa8c1-6764-41d8-9150-f3cb30633d3e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: db28891a7e1bed887f3a8d58a5994734d65b9185
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85705845"
---
# <a name="reduce-geography-data-type-"></a>Reduce (tipo de datos Geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Devuelve una aproximación de la instancia de **geography** especificada que se genera al aplicar el algoritmo de Douglas-Peucker a la instancia con la tolerancia indicada.  
  
 Este método del tipo de datos **geography** admite instancias de **FullGlobe** o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.Reduce ( tolerance )  
```  
  
## <a name="arguments"></a>Argumentos  
  
|||  
|-|-|  
|Término|Definición|  
|*tolerance*|Es un valor de tipo **float**. *tolerance* es la tolerancia que se usa como entrada para el algoritmo de Douglas-Peucker. *tolerance* debe ser un número positivo.|  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Observaciones  
 Para los tipos de colección, este algoritmo funciona independientemente en cada tipo **geography** contenido en la instancia. Este algoritmo no modifica las instancias de **Point**.  
  
 Este método intentará conservar los extremos de las instancias de **LineString**, pero es posible que no pueda hacerlo para mantener un resultado válido.  
  
 Si se llama a `Reduce()` con un valor negativo, este método generará una **ArgumentException**. Las tolerancias utilizadas en `Reduce()` deben ser números positivos.  
  
 El algoritmo de Douglas Peucker funciona en cada curva o anillo de la instancia de **geography** quitando todos los puntos excepto el de inicio y el final. Después, cada punto quitado se agrega de nuevo, comenzando con el punto periférico más lejano, hasta que no haya ningún punto más allá de *tolerance* del resultado. A continuación, el resultado se convierte en válido, si es necesario, cuando se garantiza un resultado válido.  
  
 En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], este método se ha extendido a las instancias de **FullGlobe**.  
  
 Este método no es preciso.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia sencilla de `LineString` y se utiliza `Reduce()` para simplificar la instancia.  
  
```  
DECLARE @g geography = 'LineString(120 45, 120.1 45.1, 199.9 45.2, 120 46)'  
SELECT @g.Reduce(10000).ToString()  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
