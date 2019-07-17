---
title: Crear jerarquías definidas por el usuario | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f6ca49e3a7714134d554538ae4f37e267999f2c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208412"
---
# <a name="user-defined-hierarchies---create"></a>Jerarquías definidas por el usuario: Crear
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] le permite crear las jerarquías definidas por el usuario. Una jerarquía es una colección de niveles basados en atributos. Por ejemplo, una jerarquía de tiempo puede contener los niveles año, trimestre, mes, semana y día. En algunas jerarquías, cada atributo de miembro implica únicamente al atributo de miembro que tiene por encima. Esto se conoce a veces como una jerarquía natural. Los usuarios finales pueden utilizar una jerarquía para examinar los datos del cubo. Defina las jerarquías utilizando el panel Jerarquías del Diseñador de dimensiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Al crear una jerarquía definida por el usuario, esta se podría volver *desigual*. En una jerarquía desigual, el miembro primario lógico de al menos un miembro no se encuentra en el nivel que está inmediatamente por encima del miembro. Si tiene una jerarquía desigual, hay valores que controlan si los miembros que faltan están visibles y cómo mostrarlos. Para más información, vea [Jerarquías desiguales](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md).  
  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de jerarquía de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Propiedades de nivel: Jerarquías de usuario](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [Dimensiones de elementos primarios y secundarios](../../analysis-services/multidimensional-models/parent-child-dimension.md)  
  
  
