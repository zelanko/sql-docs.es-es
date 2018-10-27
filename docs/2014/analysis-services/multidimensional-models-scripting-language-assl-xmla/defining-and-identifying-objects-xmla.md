---
title: Definir e identificar objetos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- identifying objects [XML for Analysis]
- XML for Analysis, objects
- object references [XML for Analysis]
- object identifiers [XML for Analysis]
- object definitions [XML for Analysis]
- XMLA, objects
ms.assetid: 43b65f6d-0123-4556-81f0-c7a0b84361e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 595a792e515e862297389faccc324fff8727b8da
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147990"
---
# <a name="defining-and-identifying-objects-xmla"></a>Definir e identificar objetos (XMLA)
  Los objetos se identifican en los comandos XML for Analysis (XMLA) mediante identificadores de objetos y referencias a objetos, y se definen mediante los elementos ASSL (Analysis Services Scripting Language) de los comandos XMLA.  
  
## <a name="object-identifiers"></a>Identificadores de objetos  
 Un objeto se identifica mediante el identificador único del objeto tal como se define en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los identificadores de objetos se pueden especificar o determinar explícitamente por la instancia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cuando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea el objeto. Puede usar el [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) método para recuperar los identificadores de objetos para posterior `Discover` o [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) llamadas al método.  
  
## <a name="object-references"></a>Referencias del objeto  
 Varios comandos XMLA, como [eliminar](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla) o [proceso](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla), usar una referencia de objeto para hacer referencia a un objeto de forma no ambigua. Una referencia a objetos contiene el identificador de objetos del objeto en el que se ejecuta un comando y los identificadores de objetos de los antecesores para ese objeto. Por ejemplo, la referencia a objetos para una partición contiene el identificador de objetos de la partición, así como los identificadores de objetos del grupo, cubo y base de datos de medida primario de esa partición.  
  
## <a name="object-definitions"></a>Definiciones de objetos  
 El [crear](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) y [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) comandos en XMLA crean o modifican, respectivamente, los objetos en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia. Las definiciones de esos objetos se representan mediante un [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) elemento que contiene los elementos de ASSL. Los identificadores de objeto pueden especificarse explícitamente para todas las principales y muchos de los objetos secundarios mediante el uso de la [ID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) elemento. Si no se usa el elemento `ID`, la instancia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona un identificador único, con una convención de nomenclatura que depende del objeto que se va a identificar. Para obtener más información sobre cómo usar el `Create` y `Alter` comandos para definir objetos, consulte [crear y modificar objetos &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
## <a name="see-also"></a>Vea también  
 [Elemento de objeto &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Elemento ParentObject &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Elemento Source &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)   
 [Elemento Target &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)   
 [Desarrollo con XMLA en Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
