---
title: STPointN (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- STPointN_TSQL
- STPointN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN method
ms.assetid: 47670feb-b9e0-4b4b-af83-b9bba7da66ac
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d2cb15c564f13051f5d38fce49d7c3f9dd88487c
ms.sourcegitcommit: a6596c62f607041c4402f7d5b41a232fca257c14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36256937"
---
# <a name="stpointn-geography-data-type"></a>STPointN (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el punto especificado de una instancia de **geography**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STPointN ( expression )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Es una expresión **int** entre 1 y el número de puntos de la instancia de **geography**.  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
 Tipo Open Geospatial Consortium (OGC): **Point**  
  
## <a name="remarks"></a>Notas  
 Si se trata de una instancia de **geography** creada por el usuario, STPointN() devuelve el punto especificado por *expression* considerando los puntos en el orden en el que se especificaron inicialmente.  
  
 Si se trata de una instancia de **geography** generada por el sistema, STPointN() devuelve el punto especificado por *expression* considerando todos los puntos en el orden en que se generarían: primero por instancias de **geography**, después por anillos dentro de la instancia (si procede) y, luego, por puntos dentro del anillo. Este orden es determinista.  
  
 Si se llama a este método con un valor inferior a 1, se genera una excepción **ArgumentOutOfRangeException**.  
  
 Si se llama a este método con un valor superior al número de puntos de la instancia, devuelve NULL.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia de `LineString` y se usa `STPointN()` para recuperar el segundo punto de la descripción de la instancia.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
