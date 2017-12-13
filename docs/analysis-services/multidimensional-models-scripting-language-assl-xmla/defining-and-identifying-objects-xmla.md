---
title: Definir e identificar objetos (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- objects [XML for Analysis]
- identifying objects [XML for Analysis]
- XML for Analysis, objects
- object references [XML for Analysis]
- object identifiers [XML for Analysis]
- object definitions [XML for Analysis]
- XMLA, objects
ms.assetid: 43b65f6d-0123-4556-81f0-c7a0b84361e5
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bb3185b6c95807fa4adb383844a62dcb14342a7c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="defining-and-identifying-objects-xmla"></a>Definir e identificar objetos (XMLA)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Los objetos se identifican en XML para los comandos de Analysis (XMLA) mediante el uso de identificadores de objetos y referencias de objeto y se definen mediante los elementos comandos XMLA de Analysis Services Scripting Language (ASSL).  
  
## <a name="object-identifiers"></a>Identificadores de objetos  
 Un objeto se identifica mediante el identificador único del objeto tal como se define en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los identificadores de objetos se pueden especificar o determinar explícitamente por la instancia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cuando [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea el objeto. Puede usar el [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) método para recuperar los identificadores de objetos en posteriores **Discover** o [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) llamadas al método.  
  
## <a name="object-references"></a>Referencias del objeto  
 Varios comandos XMLA, como [eliminar](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md) o [proceso](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md), utilice una referencia de objeto para hacer referencia a un objeto de manera no ambigua. Una referencia a objetos contiene el identificador de objetos del objeto en el que se ejecuta un comando y los identificadores de objetos de los antecesores para ese objeto. Por ejemplo, la referencia a objetos para una partición contiene el identificador de objetos de la partición, así como los identificadores de objetos del grupo, cubo y base de datos de medida primario de esa partición.  
  
## <a name="object-definitions"></a>Definiciones de objetos  
 El [crear](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md) y [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comandos en XMLA crean o modifican, respectivamente, objetos en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia. Las definiciones de los objetos se representan mediante un [ObjectDefinition](../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md) elemento que contiene los elementos de ASSL. Los identificadores de objeto pueden especificarse explícitamente para los principales y muchos de los objetos secundarios mediante el uso de la [identificador](../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md) elemento. Si el **identificador** no se utiliza el elemento, el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancia proporciona un identificador único, con una convención de nomenclatura que depende del objeto que se trate. Para obtener más información sobre cómo usar el **crear** y **Alter** comandos para definir objetos, consulte [crear y modificar objetos &#40; XMLA &#41; ](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Elemento Object &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)   
 [ParentObject, elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)   
 [Elemento Source &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)   
 [Elemento de destino &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)   
 [Desarrollo con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
