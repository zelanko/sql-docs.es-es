---
title: "Definir una relación de hechos y las propiedades de relación de hechos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: fact dimensions [Analysis Services]
ms.assetid: d8e41724-da77-4ac1-bc42-956b5d91ea5d
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e1e58f9616fc40ad895858a6eb6b3cfa7e0bbed1
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="define-a-fact-relationship-and-fact-relationship-properties"></a>Definir relaciones de hechos y propiedades de las relaciones de hechos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Al definir una nueva dimensión de cubo o un nuevo grupo de medida, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] intentará detectar si una relación de dimensión de hechos existe y, a continuación, establezca la configuración de uso de dimensiones en **hechos**. Puede ver o modificar una relación de dimensión de hechos en la pestaña **Uso de dimensiones** del Diseñador de cubos. La relación de hechos entre una dimensión y un grupo de medida presenta las siguientes restricciones:  
  
-   Una dimensión de cubo solamente puede tener una relación de hechos para un determinado grupo de medida.  
  
-   Una dimensión de cubo puede tener relaciones de hechos independientes con varios grupos de medida.  
  
-   El atributo de granularidad de la relación debe ser el atributo clave (como Transaction Number) de la dimensión. De este modo se crea una relación de uno a uno entre la dimensión y los hechos de la tabla de hechos.  
  
  
