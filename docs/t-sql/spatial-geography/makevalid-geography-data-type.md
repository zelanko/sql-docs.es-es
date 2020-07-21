---
title: MakeValid (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- MakeValid method (geography)
ms.assetid: f67038e3-4f62-4465-994e-e95ac27d8ada
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9a57da991a4dbea9f44e70d68c372601ecb85146
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85705915"
---
# <a name="makevalid-geography-data-type"></a>MakeValid (tipo de datos geography)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  Convierte una instancia de **geography** que no es válida en una instancia de **geography** válida con un tipo de Open Geospatial Consortium (OGC) válido.  
  
 Si un objeto de entrada devuelve False para STIsValid(), `MakeValid()` convierte la instancia que no es válida en una instancia válida.  
  
 Este método del tipo de datos geography admite instancias de **FullGlobe** o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.MakeValid ()  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Observaciones  
 Este método puede cambiar el tipo de la instancia de **geography**. Además, los puntos de una instancia de **geography** pueden desplazarse ligeramente. Los resultados de algunos métodos, como NumPoint(), pueden cambiar.  
  
 En los casos en los que la instancia espacial que no es válida corta en intersección con el ecuador y el valor de EnvelopeAngle() es 180, se devolverá una instancia de **FullGlobe**. El método `MakeValid()` del tipo de datos **geography** hará todo lo posible pare devolver instancias válidas, pero no está garantizado que los resultados sean precisos ni exactos.  
  
> [!NOTE]  
>  Los objetos no válidos se pueden almacenar en la base de datos. Los métodos que se pueden ejecutar en instancias no válidas (aquellas en las que STIsValid() devuelve False) son métodos que comprueban la validez o permiten la exportación: STIsValid(), MakeValid(), STAsText(), STAsBinary(), ToString(), AsTextZM() y AsGml().  
  
 Este método no es preciso.  
  
## <a name="examples"></a>Ejemplos  
 En el primer ejemplo se crea una instancia de `LineString` no válida que se superpone a sí misma y usa `STIsValid()` para confirmar que es una instancia no válida. `STIsValid()` devuelve el valor 0 para una instancia no válida.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(0 2, 1 1, 1 0, 1 1, 2 2)', 4326);  
SELECT @g.STIsValid();  
```  
  
 En el segundo ejemplo se usa `MakeValid()` para convertir la instancia en válida y comprobar que de hecho es así. `STIsValid()` devuelve el valor 1 para una instancia válida.  
  
```  
SET @g = @g.MakeValid();  
SELECT @g.STIsValid();  
```  
  
 En el tercer ejemplo se comprueba cómo se ha cambiado la instancia para convertirla en una instancia válida.  
  
```  
SELECT @g.ToString();  
```  
  
 En este ejemplo, cuando se selecciona la instancia de `LineString`, los valores se devuelven como una instancia de `MultiLineString` válida.  
  
```  
MULTILINESTRING ((0 2, 1 1, 2 2), (1 1, 1 0))  
```  
  
## <a name="see-also"></a>Consulte también  
 [STIsValid &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
