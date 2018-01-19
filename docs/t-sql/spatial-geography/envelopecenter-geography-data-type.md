---
title: EnvelopeCenter (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- EnvelopeCenter
- EnvelopeCenter_TSQL
dev_langs: TSQL
helpviewer_keywords: EnvelopeCenter method
ms.assetid: dee9d807-faad-45b8-b3f3-7e8aa7d07147
caps.latest.revision: "17"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 07b46f0d198fe2e90456252c9b1ad95669cfc478
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/19/2018
---
# <a name="envelopecenter-geography-data-type-"></a>EnvelopeCenter (tipo de datos Geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve un punto que se puede usar como el centro de un círculo límite para la **geography** instancia.  
  
 Para determinar el círculo límite, cada punto de la instancia se describe como un vector desde el centro de la Tierra al punto en la superficie de la Tierra. Para calcular el punto central del círculo límite, se calcula el promedio de todos los vectores. Bucles cerrados, ya sea en un **polígono** instancia o un **linestring** de instancia, el primer y último punto se utiliza una sola vez.  
  
 Esto **geography** admite el método de tipo de datos **FullGlobe** instancias o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
EnvelopeCenter( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Comentarios  
 Este método devuelve un **punto**. Cuando se usa con `EnvelopeAngle()`, `EnvelopeCenter()` devuelve un círculo de límite de un **geography** instancia.  
  
> [!NOTE]  
>  `EnvelopeCenter()`Devuelve un círculo límite para un **geography** instancia, pero los resultados no se garantiza para generar el círculo de límite mínimo. En cambio, el **geometry** método de tipo de datos `STEnvelope()` se garantiza para devolver el cuadro de límite mínimo cuando se aplica a un **geometry** instancia.  
  
 En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores, devuelve el centro del círculo que representa el envolvente de esta instancia como un **punto**. Para todos los objetos grandes como está definido en `EnvelopeAngle()` = 180, `EnvelopeCenter()` devolverá (90,0).  
  
 Este método no es preciso.  
  
## <a name="examples"></a>Ejemplos  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';  
SELECT @g.EnvelopeCenter().ToString();  
```  
  
## <a name="see-also"></a>Vea también  
 [Métodos extendidos en instancias de Geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeAngle &#40; tipo de datos geography &#41;](../../t-sql/spatial-geography/envelopeangle-geography-data-type.md)  
  
  
