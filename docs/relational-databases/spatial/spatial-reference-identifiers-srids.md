---
title: "Identificadores de referencia espacial (SRID) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-spatial"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Identificadores de referencia espacial (SRID)"
  - "datos espaciales geodésicos [SQL Server], identificadores"
  - "SRID"
ms.assetid: 0612658a-7d1b-4178-bdc2-42b914ea31a7
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Identificadores de referencia espacial (SRID)
  Cada instancia espacial tiene un identificador de referencia espacial (SRID). El SRID corresponde a un sistema de referencia espacial basado en el elipsoide concreto usado para la creación de mapas de tierra plana o de tierra redonda.  
  
> [!IMPORTANT]  
>  Para obtener una descripción detallada y ejemplos de las características espaciales introducidas en [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluido un nuevo SRID, descargue las notas del producto sobre las [nuevas características espaciales de SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=226407).  
  
 Una columna espacial puede contener objetos con SRID diferentes. Sin embargo, solo se pueden usar instancias espaciales con el mismo SRID al realizar operaciones con métodos de datos espaciales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en sus datos. El resultado de cualquier método espacial derivado de dos instancias de datos espaciales solo es válido si dichas instancias tienen el mismo SRID basado en la misma unidad de medida, dato y proyección usados para determinar las coordenadas de las instancias. Las unidades de medida más comunes de un SRID son metros o metros cuadrados.  
  
 Si dos instancias espaciales no tienen el mismo SRID, los resultados de un método de tipo de datos **geometry** o **geography** usado en las instancias devolverá NULL. Por ejemplo, para que el siguiente término de predicado devuelva un resultado distinto de NULL, las dos instancias de **geometry**, `geometry1` y `geometry2`, deben tener el mismo SRID:  
  
 `geometry1.STIntersects(geometry2) = 1`  
  
> [!NOTE]  
>  El sistema de identificación de referencia espacial está definido por la norma de [European Petroleum Survey Group (EPSG)](http://go.microsoft.com/fwlink/?LinkId=99349), que consiste en un conjunto de normas desarrolladas para cartografía, sondeos y almacenamiento de datos geodésicos. Esta norma es propiedad del comité Surveying and Positioning Committee de Oil and Gas Producers (OGP).  
  
## Vea también  
 [Información general de los tipos de datos espaciales](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  