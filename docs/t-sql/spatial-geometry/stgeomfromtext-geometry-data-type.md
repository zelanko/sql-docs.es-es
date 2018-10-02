---
title: STGeomFromText (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomFromText (geometry Data Type)
- STGeomFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomFromText (geometry Data Type)
ms.assetid: 20cace39-02e5-46c1-a9a5-841d04d0da16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a8436835ab2003e2700ec48d5a490887d0d0cb25
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47669803"
---
# <a name="stgeomfromtext-geometry-data-type"></a>STGeomFromText (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve una instancia de **geometry** a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC), ampliada con los valores Z (elevación) y M (medida) pertenecientes a la instancia.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
STGeomFromText ( 'geometry_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *geometry_tagged_text*  
 Es la representación WKT de la instancia de **geometry** que se quiere devolver. *geometry_tagged_text* es una expresión **nvarchar(max)**.  
  
 *SRID*  
 Es una expresión **int** que representa el identificador de referencia espacial (SRID) de la instancia de **geometry** que se quiere devolver.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
## <a name="remarks"></a>Notas  
 El tipo OGC de la instancia de **geometry** devuelta por `STGeomFromText()` se establece en la entrada WKT correspondiente.  
  
 Este método produce una excepción **FormatException** si la entrada no tiene el formato correcto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `STGeomeFromText()` para crear una instancia de `geometry`.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos de geometría estáticos de OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

