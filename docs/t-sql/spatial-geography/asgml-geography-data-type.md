---
title: AsGml (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsGml_(geography_Data_Type)_TSQL
- AsGml
- AsGml_TSQL
- AsGml (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- AsGml method
ms.assetid: 67795c64-d8d3-48dc-93ef-3c8a9274deb6
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 9d4faaae6df3f1800c592d511972e9fa46c7348e
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65935468"
---
#  <a name="asgml---geography-data-type"></a>AsGml: tipo de datos geography
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve la representación del lenguaje de marcado de geografía (GML) de una instancia de **geography**.  
  
 Para obtener más información sobre el lenguaje de marcado de geografía, vea las siguientes especificaciones de Open Geospatial Consortium: [Especificaciones de OGC, Lenguaje de marcado de geografía](https://go.microsoft.com/fwlink/?LinkId=93629).  
  
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
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.AsGml();  
```  
  
 Este método devuelve la descripción como instancia de `LineString`.  
  
```  
<LineString xmlns="https://www.opengis.net/gml"><posList>47.656 -122.36 47.656 -122.343</posList></LineString>  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
