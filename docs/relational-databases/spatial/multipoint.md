---
title: MultiPoint | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiPoint geometry subtype [SQL Server]
ms.assetid: 2aaab211-3aba-4dbd-90b7-095d997b1f62
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5551c6547fd93d0d6dce0565e152ba65650b6be7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85640391"
---
# <a name="multipoint"></a>MultiPoint
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Un **MultiPoint** es una colección de cero o más puntos. El límite de una instancia de **MultiPoint** está vacío.  
  
## <a name="examples"></a>Ejemplos  

### <a name="example-a"></a>Ejemplo A.
El ejemplo siguiente crea una instancia de `geometry MultiPoint` con SRID 23 y dos puntos: un punto con las coordenadas (2, 3), un punto con las coordenadas (7, 8) y un valor de Z de 9,5.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
### <a name="example-b"></a>Ejemplo B. 
En el ejemplo siguiente se expresa la instancia de `MultiPoint` mediante `STMPointFromText()`.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STMPointFromText('MULTIPOINT((2 3), (7 8 9.5))', 23);  
```  
  
### <a name="example-c"></a>Ejemplo C.
El ejemplo siguiente usa el método `STGeometryN()` para recuperar una descripción del primer punto de la colección.  
  
```sql  
SELECT @g.STGeometryN(1).STAsText();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Punto](../../relational-databases/spatial/point.md)   
 [Datos espaciales &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
