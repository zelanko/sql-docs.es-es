---
title: GeomFromGML (tipo de datos geography) | Documentos de Microsoft
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
- GeomFromGML_TSQL
- GeomFromGML
dev_langs:
- TSQL
helpviewer_keywords:
- GeomFromGML (geography Data Type)
- GeomFromGML method
ms.assetid: 470d0997-3cb0-4d34-9a45-b332fe432b14
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ec0d21afb92b000f29fb91c4e3b848b4881b99c7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="geomfromgml-geography-data-type"></a>GeomFromGML (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Construye un **geography** instancia dada una representación en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subconjunto del lenguaje de marcado de geografía (GML).
  
Para obtener más información sobre GML, consulte las siguientes especificaciones de Open Geospatial Consortium: [especificaciones de OGC, lenguaje de marcado de geografía](http://go.microsoft.com/fwlink/?LinkId=93629)
  
Esto **geography** admite el método de tipo de datos **FullGlobe** instancias o instancias espaciales mayores que un hemisferio.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
GeomFromGml ( GML_input, SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *GML_input*  
 Es una entrada XML desde la que GML devolverá un valor.  
  
 *SRID*  
 Es un **int** expresión que representa el espaciales identificador de referencia (SRID) de la **geography** instancia para devolver.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentarios  
 Este método produce una **FormatException** si la entrada no tiene el formato correcto.  
  
 Este método producirá **ArgumentException** si la entrada contiene borde opuesto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `GeomFromGml()` para crear una instancia de `geography`.  
  
```  
DECLARE @g geography;  
DECLARE @x xml;  
SET @x = '<LineString xmlns="http://www.opengis.net/gml"><posList>47.656 -122.36 47.656 -122.343</posList></LineString>';  
SET @g = geography::GeomFromGml(@x, 4326);  
SELECT @g.ToString();  
```  
  
 En el ejemplo siguiente se usa `GeomFromGml()` para crear una instancia de `FullGlobe``geography`.  
  
```  
DECLARE @g geography;  
DECLARE @x xml;  
SET @x = '<FullGlobe xmlns="http://schemas.microsoft.com/sqlserver/2011/geography" />';  
SET @g = geography::GeomFromGml(@x, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de geografía estáticos extendidos](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  

