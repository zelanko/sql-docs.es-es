---
title: ReorientObject (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ReorientObject
- ReorientObject_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ReorientObject method (geography)
ms.assetid: e2a1a4f1-211b-4e82-abed-03fc7140a83c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0f14609b70d5984be8166e17a5388297fead4db0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800096"
---
# <a name="reorientobject-geography-data-type"></a>ReorientObject (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Devuelve una instancia de **geography** con las regiones interiores y exteriores intercambiadas.  
  
 Este método del tipo de datos **geography** admite instancias de **FullGlobe** o instancias espaciales mayores que un hemisferio.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.ReorientObject (geography)  
```  
  
## <a name="arguments"></a>Argumentos  
 *geography*  
 Es otra instancia de **geography** en la que se invoca `ReorientObject()`.  
  
## <a name="return-value"></a>Valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Notas  
 Este método cambia la orientación de anillo de todos los **Polygons** de **GeometryCollection**, pero no quita ni cambia los **Points** o **Linestrings** de la colección especificada.  
  
 Si se pasa **GeometryCollection** a este método, se reorientan todas las instancias de la colección, pero la colección en su totalidad no se reorienta.  
  
## <a name="examples"></a>Ejemplos  
  
```  
DECLARE @R GEOGRAPHY = GEOGRAPHY::Parse('Polygon((-10 -10, -10 10, 10 10, 10 -10, -10 -10))');  
SELECT @R.ReorientObject().STAsText();  
--Result: POLYGON ((10 10, -10 10, -10 -10, 10 -10, 10 10))  
```  
  
## <a name="see-also"></a>Ver también  
 [Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
