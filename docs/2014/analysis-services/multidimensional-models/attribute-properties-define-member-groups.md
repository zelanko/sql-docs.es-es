---
title: Definir grupos de miembros | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- member groups [Analysis Services]
- grouping members
- DiscretizationMethod property
ms.assetid: 006cc915-c499-4781-b9a7-01ad31bebf6a
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7b9daa1b369f1d42a4dbaea76060bdefe6741a18
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201485"
---
# <a name="define-member-groups"></a>Definir grupos de miembros
  Si un atributo contiene muchos miembros, puede elegir agruparlos en cubos, reduciendo así el número de miembros que los usuarios ven cuando exploran los datos en una jerarquía. También puede determinar el número de cubos en los que se agrupan los miembros y establecer un esquema de nomenclatura para los cubos. Para más información, vea [Agrupar miembros de atributos &#40;Discretización&#41;](attribute-properties-group-attribute-members.md).  
  
 Los miembros se agrupan estableciendo la propiedad **DiscretizationMethod** , a la que puede obtener acceso mediante la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Al crear grupos de miembros, los cambios no están a disposición de los usuarios hasta que se procesa la dimensión. Para obtener más información, consulte [procesamiento del objeto de modelo multidimensionales](processing-a-multidimensional-model-analysis-services.md).  
  
### <a name="to-create-member-groups"></a>Para crear grupos de miembros  
  
1.  Abra la dimensión con la que desea trabajar. De forma predeterminada, se abrirá la pestaña **Estructura de dimensión** .  
  
2.  En **Atributos**, haga clic con el botón derecho en el atributo cuyos miembros quiere agrupar y, después, haga clic en **Propiedades**.  
  
3.  En la lista desplegable junto a **DiscretizationMethod**, seleccione un método para agrupar los miembros. Para más información sobre la configuración de **DiscretizationMethod**, vea [Agrupar miembros de atributos &#40;Discretización&#41;](attribute-properties-group-attribute-members.md).  
  
  