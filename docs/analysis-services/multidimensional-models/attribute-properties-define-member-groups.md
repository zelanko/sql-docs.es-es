---
title: Definir grupos de miembros | Documentos de Microsoft
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
helpviewer_keywords:
- member groups [Analysis Services]
- grouping members
- DiscretizationMethod property
ms.assetid: 006cc915-c499-4781-b9a7-01ad31bebf6a
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 26a3a5494cc51521fe9c5e5b179a493d4bed0205
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="attribute-properties---define-member-groups"></a>Propiedades de atributo: definir los grupos de miembros
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Si un atributo tiene un gran número de miembros, puede agrupar los miembros en sectores de almacenamiento, lo que reduce el número de miembros que los usuarios ven cuando exploran los datos en una jerarquía. También puede determinar el número de cubos en los que se agrupan los miembros y establecer un esquema de nomenclatura para los cubos. Para más información, vea [Agrupar miembros de atributos &#40;Discretización&#41;](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md).  
  
 Los miembros se agrupan estableciendo la propiedad **DiscretizationMethod** , a la que puede obtener acceso mediante la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Al crear grupos de miembros, los cambios no están a disposición de los usuarios hasta que se procesa la dimensión. Para más información, vea [Procesar un modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-create-member-groups"></a>Para crear grupos de miembros  
  
1.  Abra la dimensión con la que desea trabajar. De forma predeterminada, se abrirá la pestaña **Estructura de dimensión** .  
  
2.  En **Atributos**, haga clic con el botón derecho en el atributo cuyos miembros quiere agrupar y, después, haga clic en **Propiedades**.  
  
3.  En la lista desplegable junto a **DiscretizationMethod**, seleccione un método para agrupar los miembros. Para más información sobre la configuración de **DiscretizationMethod**, vea [Agrupar miembros de atributos &#40;Discretización&#41;](../../analysis-services/multidimensional-models/attribute-properties-group-attribute-members.md).  
  
  
