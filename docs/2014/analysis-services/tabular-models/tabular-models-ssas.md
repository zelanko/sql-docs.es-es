---
title: Tabular (SSAS Tabular) de modelado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 80027288-c203-4667-a3e1-40fa572b4975
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 11a5a9332c7fa85fd6407523ffd9c7c48a2c0514
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198755"
---
# <a name="tabular-modeling-ssas-tabular"></a>Modelado tabular (SSAS tabular)
  Los modelos tabulares son bases de datos "en memoria" de Analysis Services. Gracias a los algoritmos de compresión avanzados y al procesador de consultas multiproceso, el motor analítico en memoria xVelocity (VertiPaq) ofrece un acceso rápido a los objetos y los datos de los modelos tabulares para aplicaciones cliente de informes como Microsoft Excel y Microsoft [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
 Los modelos tabulares admiten el acceso a los datos mediante dos modos: modo de almacenamiento en caché y modo DirectQuery. En el modo de almacenamiento en caché, puede integrar datos de varios orígenes como bases de datos relacionales, fuentes de distribución de datos y archivos de texto planos. En el modo DirectQuery, puede omitir el modelo en memoria, lo que permite a las aplicaciones cliente consultar los datos directamente en el origen relacional (SQL Server).  
  
 Los modelos tabulares se crean en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] mediante las nuevas plantillas de proyectos de modelos tabulares. Puede importar datos de varios orígenes y, a continuación, enriquecer el modelo agregando relaciones, columnas calculadas, medidas, KPI y jerarquías. A continuación, los modelos se pueden implementar en una instancia de Analysis Services que permite a las aplicaciones cliente de informes conectarse con ellos. Los modelos implementados se pueden administrar en SQL Server Management Studio del mismo modo que los modelos multidimensionales. También se pueden crear particiones de los mismos para optimizar el procesamiento y protegerlos en el nivel de fila usando la seguridad basada en roles.  
  
## <a name="in-this-section"></a>En esta sección  
 [Soluciones de modelos tabulares &#40;Tabular de SSAS&#41;](../tabular-model-solutions-ssas-tabular.md)  
  
 [Las bases de datos de modelo tabular &#40;Tabular de SSAS&#41;](tabular-model-databases-ssas-tabular.md)  
  
 [Acceso a datos de modelos tabulares](tabular-model-data-access.md)  
  
  
