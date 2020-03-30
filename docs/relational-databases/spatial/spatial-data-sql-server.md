---
title: Datos espaciales (SQL Server) | Microsoft Docs
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f600f45241016bc2f5bb59faa89b5f45b317c90d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "72278142"
---
# <a name="spatial-data-sql-server"></a>Datos espaciales (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Los datos espaciales representan información sobre la ubicación física y la forma de objetos geométricos. Estos objetos pueden ser ubicaciones de punto u objetos más complejos como países, carreteras o lagos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite dos tipos de datos espaciales: el tipo de datos **geometry** y el tipo de datos **geography** .  
  
-   El tipo **geometry** representa los datos en un sistema de coordenadas euclidiano (plano).  
  
-   El tipo **geography** representa los datos en un sistema de coordenadas de tierra redonda.  
  
 Ambos tipos de datos se implementan como tipos de datos .NET Common Language Runtime (CLR) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="related-tasks"></a><a name="reltasks"></a> Tareas relacionadas  
 [Creación, construcción y consulta de instancias de Geometry](../../relational-databases/spatial/create-construct-and-query-geometry-instances.md)  
 Describe métodos que puede usar con instancias del tipo de datos geometry.  
  
 [Creación, construcción y consulta de instancias de Geography](../../relational-databases/spatial/create-construct-and-query-geography-instances.md)  
 Describe métodos que puede usar con instancias del tipo de datos geography.  
  
 [Consulta de datos espaciales para el vecino más próximo](../../relational-databases/spatial/query-spatial-data-for-nearest-neighbor.md)  
 Describe el modelo de consulta común que se usa para buscar los objetos espaciales más cercanos a un objeto espacial concreto.  
  
 [Creación, modificación y eliminación de índices espaciales](../../relational-databases/spatial/create-modify-and-drop-spatial-indexes.md)  
 Proporciona información acerca de cómo crear, modificar y quitar un índice espacial.  
  
## <a name="related-content"></a>Contenido relacionado  
 [Información general de los tipos de datos espaciales](../../relational-databases/spatial/spatial-data-types-overview.md)  
 Presenta los tipos de datos espaciales.  
  
-   [Point](../../relational-databases/spatial/point.md)  
  
-   [LineString](../../relational-databases/spatial/linestring.md)  
  
-   [CircularString](../../relational-databases/spatial/circularstring.md)  
  
-   [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)  
  
-   [Polygon](../../relational-databases/spatial/polygon.md)  
  
-   [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  
  
-   [MultiPoint](../../relational-databases/spatial/multipoint.md)  
  
-   [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
  
-   [MultiPolígono](../../relational-databases/spatial/multipolygon.md)  
  
-   [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  
  
 [Información general sobre los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md)  
 Presenta los índices espaciales, y describe la teselación y los esquemas de teselación.  
  
  
