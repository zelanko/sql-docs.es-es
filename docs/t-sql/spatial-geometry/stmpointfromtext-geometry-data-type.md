---
title: STMPointFromText (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STMPointFromText (geometry Data Type)
- STMPointFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMPointFromText (geometry Data Type)
ms.assetid: 37059074-5ee8-4f55-9414-1e958fd3adaf
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: cc462311df940b03c8a76e2867c49e6b35729415
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65938611"
---
# <a name="stmpointfromtext-geometry-data-type"></a>STMPointFromText (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve una instancia de **geometry** a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC), ampliada con los valores Z (elevación) y M (medida) pertenecientes a la instancia.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
STMPointFromText ( 'multipoint_tagged_text', SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *multipoint_tagged_text*  
 Es la representación WKT de la instancia de **geometryMultiPoint** que se quiere devolver. *multipoint_tagged_text* es una expresión **nvarchar(max)** .  
  
 *SRID*  
 Es una expresión **int** que representa el identificador de referencia espacial (SRID) de la instancia de **geometryMultiPoint** que se quiere devolver.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de valor devuelto de CLR: **SqlGeometry**  
  
 Tipo de OGC: **MultiPoint**  
  
## <a name="remarks"></a>Notas  
 Este método produce una excepción **FormatException** si la entrada no tiene el formato correcto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `STMPointFromText()` para crear una instancia de `geometry`.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STMPointFromText('MULTIPOINT ((100 100), (200 200))', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de geometría estáticos de OGC](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

