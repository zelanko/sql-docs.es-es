---
title: MultiLineString | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiLineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 95deeefe-d6c5-4a11-b347-379e4486e7b7
author: MladjoA
ms.author: mlandzic
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f8df41184356f29e3037f36d519c9957f2f3e5b7
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65936444"
---
# <a name="multilinestring"></a>MultiLineString
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Un **MultiLineString** es una colección de cero o más instancias de **geometry** o **geographyLineString** .  
  
## <a name="multilinestring-instances"></a>Instancias de MultiLineString  
 En la ilustración siguiente se muestran ejemplos de instancias de **MultiLineString** .  
  
 ![Ejemplos de instancias MultiLineString de geometry](../../relational-databases/spatial/media/multilinestring.gif "Ejemplos de instancias MultiLineString de geometry")  
  
 Como se muestra en la ilustración:  
  
-   La figura 1 es una instancia sencilla de **MultiLineString** cuyo límite son los cuatro extremos de sus dos elementos **LineString** .  
  
-   La figura 2 es una instancia sencilla de **MultiLineString** porque solo forman una intersección los extremos de los elementos **LineString** . El límite lo constituyen los dos extremos que no se superponen.  
  
-   La figura 3 es una instancia no sencilla de **MultiLineString** porque el interior de uno de sus elementos **LineString** forma parte de una intersección. El límite de esta instancia de **MultiLineString** lo constituyen los cuatro extremos.  
  
-   La figura 4 es una instancia de **MultiLineString** no sencilla y sin cerrar.  
  
-   La figura 5 es una instancia de **MultiLineString**sencilla y sin cerrar. No está cerrada porque no lo están sus elementos **LineStrings** . Es sencilla porque ninguno de los interiores de ninguna de las instancias de **LineStrings** forma parte de una intersección.  
  
-   La figura 6 es una instancia de **MultiLineString** sencilla y cerrada. Está cerrada porque lo están todos sus elementos. Es sencilla porque ninguno de sus elementos forma parte de una intersección con los interiores.  
  
### <a name="accepted-instances"></a>Instancias aceptadas  
 Para que se acepte una instancia de **MultiLineString** , debe estar vacío o estar formada solo por instancias de **LineString** aceptadas. Para obtener más información sobre instancias **LineString** aceptadas, vea [LineString](../../relational-databases/spatial/linestring.md). A continuación se enumeran ejemplos de instancias **MultiLineString** aceptadas.  
  
```sql  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
```  
  
En el siguiente ejemplo se produce una excepción `System.FormatException` porque la segunda instancia de **LineString** no es válida.  
  
```sql  
DECLARE @g geometry = 'MULTILINESTRING((1 1, 3 5),(-5 3))';  
```  
  
### <a name="valid-instances"></a>Instancias válidas  
Para que una instancia de **MultiLineString** sea válida debe cumplir los siguientes criterios:  
  
1.  Todas las instancias que forman la instancia de **MultiLineString** deben ser instancias válidas de **LineString** .  
  
2.  Dos de las instancias de **LineString** que forman la instancia de **MultiLineString** pueden superponerse durante un intervalo. Las instancias de **LineString** solo pueden formar una intersección o tocarse una a la otra o a otra instancia de **LineString** en un número finito de puntos.  
  
En el ejemplo siguiente se muestran tres instancias válidas de **MultiLineString** y una instancia de **MultiLineString** que no es válida.  
  
```sql  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
`@g4` no es válido porque la segunda instancia de **LineString** se superpone a la primera instancia de **LineString** en un intervalo. Se tocan en un número infinito de puntos.  
  
## <a name="examples"></a>Ejemplos  
El ejemplo siguiente crea una instancia sencilla de `geometry``MultiLineString` que contiene dos elementos `LineString` con un SRID de 0.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
```  
  
Para crear instancias de esta instancia con otro SRID, utilice `STGeomFromText()` o `STMLineStringFromText()`. También puede utilizar `Parse()` y, a continuación, modificar el SRID, como se muestra en el ejemplo siguiente.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
SET @g.STSrid = 13;  
```  
  
## <a name="see-also"></a>Consulte también  
 [STLength &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STIsClosed &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [LineString](../../relational-databases/spatial/linestring.md)   
 [Datos espaciales &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
