---
title: "Crear jerarquías definidas por el usuario | Documentos de Microsoft"
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
- user-defined hierarchies [Analysis Services]
ms.assetid: 16715b85-0630-4a8e-99b0-c0d213cade26
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 51e4bcb074da0b11587d8783008fd250fa8867fe
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="user-defined-hierarchies---create"></a>Crear jerarquías definidas por el usuario:
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] le permite crear las jerarquías definidas por el usuario. Una jerarquía es una colección de niveles basados en atributos. Por ejemplo, una jerarquía de tiempo puede contener los niveles año, trimestre, mes, semana y día. En algunas jerarquías, cada atributo de miembro implica únicamente al atributo de miembro que tiene por encima. Esto se conoce a veces como una jerarquía natural. Los usuarios finales pueden utilizar una jerarquía para examinar los datos del cubo. Defina las jerarquías utilizando el panel Jerarquías del Diseñador de dimensiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Al crear una jerarquía definida por el usuario, esta se podría volver *desigual*. En una jerarquía desigual, el miembro primario lógico de al menos un miembro no se encuentra en el nivel que está inmediatamente por encima del miembro. Si tiene una jerarquía desigual, hay valores que controlan si los miembros que faltan están visibles y cómo mostrarlos. Para más información, vea [Jerarquías desiguales](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md).  
  
> [!NOTE]  
>  Para más información sobre los problemas de rendimiento relacionados con el diseño y la configuración de las jerarquías definidas por el usuario, vea la [Guía de rendimiento de SQL Server 2005 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de jerarquía de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Propiedades de nivel - jerarquías de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [Dimensiones de elementos primarios y secundarios](../../analysis-services/multidimensional-models/parent-child-dimension.md)  
  
  

