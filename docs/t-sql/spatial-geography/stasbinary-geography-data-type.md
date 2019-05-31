---
title: STAsBinary (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STAsBinary_TSQL
- STAsBinary (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsBinary method
ms.assetid: 99602a62-265d-4aa4-a8dc-92992ca55ba4
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 463b76f05f0b5bf3ad14a10382140436ea33c596
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65936210"
---
# <a name="stasbinary-geography-data-type"></a>STAsBinary (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve la representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC) de una instancia de **geography**.  
  
 Este método del tipo de datos **geography** admite instancias de **FullGlobe** o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STAsBinary ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **varbinary (max)**  
  
 Tipo de valor devuelto de CLR: **SqlBytes**  
  
## <a name="remarks"></a>Notas  
 El tipo OGC de una instancia de **geography** se puede determinar mediante la invocación de [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `STAsBinary()` para crear una instancia de `LineString``geography` de (-122.360, 47.656) a (-122.343, 47.656) a partir de texto. A continuación, devuelve el resultado en el formato WKB.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING( -122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsBinary();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
