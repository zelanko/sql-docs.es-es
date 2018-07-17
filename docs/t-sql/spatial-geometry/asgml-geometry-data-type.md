---
title: AsGml (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ae0750b559f153faed05feaa2d2a0e561a6e133f
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36245427"
---
# <a name="asgml-geometry-data-type"></a>AsGml (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve la representación del lenguaje de marcado de geografía (GML) para una instancia de **geometry**.
  
Para obtener más información sobre el Lenguaje de marcado de geografía, vea la siguiente especificación de Open Geospatial Consortium:[ Especificaciones de OGC, Lenguaje de marcado de geografía.](http://go.microsoft.com/fwlink/?LinkId=93629)
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.AsGml ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **xml**  
  
 Tipo devuelto de CLR: **SqlXml**  
  
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
<LineString xmlns="http://www.opengis.net/gml">  
<posList>0 0 0 1 1 0</posList></LineString>  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos extendidos en instancias de geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

