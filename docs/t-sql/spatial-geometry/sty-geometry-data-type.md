---
title: STY (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STY_TSQL
- STY (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STY (geometry Data Type)
ms.assetid: f72e0eaa-7d1d-4052-88fd-a172d8cb0d71
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b4c8b0a123f2c4151a55813f0fd1025421e3eda3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755303"
---
# <a name="sty-geometry-data-type"></a>STY (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Propiedad de la coordenada Y de una instancia de **Point**.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STY  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de CLR: **SqlDouble**  
  
## <a name="remarks"></a>Notas  
 El valor de esta propiedad será NULL si la instancia de **geometry** es un punto. Esta propiedad es de solo lectura.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `Point` y se utiliza `STY` para recuperar la coordenada Y de la instancia.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 8)', 0);  
SELECT @g.STY;  
```  
  
## <a name="see-also"></a>Ver también  
 [STX &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STSrid &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)   
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

