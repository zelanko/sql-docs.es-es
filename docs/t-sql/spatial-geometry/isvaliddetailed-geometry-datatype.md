---
title: IsValidDetailed (tipo de datos geometry) | Documentos de Microsoft
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
dev_langs: TSQL
helpviewer_keywords: IsValidDetailed geometry
ms.assetid: 5a31e88a-ad7b-4ef7-b773-e2571f1cb3aa
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96f7531e9b692db3a026e4697e502f3d10e39cfa
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="isvaliddetailed-geometry-datatype"></a>IsValidDetailed (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Devuelve un mensaje que puede ayudar a identificar problemas con un objeto espacial no válido. Cuando el objeto no es válido, solo se devuelve el primer error. Cuando el objeto es válido, se devuelve el valor 24400.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.IsValidDetailed()  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **nvarchar (max)**  
  
 Tipo de valor devuelto de CLR: **cadena**  
  
## <a name="remarks"></a>Comentarios  
 La tabla siguiente contiene los posibles valores devueltos:  
  
|Valor devuelto|Description|  
|------------------|-----------------|  
|24400|Válido|  
|24401|No es válido por un motivo desconocido.|  
|24402|No es válido porque el punto {0} es un punto aislado, que no es válido en este tipo de objeto.|  
|24403|No es válido porque algún par de bordes del polígono se solapan.|  
|24404|No es válido porque el anillo del polígono {0} se corta a sí mismo o a algún otro anillo.|  
|24405|No es válido porque algún anillo del polígono se corta a sí mismo o a algún otro anillo.|  
|24406|No es válido porque la curva {0} degenera en un punto.|  
|24407|No es válido porque el anillo de polígono {0} se contrae hasta una línea en {1} de punto.|  
|24408|No es válido porque el anillo del polígono {0} no se cierra.|  
|24409|No es válido porque alguna parte del anillo del polígono {0} está en el interior de un polígono.|  
|24410|No es válido porque el anillo {0} es el primero de un polígono que no es el anillo exterior.|  
|24411|No es válido porque el anillo {0} se encuentra fuera de la {1} de anillo exterior de su polígono.|  
|24412|No es válido porque no está conectado el interior de un polígono con {0} de anillos y {1}.|  
|24413|No es válido debido a dos bordes que se solapan en la curva {0}.|  
|24414|No es válido porque un borde de la curva {0} superpone a un borde de {1} de la curva.|  
|24415|No es válido porque el polígono tiene una estructura de anillo no válida.|  
|24416|No es válido porque en curva {0} del borde que comienza en el punto de {1} es una línea o un arco degenerado con extremos opuestos.|  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo de un objeto espacial no válido, se muestra cómo el **IsValidDetailed()** se comporta de métodos.  
  
```sql  
DECLARE @p GEOMETRY = 'Polygon((2 2, 4 4, 4 2, 2 4, 2 2))'  
SELECT @p.IsValidDetailed()  
--Returns: 24404: Not valid because polygon ring (1) intersects itself or some other ring.  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos extendidos en instancias de geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

