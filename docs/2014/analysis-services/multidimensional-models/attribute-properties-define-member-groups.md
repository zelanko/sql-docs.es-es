---
title: Definir grupos de miembros | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- member groups [Analysis Services]
- grouping members
- DiscretizationMethod property
ms.assetid: 006cc915-c499-4781-b9a7-01ad31bebf6a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2da7f19fa9626792a117ffa0108a28c50f32c5f5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66077298"
---
# <a name="define-member-groups"></a>Definir grupos de miembros
  Si un atributo contiene muchos miembros, puede elegir agruparlos en cubos, reduciendo así el número de miembros que los usuarios ven cuando exploran los datos en una jerarquía. También puede determinar el número de cubos en los que se agrupan los miembros y establecer un esquema de nomenclatura para los cubos. Para más información, vea [Agrupar miembros de atributos &#40;Discretización&#41;](attribute-properties-group-attribute-members.md).  
  
 Los miembros se agrupan estableciendo la propiedad **DiscretizationMethod** , a la que puede obtener acceso mediante la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Al crear grupos de miembros, los cambios no están a disposición de los usuarios hasta que se procesa la dimensión. Para obtener más información, vea [procesamiento de objetos de modelo multidimensional](processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-create-member-groups"></a>Para crear grupos de miembros  
  
1.  Abra la dimensión con la que desea trabajar. De forma predeterminada, se abrirá la pestaña **Estructura de dimensión** .  
  
2.  En **Atributos**, haga clic con el botón derecho en el atributo cuyos miembros quiere agrupar y, después, haga clic en **Propiedades**.  
  
3.  En la lista desplegable junto a **DiscretizationMethod**, seleccione un método para agrupar los miembros. Para más información sobre la configuración de **DiscretizationMethod**, vea [Agrupar miembros de atributos &#40;Discretización&#41;](attribute-properties-group-attribute-members.md).  
  
  
