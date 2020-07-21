---
title: M (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- M (geometry Data Type)
- M_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- M (geometry Data Type)
ms.assetid: 443ae2ea-739b-41ef-96cc-ac5dfd65e10b
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 0acb70b63e0c488913bd5633606acb63fa31b2b7
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759548"
---
# <a name="m-geometry-data-type"></a>M (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Valor **M** (medida) de la instancia de **geometry**. La semántica del valor de medida la define el usuario.  

## <a name="syntax"></a>Sintaxis  
  
```  
  
.M  
```  
  
## <a name="arguments"></a>Argumentos  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo de CLR: **SqlDouble**  
  
## <a name="remarks"></a>Observaciones  
 Si la instancia de **geometry** no es de tipo **Point**, se asignará el valor null a esta propiedad, así como a cualquier instancia de **Point** para la que no se establezca dicha propiedad.  
  
 Esta propiedad es de solo lectura.  
  
 Los valores **M** no se usan en los cálculos realizados por la biblioteca y, por lo tanto, no se incluirán en ninguno de dichos cálculos.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `Point` con valores Z (elevación) y M (medida), y se usa `M` para capturar el valor M de la instancia.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos extendidos en instancias de geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Z &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)   
 [AsTextZM &#40;tipo de datos geometry&#41;](../../t-sql/spatial-geometry/astextzm-geometry-data-type.md)  
  
  

