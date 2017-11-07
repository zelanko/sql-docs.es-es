---
title: "Propiedades - jerarquías de usuario del nivel | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
ms.assetid: dabb7335-887b-442a-b67c-4901ba1242b7
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7fa44b453e1c91d8a43dde01ec582b59f22d3824
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="user-hierarchies---level-properties"></a>Jerarquías de usuario - propiedades de nivel
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
  
  

