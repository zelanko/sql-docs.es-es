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
ms.openlocfilehash: 5a0c123b367fa2a85a1a3732200452a474b032c6
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68088924"
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries (tipo de datos geometry)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el número de geometrías que componen una instancia de **geometry**.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
.STNumGeometries ( )  
```  
  
## <a name="return-types"></a>Tipos de valor devuelto  
 Tipo de valor devuelto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo de valor devuelto de CLR: **SqlInt32**  
  
## <a name="remarks"></a>Observaciones  
 Este método devuelve 1 si la instancia de **geometry** no es una instancia de **MultiPoint**, **MultiLineString**, **MultiPolygon** o  **GeometryCollection** y 0 si la instancia de **geometry** está vacía.  
  
> [!NOTE]  
>  Si **GeometryCollection** tiene elementos anidados vacíos, `STNumGeometries()` no devuelve 0. Aunque los elementos de la instancia de **GeometryCollection** estén vacíos, la propia instancia no es un conjunto vacío.  
  
  

