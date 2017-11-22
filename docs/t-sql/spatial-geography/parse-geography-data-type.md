---
title: Parse (tipo de datos geography) | Documentos de Microsoft
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
helpviewer_keywords:
- Parse method
- Parse (geography Data Type)
ms.assetid: 21c402fa-fd0f-4d09-a097-49cee0316d4e
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 932a65d59e0083463533493071987f6af79be54c
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="parse-geography-data-type"></a>Parse (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un **geography** instancia a partir de una representación Open Geospatial Consortium (OGC) Well-Known Text (WKT). Parse() equivale a [STGeomFromText](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md), salvo que presupone un identificador (SRID) de 4326 como parámetro de referencia espacial. La entrada puede incluir valores opcionales para Z (elevación) y M (medida).
  
Esto **geography** admite el método de tipo de datos **FullGlobe** instancias o instancias espaciales mayores que un hemisferio.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Parse ( 'geography_tagged_text' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography_tagged_text*  
 Es la representación WKT de la **geography** instancia para devolver. *geography_tagged_text* es un **nvarchar** expresión.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentarios  
 El tipo OGC de la **geography** instancia devuelta por `Parse()` se establece en la entrada WKT correspondiente.  
  
 La cadena 'Null' se interpretará como un valor null **geography** instancia.  
  
 Este método producirá **ArgumentException** si la entrada contiene un borde opuesto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `Parse()` para crear una instancia de `geography`.  
  
```  
DECLARE @g geography;   
SET @g = geography::Parse('LINESTRING(-122.360 47.656, -122.343 47.656)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de geografía estáticos extendidos](../../t-sql/spatial-geography/extended-static-geography-methods.md)   
 [STGeomFromText &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
  
