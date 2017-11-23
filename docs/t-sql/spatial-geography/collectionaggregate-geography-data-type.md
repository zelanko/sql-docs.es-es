---
title: CollectionAggregate (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 07/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords: CollectionAggregate method (geography)
ms.assetid: e49a644a-dbf2-46c3-98f5-4b3ec197e2ad
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2a2bec127117014b61cf9c40966ad1c28c4cee1c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="collectionaggregate-geography-data-type"></a>CollectionAggregate (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Crea un **GeometryCollection** instancia a partir de un conjunto de **geography** objetos.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ConvexHullAggregate ( geography_operand )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography_operand*  
 Es un **geography** columna de tabla de tipo que representa un conjunto de **geography** objetos que se mostrarán en el **GeometryCollection** instancia.  
  
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
 En el ejemplo siguiente se devuelve una `GeometryCollection` instancia que contiene un conjunto de **geography** objetos.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT geography::CollectionAggregate(SpatialLocation).ToString() AS SpatialLocation  
 FROM Person.Address  
 WHERE City LIKE ('Bothell')
 ```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de geografía estáticos extendidos](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
