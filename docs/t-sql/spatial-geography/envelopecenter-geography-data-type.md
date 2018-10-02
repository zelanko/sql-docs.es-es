---
title: EnvelopeCenter (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeCenter
- EnvelopeCenter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeCenter method
ms.assetid: dee9d807-faad-45b8-b3f3-7e8aa7d07147
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d2f53f6efd0e4c1dbcbbeaccc78fd25fdad0c093
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685373"
---
# <a name="envelopecenter-geography-data-type-"></a>EnvelopeCenter (tipo de datos Geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve un punto que se puede usar como centro de un círculo límite para la instancia de **geography**.  
  
 Para determinar el círculo límite, cada punto de la instancia se describe como un vector desde el centro de la Tierra al punto en la superficie de la Tierra. Para calcular el punto central del círculo límite, se calcula el promedio de todos los vectores. En los bucles cerrados, en una instancia de **polygon** o de **linestring**, el primer punto y el último se usan solo una vez.  
  
 Este método del tipo de datos **geography** admite instancias de **FullGlobe** o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Notas  
 Este método devuelve un **point**. Cuando se usa con `EnvelopeAngle()`, `EnvelopeCenter()` devuelve un círculo de límite de una instancia de **geography**.  
  
> [!NOTE]  
>  `EnvelopeCenter()` devuelve un círculo de límite de una instancia de **geography**, pero no se garantiza que los resultados generen el círculo de límite mínimo. Por el contrario, se garantiza que el método `STEnvelope()` del tipo de datos **geometry** devuelve el cuadro de límite mínimo cuando se aplica a una instancia de **geometry**.  
  
 En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores, devuelve el centro del círculo que representa el envolvente de esta instancia como **point**. Para todos los objetos grandes como está definido en `EnvelopeAngle()` = 180, `EnvelopeCenter()` devolverá (90,0).  
  
 Este método no es preciso.  
  
## <a name="examples"></a>Ejemplos  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeAngle &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  
