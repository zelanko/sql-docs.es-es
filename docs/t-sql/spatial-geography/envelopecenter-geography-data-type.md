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
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: da1c2fd6f1e6732f28f79196b433b8e46a595a85
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68066435"
---
# <a name="envelopecenter-geography-data-type"></a>EnvelopeCenter (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve un punto que se puede usar como centro de un círculo de límite para la instancia de **geography**.  
  
Cada punto de la instancia se describe como un vector. Para calcular el círculo de límite, el vector se extiende desde el centro de la Tierra hasta el punto en la superficie de la Tierra. Para calcular el punto central del círculo límite, se calcula el promedio de todos los vectores. En los bucles cerrados, en una instancia de **polygon** o de **linestring**, el primer punto y el último se usan solo una vez.  
  
Este método del tipo de datos **geography** admite instancias de **FullGlobe** o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto  
Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Observaciones  
Este método devuelve un **point**. Cuando se usa con `EnvelopeAngle()`, `EnvelopeCenter()` devuelve un círculo de límite de una instancia de **geography**.  
  
> [!NOTE]  
>  `EnvelopeCenter()` devuelve un círculo de límite de una instancia de **geography**, pero no se garantiza que los resultados generen el círculo de límite mínimo. Por el contrario, se garantiza que el método **del tipo de datos**geometry`STEnvelope()` devuelve el cuadro de límite mínimo cuando se aplica a una instancia de **geometry**.  
  
En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores, devuelve el centro del círculo que representa el envolvente de esta instancia como **point**. Para todos los objetos grandes como está definido en `EnvelopeAngle()` = 180, `EnvelopeCenter()` devolverá (90,0).  
  
Este método no es exacto.  
  
## <a name="examples"></a>Ejemplos  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
[Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
[EnvelopeAngle &#40;tipo de datos geography&#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  
