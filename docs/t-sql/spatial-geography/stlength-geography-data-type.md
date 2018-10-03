---
title: STLength (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLength (geography Data Type)
- STLength_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLength method
ms.assetid: 774560ab-4a4a-4058-b043-1e67cf6fb9eb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a07da59b2ed5d6da4ee6cf6180cfb65470ee5793
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47764763"
---
# <a name="stlength-geography-data-type"></a>STLength (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve la longitud total de los elementos de una instancia de **geography** o las instancias de **geography** incluidas en una colección **GeometryCollection**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STLength ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de valor devuelto de CLR: **SqlDouble**  
  
## <a name="remarks"></a>Notas  
 Si se trata de una instancia de **geography** cerrada, su longitud se calcula como la longitud total alrededor de la instancia; la longitud de cualquier polígono es su perímetro y la longitud de un punto es 0. La longitud de una colección de **GeometryCollection** se halla calculando la suma de las longitudes de todas las instancias de **geography** contenidas dentro de la colección.  
  
 STLength() funciona con LineString válidos y no válidos. Si un LineString no es válido normalmente se debe a la superposición de segmentos, lo cual se puede deber a anomalías como seguimientos de GPS inexactos. STLength() no quita segmentos superpuestos o no válidos. Incluye los segmentos superpuestos y no válidos en el valor de longitud que devuelve. El método MakeValid() puede quitar segmentos superpuestos de un LineString.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `LineString` y se usa `STLength()` para averiguar la longitud de dicha instancia.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STLength();  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
