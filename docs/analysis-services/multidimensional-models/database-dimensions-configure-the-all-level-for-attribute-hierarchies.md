---
title: "Configurar el nivel (All) para las jerarquías de atributo | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- All members
- IsAggregatable property
- topmost levels [Analysis Services]
- (All) levels
- AttributeAllMemberName property
- levels [Analysis Services]
- members [Analysis Services], All
- AllMemberName property
ms.assetid: 0cb35e6f-b10f-483d-b893-78f6ca3979fd
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2378dafcda0d9eca8786fb81cadfd44b22d0998b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="database-dimensions---configure-the-all-level-for-attribute-hierarchies"></a>Dimensiones de base de datos: configurar el nivel (All) para las jerarquías de atributo
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], (All) es un nivel opcional generado por el sistema. Contiene un único miembro cuyo valor es la agregación de los valores de todos los miembros del nivel inmediatamente subordinado. Este miembro se denomina All. Se trata de un miembro generado por el sistema que no se encuentra en la tabla de dimensión. Puesto que el miembro del nivel (All) está en la parte superior de la jerarquía, el valor del miembro es la agregación consolidada de los valores de todos los miembros de la jerarquía. El miembro All actúa a menudo como miembro predeterminado de una jerarquía.  
  
 La presencia de un nivel (All) en una jerarquía de atributo depende del valor de la propiedad **IsAggregatable** para el atributo, mientras que la presencia de un nivel (All) en una jerarquía definida por el usuario depende de la propiedad **IsAggregatable** del atributo en el nivel superior de la jerarquía definida por el usuario. Si la propiedad **IsAggregatable** se establece en **True**, es necesario que exista un nivel (All). Una jerarquía no tiene el nivel (All) si la propiedad **IsAggregatable** se establece en **False**.  
  
## <a name="establishing-the-topmost-level"></a>Establecer el nivel superior  
 Si la propiedad **IsAggregatable** está establecida en **False** en el atributo de origen de un nivel de la jerarquía, por encima de dicho nivel no aparecerá ningún nivel que se pueda agregar en la jerarquía. Un nivel no agregable tiene que ser el nivel superior de cualquier jerarquía, o bien la propiedad **IsAggregatable** de los atributos de origen de los niveles situados por encima de este también tienen que establecerse en **False**.  
  
## <a name="all-member-and-all-level"></a>Miembro All y nivel (All)  
 El único miembro del nivel (All) se llama All. La propiedad **AttributeAllMemberName**de una dimensión especifica el nombre del miembro All para los atributos de una dimensión. La propiedad **AllMemberName** en una jerarquía especifica el nombre del miembro All de la jerarquía.  
  
## <a name="see-also"></a>Vea también  
 [Definir un miembro predeterminado](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  

