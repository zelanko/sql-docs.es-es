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
ms.openlocfilehash: 3bd050fc07c39dc33781a2c9c1ec09128540f216
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762275"
---
# <a name="stnumgeometries-geometry-data-type"></a>STNumGeometries (tipo de datos geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

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
  
  

