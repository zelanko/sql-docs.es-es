---
title: Elemento ALTER (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Alter Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Alter
- microsoft.xml.analysis.alter
- urn:schemas-microsoft-com:xml-analysis#Alter
helpviewer_keywords:
- Alter command
ms.assetid: 84e58385-c9ba-48fa-a867-94d35b777a56
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 314d1cf2ee33d4c5a17e0a7bee79820593a5fe2c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="alter-element-xmla"></a>Elemento Alter (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene elementos del Lenguaje de scripting de Analysis Services (ASSL) utilizados por el método [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) para modificar objetos en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Alter Scope="enum" AllowCreate="boolean" ObjectExpansion="enum">  
      <Object>...</Object>  
      <ObjectDefinition>...</ObjectDefinition>  
   </Alter>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [ObjectDefinition](../../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Description|  
|---------------|-----------------|  
|AllowCreate|(Atributo **Boolean** opcional). Indica si deberían crearse los objetos definidos en el comando **Alter** en caso de que no aún no existan.<br /><br /> Si establece en true, los objetos definidos en el **ObjectDefinition** elemento se crean en el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia si aún no existen. En otras palabras, el comando **Alter** se trata como un comando **Create** si los objetos aún no existen en la instancia.<br /><br /> Si este atributo se omite o se establece a **false**, se producirá un error si los objetos aún no existen.|  
|ObjectExpansion|(Atributo **Enum** opcional). Define la extensión de la modificación que va a realizar el método **Execute** .<br /><br /> Si está establecido en *ObjectProperties*, el elemento **ObjectDefinition** debería contener únicamente la definición completa del objeto principal a modificar, incluyendo los objetos secundarios subordinados. Los objetos principales subordinados al objeto que se va a modificar no se modificarán.<br /><br /> Nota: Cuando se usa el *ObjectProperties* establecer con el [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) tipo de datos, el [datos](../../../analysis-services/scripting/objects/data-element-assl.md) elemento del asociado [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) no es necesario especificar los tipos de datos. Si no se especifica, **ClrAssembly** utiliza los archivos existentes.<br /><br /> Si está establecido en *ExpandFull*, el elemento **ObjectDefinition** debería contener no solo la definición completa del objeto a modificar, sino también las definiciones de todos los objetos principales que son descendientes del objeto que se va a modificar.<br /><br /> Nota: La *ExpandFull* configuración no se puede usar con el [Server](../../../analysis-services/scripting/objects/server-element-assl.md) elemento.|  
|Ámbito|(Atributo **Enum** opcional) Define la duración de objetos definido en el elemento **ObjectDefinition** .<br /><br /> Si se establece en *Session*, los objetos definidos en el elemento **ObjectDefinition** solamente existirán durante la sesión XMLA.<br /><br /> Nota: Cuando se usa el *sesión* establecer, el **ObjectDefinition** solo puede contener el elemento [dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md), [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), o [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elementos ASSL.<br /><br /> Si se omite este atributo, los objetos definidos en el **ObjectDefinition** elemento se conservan en el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.|  
  
## <a name="remarks"></a>Comentarios  
 Cada **Alter** comando cambia la definición de un objeto principal bajo el objeto primario especificado por el [ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md) elemento.  
  
## <a name="see-also"></a>Vea también  
 [Comandos & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
