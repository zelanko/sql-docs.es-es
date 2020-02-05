---
title: STSrid (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STSrid (geometry Data Type)
- STSrid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSrid (geometry Data Type)
ms.assetid: 5e0de983-a0fe-48b7-9e08-30588d7271e2
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f1119c0c906e3a3825882e3fe1043e9bdaceb0f9
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68066299"
---
# <a name="stsrid-geometry-data-type"></a>STSrid (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **STSrid** es un número entero que representa el identificador de referencia espacial de la instancia.  
  
Esta propiedad se puede modificar.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
STSrid  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de CLR: **SqlInt32**  
  
## <a name="examples"></a>Ejemplos  
 En el primer ejemplo se crea una instancia de **geometry** con el valor SRID 13 y se usa `STSrid` para confirmar dicho SRID.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0))', 13);  
SELECT @g.STSrid;  
```  
  
 El segundo ejemplo usa `STSrid` para cambiar el valor SRID de la instancia a 23 y, a continuación, confirma la modificación de dicho valor.  
  
```  
SET @g.STSrid = 23;  
SELECT @g.STSrid;  
```  
  
## <a name="see-also"></a>Consulte también  
 [STX &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/stx-geometry-data-type.md)   
 [STY &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/sty-geometry-data-type.md)   
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

