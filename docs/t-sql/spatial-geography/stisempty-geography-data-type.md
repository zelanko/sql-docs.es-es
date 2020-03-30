---
title: STIsEmpty (tipo de datos geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsEmpty_TSQL
- STIsEmpty (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STIsEmpty method
ms.assetid: 4cbc66e3-9035-4ecf-8f5a-6301f168c26c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5cd0e37ddf47e80ff524d02688d5764d93717a67
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68042064"
---
# <a name="stisempty-geography-data-type"></a>STIsEmpty (tipo de datos geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve 1 si una instancia de **geography** está vacía. Devuelve 0 si una instancia de **geography** no está vacía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STIsEmpty ( )  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de valor devuelto de CLR: **SqlBoolean**  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una instancia vacía de `geography` y se usa `STIsEmpty()` para comprobar que efectivamente está vacía.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON EMPTY', 4326);  
SELECT @g.STIsEmpty();  
```  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de OGC en instancias de geography](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
