---
title: STAsText (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STAsText_TSQL
- STAsText (geometry Data Type)
dev_langs: TSQL
helpviewer_keywords: STAsText (geometry Data Type)
ms.assetid: e0decf5e-2858-4c56-b61a-6123f47fb51c
caps.latest.revision: "25"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: aac75544ff6e47c5cdabde89e3b051ef6cd26811
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="stastext-geometry-data-type"></a>STAsText (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Devuelve la representación de Open Geospatial Consortium (OGC) Well-Known Text (WKT) de un **geometry** instancia. Este texto no contendrá ningún valor Z (elevación) ni M (medida) perteneciente a la instancia.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STAsText ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **nvarchar (max)**  
  
 Tipo de valor devuelto de CLR: **SqlChars**  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de geometría `LineString` desde (0,0) hasta (2,3) a partir del texto. `STAsText()` devuelve el resultado en forma de texto.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 3)', 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

