---
title: STX (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STX (geometry Data Type)
- STX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STX (geometry Data Type)
ms.assetid: 2aef77e8-0460-43f9-bad6-2aae6d8c36f9
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: f22b505e0fbb49790b855b0839530d9208477071
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65935582"
---
# <a name="stx-geometry-data-type"></a>STX (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

La propiedad de la coordenada x de una instancia de **Point**.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STX  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Notas  
 El valor de esta propiedad será NULL si la instancia de **geometry** no es un punto.  
  
 Esta propiedad es de solo lectura.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `Point` y se utiliza `STX` para recuperar la coordenada x de la instancia.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(3 8)', 0);  
SELECT @g.STX;  
```  
  
## <a name="see-also"></a>Consulte también  
 [STY &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/sty-geometry-data-type.md)   
 [STSrid &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stsrid-geometry-data-type.md)   
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

