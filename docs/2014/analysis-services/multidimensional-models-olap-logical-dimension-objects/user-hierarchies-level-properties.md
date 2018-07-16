---
title: Propiedades del nivel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
ms.assetid: dabb7335-887b-442a-b67c-4901ba1242b7
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 28c5c9149d1734f410417df1d727b81e6e86ea1a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37288051"
---
# <a name="level-properties"></a>Propiedades del nivel 
  En la siguiente tabla se enumeran y describen las propiedades de un nivel en una jerarquía definida por el usuario.  
  
|Property|Descripción|  
|--------------|-----------------|  
|Descripción|Contiene la descripción del nivel.|  
|HideMemberIf|Indica si un miembro en un nivel debe ocultarse de las aplicaciones cliente y cuándo. Esta propiedad puede tener los valores siguientes:<br /><br /> Never<br /> Los miembros nunca se ocultan. Este es el valor predeterminado.<br /><br /> OnlyChildWithNoName<br /> Se oculta un miembro cuando el miembro es el único elemento secundario de un elemento primario y el nombre del miembro está vacío.<br /><br /> OnlyChildWithParentName<br /> Se oculta un miembro cuando el miembro es el único elemento secundario de un elemento primario y el nombre del miembro es idéntico al del elemento primario.<br /><br /> NoName<br /> Un miembro se oculta cuando el nombre del miembro está vacío.<br /><br /> ParentName<br /> Un miembro se oculta cuando el nombre del miembro es idéntico al del elemento primario.|  
|Id.|Contiene el identificador único (Id.) del nivel.|  
|Nombre|Contiene el nombre descriptivo del nivel. De forma predeterminada, el nombre de un nivel es el mismo que el nombre del atributo de origen.|  
|SourceAttribute|Contiene el nombre del atributo de origen en el que se basa el nivel.|  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de jerarquía de usuario](user-hierarchies-properties.md)  
  
  
