---
title: STPointFromText (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointFromText (geography Data Type)
- STPointFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STPointFromText method
ms.assetid: e5fe54dc-0007-4631-8dde-7ae4d4c41f6e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5eb48601ba6b584f0846e873c3aff4f326f72493
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86556037"
---
# <a name="stpointfromtext-geography-data-type"></a>STPointFromText (tipo de datos geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Devuelve una instancia de **geography** a partir de una representación Well-Known Text (WKT) de Open Geospatial Consortium (OGC), ampliada con los valores Z (elevación) y M (medida) pertenecientes a la instancia.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
STPointFromText ( 'point_tagged_text' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *point_tagged_text*  
 Es la representación WKT de la instancia de **geographyPoint** que se quiere devolver. *point_tagged_text* es una expresión **nvarchar(max)** .  
  
 *SRID*  
 Es una expresión **int** que representa el identificador de referencia espacial (SRID) de la instancia de **geographyPoint** que quiere devolver.  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de valor devuelto de CLR: **SqlGeography**  
  
 Tipo OGC: **Point**  
  
## <a name="remarks"></a>Observaciones  
 Este método produce una excepción **FormatException** si la entrada no tiene el formato correcto.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `STPointFromText()` para crear una instancia de `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STPointFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de geografía estáticos de OGC](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
