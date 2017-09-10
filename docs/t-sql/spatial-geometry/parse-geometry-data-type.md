---
title: Parse (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Parse (geometry Data Type)
ms.assetid: 6e080919-4b64-46cd-8dd2-254a9c232e53
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 64adf9398a6ea63203f75714aa97ccf2653e947b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="parse-geometry-data-type"></a>Parse (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un **geometry** instancia a partir de una representación Open Geospatial Consortium (OGC) Well-Known Text (WKT). `Parse()`es equivalente a [STGeomFromText()](../../t-sql/spatial-geometry/parse-geometry-data-type.md), con la excepción que se considera espaciales identificador de referencia (SRID) de 0 como un parámetro. La entrada puede incluir valores opcionales para Z (elevación) y M (medida).
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Parse ( 'geometry_tagged_text' )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometry_tagged_text*  
 Es la representación WKT de la **geometry** instancia que se va a devolver. *geometry_tagged_text* es un **nvarchar** expresión.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Comentarios  
 El tipo OGC de la **geometry** instancia devuelta por `Parse()` se establece en la entrada WKT correspondiente.  
  
 La cadena 'Null' se interpretará como un valor null **geometry** instancia.  
  
 Este método producirá una **FormatException** si la entrada no tiene el formato correcto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `Parse()` para crear una instancia de `geometry`.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::Parse('LINESTRING (100 100, 20 180, 180 180)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [STGeomFromText](../../t-sql/spatial-geometry/parse-geometry-data-type.md)   
 [Métodos de geometría estáticos ampliados](../../t-sql/spatial-geometry/extended-static-geometry-methods.md)  
  
  


