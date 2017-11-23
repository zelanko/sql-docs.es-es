---
title: STNumGeometries (tipo de datos geometry) | Documentos de Microsoft
ms.custom: 
ms.date: 08/03/2017
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
- STNumGeometries (geometry Data Type)
- STNumGeometries_TSQL
dev_langs: TSQL
helpviewer_keywords: STNumGeometries (geometry Data Type)
ms.assetid: 9402b03d-3039-42ca-ac59-f96b7f1a48de
caps.latest.revision: "22"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f1909f0d094ce1cfe170389de6ccd9c57f5503a8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el número de geometrías que componen un **geometry** instancia.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STNumGeometries ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de valor devuelto: **int**  
  
 Tipo de valor devuelto de CLR: **SqlInt32**  
  
## <a name="remarks"></a>Comentarios  
 Este método devuelve 1 si la **geometry** instancia no es un **MultiPoint**, **MultiLineString**, **MultiPolygon**, o  **GeometryCollection** instancia y 0 si la **geometry** instancia está vacía.  
  
> [!NOTE]  
>  Si un **GeometryCollection** tiene elementos anidados vacíos, `STNumGeometries()` no devolverá 0. Aunque los elementos de la **GeometryCollection** instancia está vacía, la propia instancia no es un conjunto vacío.  
  
  

