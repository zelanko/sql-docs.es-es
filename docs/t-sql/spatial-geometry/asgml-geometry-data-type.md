---
title: AsGml (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsGml(geometry_Data_Type)_TSQL
- AsGml
- AsGml(geometry Data Type)
- AsGml_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsGml (geometry Data Type)
ms.assetid: f6c2e130-05f3-4ef3-921b-d78b51437d48
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: fcf83925a7093edd44ddf46c31bee4297631bf10
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65939180"
---
# <a name="asgml-geometry-data-type"></a>AsGml (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve la representación del lenguaje de marcado de geografía (GML) para una instancia de **geometry**.
  
Para obtener más información sobre el Lenguaje de marcado de geografía, vea la siguiente especificación de Open Geospatial Consortium:[ Especificaciones de OGC, Lenguaje de marcado de geografía.](https://go.microsoft.com/fwlink/?LinkId=93629)
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.AsGml ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **xml**  
  
 Tipo de valor devuelto de CLR: **SqlXml**  
  
## <a name="remarks"></a>Notas  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `LineString` y se usa `AsGML()` para devolver la descripción de GML de dicha instancia.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0)', 0)  
SELECT @g.AsGml();  
```  
  
 Este método devuelve la descripción como instancia de `LineString`.  
  
```  
<LineString xmlns="https://www.opengis.net/gml">  
<posList>0 0 0 1 1 0</posList></LineString>  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

