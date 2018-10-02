---
title: STIntersects (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIntersects (geometry Data Type)
- STIntersects_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIntersects (geometry Data Type)
ms.assetid: 7c18f5be-5a29-422e-8ca7-d8a5f38e03f5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 595fd7d26ea0fb7e8a2b9ecd7c76030032dc1185
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47751753"
---
# <a name="stintersects-geometry-data-type"></a>STIntersects (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve 1 si una instancia de **geometry** forma intersección con otra instancia de **geometry**. Devuelve 0 en caso contrario.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STIntersects ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 Es otra instancia de **geometry** con la que se compara la instancia en la que se invoca `STIntersects()`.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de valor devuelto de CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Notas  
 Este método siempre devuelve NULL si no coinciden los identificadores de referencia espacial (SRID) de las instancias de **geometry**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `STIntersects()` para determinar si dos instancias de `geometry` forman intersección.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0, 4 2)', 0);  
SET @h = geometry::STGeomFromText('POINT(1 1)', 0);  
SELECT @g.STIntersects(@h);  
```  
  
## <a name="see-also"></a>Ver también  
 [Información general sobre los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

