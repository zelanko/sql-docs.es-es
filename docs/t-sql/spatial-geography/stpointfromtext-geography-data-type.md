---
title: STPointFromText (tipo de datos geography) | Documentos de Microsoft
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
- STPointFromText (geography Data Type)
- STPointFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STPointFromText method
ms.assetid: e5fe54dc-0007-4631-8dde-7ae4d4c41f6e
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1b887aa5f33d40b047a81837ea91bfff8ecca7d1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="stpointfromtext-geography-data-type"></a>STPointFromText (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un **geography** instancia a partir de una representación Open Geospatial Consortium (OGC) Well-Known Text (WKT), ampliada con los Z (elevación) y los valores M (medida) pertenecientes a la instancia.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
STPointFromText ( 'point_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *point_tagged_text*  
 Es la representación WKT de la **geographyPoint** instancia que se va a devolver. *point_tagged_text* es un **nvarchar (max)** expresión.  
  
 *SRID*  
 Es un **int** expresión que representa el espaciales identificador de referencia (SRID) de la **geographyPoint** instancia que se va a devolver.  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
 Tipo de OGC: **punto**  
  
## <a name="remarks"></a>Comentarios  
 Este método produce una **FormatException** si la entrada no tiene el formato correcto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `STPointFromText()` para crear una instancia de `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STPointFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de geografía estáticos de OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  

