---
title: STIsEmpty (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsEmpty_TSQL
- STIsEmpty (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsEmpty (geometry Data Type)
ms.assetid: dcbd6ae1-5d63-485f-9d58-28bfd504524e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f541f5420409293080eeb07bd1bbfc54f28ef504
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86555369"
---
# <a name="stisempty-geometry-data-type"></a>STIsEmpty (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Devuelve 1 si una instancia de **geometry** está vacía. Devuelve 0 si una instancia de **geometry** no está vacía.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STIsEmpty ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de valor devuelto
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de valor devuelto de CLR: **SqlBoolean**  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia vacía de `geometry` y se usa `STIsEmpty()` para comprobar si efectivamente está vacía.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON EMPTY', 0);  
SELECT @g.STIsEmpty();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

