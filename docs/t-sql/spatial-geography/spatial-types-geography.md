---
title: Geography (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: geography
dev_langs: TSQL
helpviewer_keywords:
- geography data type [SQL Server], Transact-SQL
- spatial data types [SQL Server]
ms.assetid: d9e4952a-1841-4465-a64b-11e9288dba1d
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: e13e451fefafe8f213bd63da41c22ede4c0f1b5b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="spatial-types---geography"></a>Tipos espaciales - geography
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  El tipo de datos espaciales geography, **geography**, se implementa como un .NET common language runtime (CLR) tipo de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este tipo representa los datos en un sistema de coordenadas de tierra redonda. El tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography** data type stores ellipsoidal (round-earth) data, such as GPS latitude and longitude coordinates.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]admite un conjunto de métodos para la **geography** tipo de datos espaciales. Se incluyen los métodos en **geography** que se definen mediante el estándar Open Geospatial Consortium (OGC) y un conjunto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] extensiones para dicho estándar.  
 
 La tolerancia de errores para el **geography** métodos pueden ser tan grandes como 1.0e-7 * extensiones. Las extensiones que hacen referencia a la distancia máxima aproximada entre los puntos de la **geography**objeto.
  

## <a name="registering-the-geography-type"></a>Registro del tipo de datos Geography  
 El tipo **geography** está predefinido y está disponible en cada base de datos. Puede crear columnas de tabla de tipo **geography** y operar con los datos **geography** de la misma manera que con los demás tipos proporcionados por el sistema. Se puede utilizar en columnas calculadas persistentes y no persistentes.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-showing-how-to-add-and-query-geography-data"></a>A. Mostrar cómo agregar y consultar datos geography  
 En los ejemplos siguientes se muestra cómo agregar y consultar datos geography. El primer ejemplo crea una tabla con una columna de identidad y un `geography` columna, `GeogCol1`. Una tercera columna representa la columna de tipo `geography` en su representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC) y utiliza el método `STAsText()` . A continuación se insertan dos filas: una que contiene una instancia de `LineString` de `geography`y otra que contiene una instancia de `Polygon` .  
  
```  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable   
    ( id int IDENTITY (1,1),  
    GeogCol1 geography,   
    GeogCol2 AS GeogCol1.STAsText() );  
GO  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656 )', 4326));  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('POLYGON((-122.358 47.653 , -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
GO  
```  
  
### <a name="b-returning-the-intersection-of-two-geography-instances"></a>B. Devolver la intersección de dos instancias de geography  
 En el ejemplo siguiente se utiliza el método `STIntersection()` para devolver los puntos de intersección de las dos instancias de `geography` insertadas previamente.  
  
```  
DECLARE @geog1 geography;  
DECLARE @geog2 geography;  
DECLARE @result geography;  
  
SELECT @geog1 = GeogCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geog2 = GeogCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geog1.STIntersection(@geog2);  
SELECT @result.STAsText();  
```  
  
### <a name="c-using-geography-in-a-computed-column"></a>C. Usar geography en una columna calculada  
 En el ejemplo siguiente se crea una tabla con una columna calculada persistente utilizando un **geography** tipo.  
  
```  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable  
(  
    locationId int IDENTITY(1,1),  
    location geography,  
    deliveryArea as location.STBuffer(10) persisted  
)  
```  
  
## <a name="see-also"></a>Vea también  
 [Datos espaciales &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   

  
  
