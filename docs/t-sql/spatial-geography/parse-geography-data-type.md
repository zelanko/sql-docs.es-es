---
title: Parse (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Parse method
- Parse (geography Data Type)
ms.assetid: 21c402fa-fd0f-4d09-a097-49cee0316d4e
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 023af0279bdb848e299ec1dbe31ff82305ad109a
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65935908"
---
# <a name="parse-geography-data-type"></a>Parse (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve una instancia de **geography** a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC). Parse() es equivalente a [STGeomFromText](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md), con la diferencia de que presupone un identificador de referencia espacial (SRID) de 4326 como parámetro. La entrada puede incluir valores opcionales para Z (elevación) y M (medida).
  
Este método del tipo de datos **geography** admite instancias de **FullGlobe** o instancias espaciales mayores que un hemisferio.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Parse ( 'geography_tagged_text' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography_tagged_text*  
 Es la representación WKT de la instancia de **geography** que se devuelve. *geography_tagged_text* es una expresión **nvarchar**.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Notas  
 El tipo OGC de la instancia de **geography** devuelta por `Parse()` se establece en la entrada WKT correspondiente.  
  
 La cadena "Null" se interpretará como una instancia NULL de **geography**.  
  
 Este método producirá una excepción **ArgumentException** si la entrada contiene un borde opuesto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `Parse()` para crear una instancia de `geography`.  
  
```  
DECLARE @g geography;   
SET @g = geography::Parse('LINESTRING(-122.360 47.656, -122.343 47.656)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de geografía estáticos extendidos](../../t-sql/spatial-geography/extended-static-geography-methods.md)   
 [STGeomFromText &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
  
