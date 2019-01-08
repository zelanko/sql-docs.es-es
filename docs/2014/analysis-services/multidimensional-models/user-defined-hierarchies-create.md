---
title: Crear jerarquías definidas por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined hierarchies [Analysis Services]
ms.assetid: 16715b85-0630-4a8e-99b0-c0d213cade26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1fc304afad2b125d7b6a25dcd9eb7721ec6a793f
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53377337"
---
# <a name="create-user-defined-hierarchies"></a>Crear jerarquías definidas por el usuario
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] le permite crear las jerarquías definidas por el usuario. Una jerarquía es una colección de niveles basados en atributos. Por ejemplo, una jerarquía de tiempo puede contener los niveles año, trimestre, mes, semana y día. En algunas jerarquías, cada atributo de miembro implica únicamente al atributo de miembro que tiene por encima. Esto se conoce a veces como una jerarquía natural. Los usuarios finales pueden utilizar una jerarquía para examinar los datos del cubo. Defina las jerarquías utilizando el panel Jerarquías del Diseñador de dimensiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Al crear una jerarquía definida por el usuario, esta se podría volver *desigual*. En una jerarquía desigual, el miembro primario lógico de al menos un miembro no se encuentra en el nivel que está inmediatamente por encima del miembro. Si tiene una jerarquía desigual, hay valores que controlan si los miembros que faltan están visibles y cómo mostrarlos. Para más información, vea [Jerarquías desiguales](user-defined-hierarchies-ragged-hierarchies.md).  
  
> [!NOTE]  
>  Para más información sobre los problemas de rendimiento relacionados con el diseño y la configuración de las jerarquías definidas por el usuario, vea la [Guía de rendimiento de SQL Server 2005 Analysis Services](https://go.microsoft.com/fwlink/?LinkId=81621).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de jerarquía de usuario](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [Propiedades del nivel &#91;eliminado&#93;](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [Jerarquía de elementos primarios y secundarios](parent-child-dimension.md)  
  
  
