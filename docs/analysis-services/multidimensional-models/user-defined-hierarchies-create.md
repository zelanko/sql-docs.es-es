---
title: Crear jerarquías definidas por el usuario | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b577151e7b56b6a952030069997de4a538cf00e5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="user-defined-hierarchies---create"></a>Crear jerarquías definidas por el usuario:
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] le permite crear las jerarquías definidas por el usuario. Una jerarquía es una colección de niveles basados en atributos. Por ejemplo, una jerarquía de tiempo puede contener los niveles año, trimestre, mes, semana y día. En algunas jerarquías, cada atributo de miembro implica únicamente al atributo de miembro que tiene por encima. Esto se conoce a veces como una jerarquía natural. Los usuarios finales pueden utilizar una jerarquía para examinar los datos del cubo. Defina las jerarquías utilizando el panel Jerarquías del Diseñador de dimensiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Al crear una jerarquía definida por el usuario, esta se podría volver *desigual*. En una jerarquía desigual, el miembro primario lógico de al menos un miembro no se encuentra en el nivel que está inmediatamente por encima del miembro. Si tiene una jerarquía desigual, hay valores que controlan si los miembros que faltan están visibles y cómo mostrarlos. Para más información, vea [Jerarquías desiguales](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md).  
  
> [!NOTE]  
>  Para más información sobre los problemas de rendimiento relacionados con el diseño y la configuración de las jerarquías definidas por el usuario, vea la [Guía de rendimiento de SQL Server 2005 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de jerarquía de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Propiedades de nivel - jerarquías de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [Dimensiones de elementos primarios y secundarios](../../analysis-services/multidimensional-models/parent-child-dimension.md)  
  
  
