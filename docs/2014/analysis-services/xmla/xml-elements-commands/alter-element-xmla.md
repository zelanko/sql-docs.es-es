---
title: Elemento ALTER (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Alter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Alter
- microsoft.xml.analysis.alter
- urn:schemas-microsoft-com:xml-analysis#Alter
helpviewer_keywords:
- Alter command
ms.assetid: 84e58385-c9ba-48fa-a867-94d35b777a56
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a9bdf13c64834100db14357a5a0ac7f47a6f9bf3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205795"
---
# <a name="alter-element-xmla"></a>Elemento Alter (XMLA)
  Contiene elementos de Analysis Services Scripting Language (ASSL) utilizados por el [Execute](../xml-elements-methods-execute.md) método para modificar objetos en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
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
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Objeto](../xml-elements-properties/object-element-xmla.md), [ObjectDefinition](../xml-elements-properties/objectdefinition-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|AllowCreate|(Atributo `Boolean` opcional). Indica si deberían crearse los objetos definidos en el comando `Alter` en caso de que no aún no existan.<br /><br /> Si está establecido en true, los objetos definidos en el elemento `ObjectDefinition` se crean en la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] si aún no existen. En otras palabras, el comando `Alter` se trata como un comando `Create` si los objetos aún no existen en la instancia.<br /><br /> Si este atributo se omite o se establece a `false`, se producirá un error si los objetos aún no existen.|  
|ObjectExpansion|(Atributo `Enum` opcional). Define la extensión de la modificación que va a realizar el método `Execute`.<br /><br /> Si establece en *ObjectProperties*, el `ObjectDefinition` elemento debería contener únicamente la definición completa del objeto principal a modificar, incluyendo los objetos secundarios subordinados. Los objetos principales subordinados al objeto que se va a modificar no se modificarán. **Nota:** cuando se usa el *ObjectProperties* establecer con el [ClrAssembly](../../scripting/data-type/assembly-data-type-assl.md) tipo de datos, el [datos](../../scripting/objects/data-element-assl.md) elemento asociado [ ClrAssemblyFile](../../scripting/data-type/clrassemblyfile-data-type-assl.md) no deben especificarse los tipos de datos. Si no se especifica, `ClrAssembly` utiliza los archivos existentes. <br /><br /> Si establece en *ExpandFull*, el `ObjectDefinition` elemento debería contener no solo la definición del objeto que se va a modificar, sino también las definiciones de todos los objetos principales que son descendientes del objeto a modificar. **Nota:** el *ExpandFull* no se puede usar con el [Server](../../scripting/objects/server-element-assl.md) elemento.|  
|Ámbito|(Atributo `Enum` opcional) Define la duración de objetos definido en el elemento `ObjectDefinition`.<br /><br /> Si establece en *sesión*, los objetos definidos en el `ObjectDefinition` elemento existen mientras dura la sesión XMLA. **Nota:** cuando se usa el *sesión* establecimiento, el `ObjectDefinition` solo puede contener el elemento [dimensión](../../scripting/objects/dimension-element-assl.md), [cubo](../../scripting/objects/cube-element-assl.md), o [MiningModel ](../../scripting/objects/miningmodel-element-assl.md) Elementos ASSL. <br /><br /> Si se omite este atributo, los objetos definidos en el elemento `ObjectDefinition` se almacenan en la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
  
## <a name="remarks"></a>Comentarios  
 Cada `Alter` comando cambia la definición de un objeto principal bajo el objeto primario especificado por el [ParentObject](../xml-elements-properties/parentobject-element-xmla.md) elemento.  
  
## <a name="see-also"></a>Vea también  
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
