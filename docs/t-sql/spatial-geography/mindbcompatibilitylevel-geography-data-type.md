---
title: MinDbCompatibilityLevel (tipo de datos geography) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- MinDbCompatibilityLevel
- MinDbCompatibilityLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MinDbCompatibilityLevel method (geography)
ms.assetid: a9e44748-4a9e-4179-abc4-7631597be5a7
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6c95aafc0278834c6108b99dd67908958fb47b17
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mindbcompatibilitylevel-geography-data-type"></a>MinDbCompatibilityLevel (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve la compatibilidad de base de datos mínima que reconoce el **geography** tipo de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
. MinDbCompatibilityLevel ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **int**  
  
 Tipo de valor devuelto de CLR: **int**  
  
## <a name="remarks"></a>Comentarios  
 Use `MinDbCompatibilityLevel()` para probar un objeto espacial a efectos de compatibilidad antes de cambiar el nivel de compatibilidad de una base de datos. No es válida **geography** escriba devuelve 110.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-testing-circularstring-type-for-compatibility-with-compatibility-level-110"></a>A. Probar el tipo CircularString a efectos de compatibilidad con el nivel de compatibilidad 110  
 En el ejemplo siguiente se prueba una instancia de `CircularString` a efectos de compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(-120.533 46.566, -118.283 46.1, -122.3 47.45)';  
IF @g.MinDbCompatibilityLevel() <= 110  
BEGIN  
    SELECT @g.ToString();  
END  
  
```  
  
### <a name="b-testing-linestring-type-for-compatibility-with-compatibility-level-100"></a>B. Probar el tipo LineString a efectos de compatibilidad con el nivel de compatibilidad 100  
 En el ejemplo siguiente se prueba una instancia de `LineString` a efectos de compatibilidad con [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]:  
  
```  
DECLARE @g geometry = 'LINESTRING(-120.533 46.566, -118.283 46.1, -122.3 47.45)';  
IF @g.MinDbCompatibilityLevel() <= 100  
BEGIN  
    SELECT @g.ToString();  
END  
  
```  
  
### <a name="c-testing-the-value-of-a-geography-instance-for-compatibility"></a>C. Probar el valor de una instancia de Geography a efectos de compatibilidad  
 En el ejemplo siguiente se muestran los niveles de compatibilidad para dos instancias de `geography`. Una es menor que un hemisferio y la otra es mayor que un hemisferio:  
  
```  
DECLARE @g geography = geography::Parse('POLYGON((0 -10, 120 -10, 240 -10, 0 -10))');  
DECLARE @h geography = geography::Parse('POLYGON((0 10, 120 10, 240 10, 0 10))');  
IF (@g.EnvelopeAngle() >= 90)  
BEGIN  
SELECT @g.MinDbCompatibilityLevel();  
END     
IF (@h.EnvelopeAngle() < 90)  
BEGIN  
SELECT @h.MinDbCompatibilityLevel();  
END  
  
```  
  
 La primera instrucción SELECT devuelve 110 y la segunda instrucción SELECT devuelve 100.  
  
## <a name="see-also"></a>Vea también  
 [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [Compatibilidad con versiones anteriores del motor de base de datos SQL Server](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
  
  

