---
title: Datos espaciales (SQL Server) | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geography data type [SQL Server], spatial storage design
- planar spatial data [SQL Server], designing
- spatial data types [SQL Server]
- geodetic spatial data [SQL Server]
- geometry data type [SQL Server], spatial storage design
- spatial storage [SQL Server]
- geodetic spatial data [SQL Server], designing
ms.assetid: 41a132a1-09e2-4426-b9df-225270cb8e15
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 7bd529f67f9184f86d4a9ec704e9cf7af972f3f3
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66014054"
---
# <a name="spatial-data-sql-server"></a>Datos espaciales (SQL Server)
  Los datos espaciales representan información sobre la ubicación física y la forma de objetos geométricos. Estos objetos pueden ser ubicaciones de punto u objetos más complejos como países, carreteras o lagos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite dos tipos de datos espaciales: el tipo de datos `geometry` y el tipo de datos `geography`.  
  
-   El tipo `geometry` representa los datos en un sistema de coordenadas euclidiano (plano).  
  
-   El tipo `geography` representa los datos en un sistema de coordenadas de tierra redonda.  
  
 Ambos tipos de datos se implementan como tipos de datos .NET Common Language Runtime (CLR) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Para obtener una descripción detallada y ejemplos de las características espaciales introducidas en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], descargue las notas del producto [New Spatial Features in SQL Server 2012 (Nuevas características espaciales de SQL Server 2012)](https://go.microsoft.com/fwlink/?LinkId=226407).  
  
##  <a name="reltasks"></a> Tareas relacionadas  
 [Crear, construir y consultar instancias de Geometry](create-construct-and-query-geometry-instances.md)  
 Describe métodos que puede usar con instancias del tipo de datos geometry.  
  
 [Crear, construir y consultar instancias de Geography](create-construct-and-query-geography-instances.md)  
 Describe métodos que puede usar con instancias del tipo de datos geography.  
  
 [Consultar datos espaciales para el vecino más próximo](query-spatial-data-for-nearest-neighbor.md)  
 Describe el modelo de consulta común que se usa para buscar los objetos espaciales más cercanos a un objeto espacial concreto.  
  
 [Crear, modificar y quitar índices espaciales](create-modify-and-drop-spatial-indexes.md)  
 Proporciona información acerca de cómo crear, modificar y quitar un índice espacial.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Información general de los tipos de datos espaciales](spatial-data-types-overview.md)  
 Presenta los tipos de datos espaciales.  
  
-   [Punto](point.md)  
  
-   [LineString](linestring.md)  
  
-   [CircularString](circularstring.md)  
  
-   [CompoundCurve](compoundcurve.md)  
  
-   [Polígono](polygon.md)  
  
-   [CurvePolygon](curvepolygon.md)  
  
-   [MultiPoint](multipoint.md)  
  
-   [MultiLineString](multilinestring.md)  
  
-   [MultiPolígono](multipolygon.md)  
  
-   [Colección Geometry](geometrycollection.md)  
  
 [Información general sobre los índices espaciales](spatial-indexes-overview.md)  
 Presenta los índices espaciales, y describe la teselación y los esquemas de teselación.  
  
  
