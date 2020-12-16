---
description: Identificadores de referencia espacial (SRID)
title: Identificadores de referencia espacial (SRID) | Microsoft Docs
ms.date: 03/29/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Spatial Reference Identifiers (SRIDs)
- geodetic spatial data [SQL Server], identifiers
- SRID
ms.assetid: 0612658a-7d1b-4178-bdc2-42b914ea31a7
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2873242ab181ce3d550c5b4f2274fef368d5c0f8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473136"
---
# <a name="spatial-reference-identifiers-srids"></a>Identificadores de referencia espacial (SRID)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  Cada instancia espacial tiene un identificador de referencia espacial (SRID). El SRID corresponde a un sistema de referencia espacial basado en el elipsoide concreto usado para la creación de mapas de tierra plana o de tierra redonda.  
  
 Una columna espacial puede contener objetos con SRID diferentes. Sin embargo, solo se pueden usar instancias espaciales con el mismo SRID al realizar operaciones con métodos de datos espaciales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en sus datos. El resultado de cualquier método espacial derivado de dos instancias de datos espaciales solo es válido si dichas instancias tienen el mismo SRID basado en la misma unidad de medida, dato y proyección usados para determinar las coordenadas de las instancias. Las unidades de medida más comunes de un SRID son metros o metros cuadrados.  
  
 Si dos instancias espaciales no tienen el mismo SRID, los resultados de un método de tipo de datos **geometry** o **geography** usado en las instancias devolverá NULL. Por ejemplo, para que el siguiente término de predicado devuelva un resultado distinto de NULL, las dos instancias de **geometry** , `geometry1` y `geometry2`, deben tener el mismo SRID:  
  
 `geometry1.STIntersects(geometry2) = 1`  
  
> [!NOTE]  
>  El sistema de identificación de referencia espacial está definido por la norma de [Europaan Petroleum Survey Group (EPSG)](https://go.microsoft.com/fwlink/?LinkId=99349) , que consiste en un conjunto de normas desarrolladas para cartografía, sondeos y almacenamiento de datos geodésicos. Esta norma es propiedad del comité Surveying and Positioning Committee de Oil and Gas Producers (OGP).  
  
## <a name="see-also"></a>Consulte también  
 [Información general de los tipos de datos espaciales](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
