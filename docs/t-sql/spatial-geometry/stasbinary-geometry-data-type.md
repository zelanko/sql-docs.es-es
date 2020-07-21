---
title: STAsBinary (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STAsBinary_TSQL
- STAsBinary (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsBinary (geometry Data Type)
ms.assetid: 65353777-e3e6-461c-9504-ea4d83312692
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: aa0bc1c078e476fbf888f632f583179c6066e1e8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748807"
---
# <a name="stasbinary-geometry-data-type"></a>STAsBinary (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Devuelve la representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC) de una instancia de geometry.  
 
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STAsBinary ( )  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **varbinary (max)**  
  
 Tipo de valor devuelto de CLR: **SqlBytes**  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de geometría `LineString` desde (0,0) hasta (2,3) a partir del texto. `STAsBinary()` devuelve el resultado en WKB.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 3)', 0);  
SELECT @g.STAsBinary();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
