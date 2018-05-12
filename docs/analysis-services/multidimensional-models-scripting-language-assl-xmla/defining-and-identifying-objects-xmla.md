---
title: Definir e identificar objetos (XMLA) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7b3db6fdcd8d9e6bd604d310f8d7858a4a91180e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="defining-and-identifying-objects-xmla"></a>Definir e identificar objetos (XMLA)
  Los objetos se identifican en los comandos XML for Analysis (XMLA) mediante identificadores de objetos y referencias a objetos, y se definen mediante los elementos ASSL (Analysis Services Scripting Language) de los comandos XMLA.  
  
## <a name="object-identifiers"></a>Identificadores de objetos  
 Un objeto se identifica mediante el identificador único del objeto tal como se define en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los identificadores de objetos se pueden especificar o determinar explícitamente por la instancia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cuando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea el objeto. Puede usar el [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) método para recuperar los identificadores de objetos en posteriores **Discover** o [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) llamadas al método.  
  
## <a name="object-references"></a>Referencias del objeto  
 Varios comandos XMLA, como [eliminar](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md) o [proceso](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md), utilice una referencia de objeto para hacer referencia a un objeto de manera no ambigua. Una referencia a objetos contiene el identificador de objetos del objeto en el que se ejecuta un comando y los identificadores de objetos de los antecesores para ese objeto. Por ejemplo, la referencia a objetos para una partición contiene el identificador de objetos de la partición, así como los identificadores de objetos del grupo, cubo y base de datos de medida primario de esa partición.  
  
## <a name="object-definitions"></a>Definiciones de objetos  
 El [crear](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md) y [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comandos en XMLA crean o modifican, respectivamente, objetos en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia. Las definiciones de los objetos se representan mediante un [ObjectDefinition](../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md) elemento que contiene los elementos de ASSL. Los identificadores de objeto pueden especificarse explícitamente para los principales y muchos de los objetos secundarios mediante el uso de la [identificador](../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md) elemento. Si el **identificador** no se utiliza el elemento, el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia proporciona un identificador único, con una convención de nomenclatura que depende del objeto que se trate. Para obtener más información sobre cómo usar el **crear** y **Alter** comandos para definir objetos, consulte [crear y modificar objetos &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Elemento Object & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [Elemento ParentObject &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)   
 [Elemento Source &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)   
 [Elemento de destino & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)   
 [Desarrollar con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
