---
title: Configurar el nivel (All) para las jerarquías de atributo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 13e4ca2c3eb2336a4434cd37bfd0c8484ab4c91c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325105"
---
# <a name="configure-the-all-level-for-attribute-hierarchies"></a>Configurar el nivel (All) para las jerarquías de atributo
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], (All) es un nivel opcional generado por el sistema. Contiene un único miembro cuyo valor es la agregación de los valores de todos los miembros del nivel inmediatamente subordinado. Este miembro se denomina All. Se trata de un miembro generado por el sistema que no se encuentra en la tabla de dimensión. Puesto que el miembro del nivel (All) está en la parte superior de la jerarquía, el valor del miembro es la agregación consolidada de los valores de todos los miembros de la jerarquía. El miembro All actúa a menudo como miembro predeterminado de una jerarquía.  
  
 La presencia de un nivel (All) en una jerarquía de atributo depende del `IsAggregatable` depende de la configuración de la propiedad del atributo y la presencia de un nivel (All) en una jerarquía definida por el usuario la `IsAggregatable` propiedad del atributo en el nivel superior de jerarquía definida por el usuario. Si la propiedad `IsAggregatable` está establecida en `True`, existirá un nivel (All). Una jerarquía no tendrá nivel (All) si la propiedad `IsAggregatable` está establecida en `False`.  
  
## <a name="establishing-the-topmost-level"></a>Establecer el nivel superior  
 Si la propiedad `IsAggregatable` está establecida en `False` en el atributo de origen de un nivel de la jerarquía, por encima de dicho nivel no aparecerá ningún nivel que se pueda agregar en la jerarquía. Un nivel que no se pueda agregar debe ser el nivel superior de cualquier jerarquía o la propiedad `IsAggregatable` de los atributos de origen de los niveles situados por encima de él deben también establecerse en `False`.  
  
## <a name="all-member-and-all-level"></a>Miembro All y nivel (All)  
 El único miembro del nivel (All) se llama All. El `AttributeAllMemberName`propiedad en una dimensión especifica el nombre del miembro All para los atributos de una dimensión. La propiedad `AllMemberName` en una jerarquía especifica el nombre del miembro All de la jerarquía.  
  
## <a name="see-also"></a>Vea también  
 [Definir un miembro predeterminado](attribute-properties-define-a-default-member.md)  
  
  
