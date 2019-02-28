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
ms.openlocfilehash: cda6f09124127d04c8ded1773feab4e9ffbf2ba9
ms.sourcegitcommit: 01e17c5f1710e7058bad8227c8011985a9888d36
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56265232"
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
_geography_  
Es otra instancia de **geography** en la que se invoca `ReorientObject()`.  
  
## <a name="return-value"></a>Valor devuelto  
Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
Tipo de valor devuelto de CLR: **SqlGeography**  
  
## <a name="remarks"></a>Notas  
Este método cambia la orientación de anillo de todos los **Polygons** de **GeometryCollection**, pero no quita ni cambia los **Points** o **LineStrings** de la colección especificada.  
  
Si se pasa **GeometryCollection** a este método, se reorientan todas las instancias de la colección, pero la colección en su totalidad no se reorienta.  
  
## <a name="examples"></a>Ejemplos  
  
```  
DECLARE @R GEOGRAPHY = GEOGRAPHY::Parse('Polygon((-10 -10, -10 10, 10 10, 10 -10, -10 -10))');  
SELECT @R.ReorientObject().STAsText();  
--Result: POLYGON ((10 10, -10 10, -10 -10, 10 -10, 10 10))  
```  
  
## <a name="see-also"></a>Consulte también  
[Métodos extendidos en instancias de geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
