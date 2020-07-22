---
title: AsBinaryZM (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- AsBinaryZM geometry
ms.assetid: 5eae2872-adca-4b8f-8b04-4ee91ced98f1
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: c4ed01d89bbb56fd48d0c29a54cf8c248fba439c
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555735"
---
# <a name="asbinaryzm-geometry-datatype"></a>AsBinaryZM (tipo de datos geometry)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Devuelve la representación Well-Known Binary (WKB) de Open Geospatial Consortium (OGC) de una instancia de **geometry** ampliada con los valores **Z** (elevación) y **M** (medida) pertenecientes a la instancia.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.AsBinaryZM()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de valor devuelto
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **varbinary (max)**  
  
 Tipo de valor devuelto de CLR: **SqlBytes**  
  
## <a name="remarks"></a>Observaciones  
  
## <a name="examples"></a>Ejemplos  
  
```sql  
DECLARE @g1 GEOMETRY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  

