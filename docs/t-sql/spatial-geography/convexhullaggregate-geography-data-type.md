---
title: ConvexHullAggregate (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ConvexHullAggregate_TSQL
- ConvexHullAggregate
dev_langs:
- TSQL
helpviewer_keywords:
- ConvexHullAggregate method (geography)
ms.assetid: 21784c66-2725-471b-9e2d-a8c2e3695197
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5a2f112e58838c754b946bdf3870fea31125a813
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="convexhullaggregate-geography-data-type"></a>ConvexHullAggregate (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve una forma convexa para un conjunto determinado de **geography** objetos.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ConvexHullAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography_operand*  
 Es un **geography** columna de tabla de tipo que representa un conjunto de **geography** objetos.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
## <a name="exception"></a>Exception  
 Produce una excepción `FormatException` cuando hay valores de entrada no válidos. Vea [STIsValid &#40; tipo de datos geography &#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)  
  
## <a name="remarks"></a>Comentarios  
 Método **null** cuando la entrada está vacía o la entrada tiene SRID diferentes. Vea [identificadores de referencia espacial &#40; SRID &#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
 Método omite **null** entradas.  
  
> [!NOTE]  
>  Método **null** si todos los valores introducidos son **null**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve una forma convexa del conjunto de **geography** objetos.  
  
 `USE AdventureWorks2012`  
  
 `GO`  
  
 `SELECT geography::ConvexHullAggregate(SpatialLocation).ToString() AS SpatialLocation`  
  
 `FROM Person.Address`  
  
 `WHERE City LIKE ('Bothell')`  
  
## <a name="see-also"></a>Vea también  
 [Métodos de geografía estáticos extendidos](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  

