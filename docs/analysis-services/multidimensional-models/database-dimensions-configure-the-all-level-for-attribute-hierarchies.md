---
title: Configurar el nivel (All) para las jerarquías de atributo | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 23b00a88c8abf80045a38d0b8cc5d0c695949b0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178903"
---
# <a name="database-dimensions---configure-the-all-level-for-attribute-hierarchies"></a>Dimensiones de base de datos: Configurar el nivel (All) para las jerarquías de atributo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], (All) es un nivel opcional generado por el sistema. Contiene un único miembro cuyo valor es la agregación de los valores de todos los miembros del nivel inmediatamente subordinado. Este miembro se denomina All. Se trata de un miembro generado por el sistema que no se encuentra en la tabla de dimensión. Puesto que el miembro del nivel (All) está en la parte superior de la jerarquía, el valor del miembro es la agregación consolidada de los valores de todos los miembros de la jerarquía. El miembro All actúa a menudo como miembro predeterminado de una jerarquía.  
  
 La presencia de un nivel (All) en una jerarquía de atributo depende del valor de la propiedad **IsAggregatable** para el atributo, mientras que la presencia de un nivel (All) en una jerarquía definida por el usuario depende de la propiedad **IsAggregatable** del atributo en el nivel superior de la jerarquía definida por el usuario. Si la propiedad **IsAggregatable** se establece en **True**, es necesario que exista un nivel (All). Una jerarquía no tiene el nivel (All) si la propiedad **IsAggregatable** se establece en **False**.  
  
## <a name="establishing-the-topmost-level"></a>Establecer el nivel superior  
 Si la propiedad **IsAggregatable** está establecida en **False** en el atributo de origen de un nivel de la jerarquía, por encima de dicho nivel no aparecerá ningún nivel que se pueda agregar en la jerarquía. Un nivel no agregable tiene que ser el nivel superior de cualquier jerarquía, o bien la propiedad **IsAggregatable** de los atributos de origen de los niveles situados por encima de este también tienen que establecerse en **False**.  
  
## <a name="all-member-and-all-level"></a>Miembro All y nivel (All)  
 El único miembro del nivel (All) se llama All. La propiedad **AttributeAllMemberName**de una dimensión especifica el nombre del miembro All para los atributos de una dimensión. La propiedad **AllMemberName** en una jerarquía especifica el nombre del miembro All de la jerarquía.  
  
## <a name="see-also"></a>Vea también  
 [Definir un miembro predeterminado](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  
