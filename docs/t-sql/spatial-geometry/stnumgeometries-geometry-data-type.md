---
title: STNumGeometries (tipo de datos geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumGeometries (geometry Data Type)
- STNumGeometries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumGeometries (geometry Data Type)
ms.assetid: 9402b03d-3039-42ca-ac59-f96b7f1a48de
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 99e8dd51d546a7f65771a23fd8748d9d0b17d6fb
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65938522"
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el número de geometrías que componen una instancia de **geometry**.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STNumGeometries ( )  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de valor devuelto de CLR: **SqlInt32**  
  
## <a name="remarks"></a>Notas  
 Este método devuelve 1 si la instancia de **geometry** no es una instancia de **MultiPoint**, **MultiLineString**, **MultiPolygon** o  **GeometryCollection** y 0 si la instancia de **geometry** está vacía.  
  
> [!NOTE]  
>  Si **GeometryCollection** tiene elementos anidados vacíos, `STNumGeometries()` no devuelve 0. Aunque los elementos de la instancia de **GeometryCollection** estén vacíos, la propia instancia no es un conjunto vacío.  
  
  

