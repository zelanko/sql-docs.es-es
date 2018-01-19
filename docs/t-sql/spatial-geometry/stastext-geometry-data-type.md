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
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2a4bf462c9502b5d6c714e2149669f8e3f82e0a4
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
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
  
  

