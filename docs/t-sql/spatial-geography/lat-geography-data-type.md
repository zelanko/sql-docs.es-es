---
title: Lat (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Lat
- Lat_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Lat method
ms.assetid: 051d66bc-04de-4c58-861c-760dc5b859b5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fda04401334546cde33ca14034d344c8b444e138
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804321"
---
# <a name="lat-geography-data-type"></a>Lat (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve la propiedad de latitud de la instancia de **geography**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
.Lat  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de CLR: **SqlDouble**  
  
## <a name="remarks"></a>Notas  
 En el modelo OpenGIS, Lat se define solo en instancias de **geography** que constan de un único punto. Esta propiedad devuelve NULL si las instancias de **geography** contienen más de un punto. Esta propiedad es precisa y de solo lectura.  
  
## <a name="examples"></a>Ejemplos  
 Este ejemplo crea un punto y devuelve la latitud del punto.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Lat;  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
