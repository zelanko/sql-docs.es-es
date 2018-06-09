---
title: Elemento ALTER (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5ff62bcde0aa40e9bb052691d4d3dee1317c1217
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34574607"
---
# <a name="alter-element-xmla"></a>Elemento Alter (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene elementos de Analysis Services Scripting Language (ASSL) utilizados por el [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método para modificar los objetos en una instancia de Analysis Services.  
  
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
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [ObjectDefinition](../../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|AllowCreate|(Atributo **Boolean** opcional). Indica si deberían crearse los objetos definidos en el comando **Alter** en caso de que no aún no existan.<br /><br /> Si establece en true, los objetos definidos en el **ObjectDefinition** elemento se crean en el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia si aún no existen. En otras palabras, el comando **Alter** se trata como un comando **Create** si los objetos aún no existen en la instancia.<br /><br /> Si este atributo se omite o se establece a **false**, se producirá un error si los objetos aún no existen.|  
|ObjectExpansion|(Atributo **Enum** opcional). Define la extensión de la modificación que va a realizar el método **Execute** .<br /><br /> Si está establecido en *ObjectProperties*, el elemento **ObjectDefinition** debería contener únicamente la definición completa del objeto principal a modificar, incluyendo los objetos secundarios subordinados. Los objetos principales subordinados al objeto que se va a modificar no se modificarán.<br /><br /> Nota: Cuando se usa el *ObjectProperties* establecer con el [ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md) tipo de datos, el [datos](../../../analysis-services/scripting/objects/data-element-assl.md) elemento del asociado [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md) no es necesario especificar los tipos de datos. Si no se especifica, **ClrAssembly** utiliza los archivos existentes.<br /><br /> Si está establecido en *ExpandFull*, el elemento **ObjectDefinition** debería contener no solo la definición completa del objeto a modificar, sino también las definiciones de todos los objetos principales que son descendientes del objeto que se va a modificar.<br /><br /> Nota: La *ExpandFull* configuración no se puede usar con el [Server](../../../analysis-services/scripting/objects/server-element-assl.md) elemento.|  
|Ámbito|(Atributo **Enum** opcional) Define la duración de objetos definido en el elemento **ObjectDefinition** .<br /><br /> Si se establece en *Session*, los objetos definidos en el elemento **ObjectDefinition** solamente existirán durante la sesión XMLA.<br /><br /> Nota: Cuando se usa el *sesión* establecer, el **ObjectDefinition** solo puede contener el elemento [dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md), [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), o [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elementos ASSL.<br /><br /> Si se omite este atributo, los objetos definidos en el **ObjectDefinition** elemento se conservan en el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.|  
  
## <a name="remarks"></a>Notas  
 Cada **Alter** comando cambia la definición de un objeto principal bajo el objeto primario especificado por el [ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md) elemento.  
  
## <a name="see-also"></a>Vea también
 [Comandos &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
