---
title: Propiedades - jerarquías de usuario del nivel | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 903ece979d44dedd6353919af28bdb6c82986e16
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="user-hierarchies---level-properties"></a>Jerarquías de usuario - propiedades de nivel
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En la siguiente tabla se enumeran y describen las propiedades de un nivel en una jerarquía definida por el usuario.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|Description|Contiene la descripción del nivel.|  
|HideMemberIf|Indica si un miembro en un nivel debe ocultarse de las aplicaciones cliente y cuándo. Esta propiedad puede tener los valores siguientes:<br /><br /> Never<br /> Los miembros nunca se ocultan. Es el valor predeterminado.<br /><br /> OnlyChildWithNoName<br /> Se oculta un miembro cuando el miembro es el único elemento secundario de un elemento primario y el nombre del miembro está vacío.<br /><br /> OnlyChildWithParentName<br /> Se oculta un miembro cuando el miembro es el único elemento secundario de un elemento primario y el nombre del miembro es idéntico al del elemento primario.<br /><br /> NoName<br /> Un miembro se oculta cuando el nombre del miembro está vacío.<br /><br /> ParentName<br /> Un miembro se oculta cuando el nombre del miembro es idéntico al del elemento primario.|  
|ID|Contiene el identificador único (Id.) del nivel.|  
|Nombre|Contiene el nombre descriptivo del nivel. De forma predeterminada, el nombre de un nivel es el mismo que el nombre del atributo de origen.|  
|SourceAttribute|Contiene el nombre del atributo de origen en el que se basa el nivel.|  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de la jerarquía de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)  
  
  
