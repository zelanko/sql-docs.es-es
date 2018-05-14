---
title: Elemento Create (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb6a4e848b35a31feeef31bb8e304ba43a8577f3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-element-xmla"></a>Elemento Create (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene elementos de Analysis Services Scripting Language (ASSL) utilizados por el **Execute** método para crear objetos en un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Create Scope="enum" AllowOverwrite="boolean">  
      <ParentObject>...</ParentObject>  
      <ObjectDefinition>...</ObjectDefinition>  
   </Create>  
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
|Elementos secundarios|[ObjectDefinition](../../../analysis-services/xmla/xml-elements-properties/objectdefinition-element-xmla.md), [ParentObject](../../../analysis-services/xmla/xml-elements-properties/parentobject-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|AllowOverwrite|Atributo **Boolean** opcional. Si se establece en True, los objetos definidos en el **ObjectDefinition** elemento puede sobrescribir objetos existentes en el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia. Si este atributo se omite o se establece en False, la presencia de un objeto existente genera un error.|  
|Ámbito|Atributo **Enum** opcional. Define la duración de objetos definidos en el elemento **ObjectDefinition** . Si se omite este atributo, los objetos definidos en el **ObjectDefinition** elemento se conservan en el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia. El valor siguiente está disponible:<br /><br /> *Sesión*: los objetos definidos en el **ObjectDefinition** el elemento existe únicamente para la duración del XML de sesión de Analysis (XMLA).<br />                  Tenga en cuenta que, cuando se usa el *sesión* establecer, el **ObjectDefinition** solo puede contener el elemento [dimensión](../../../analysis-services/scripting/objects/dimension-element-assl.md), [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), o [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md) elementos ASSL.|  
  
## <a name="remarks"></a>Comentarios  
 Cada operación **Create** crea un objeto principal bajo un elemento primario proporcionado por el elemento **ParentObject** . Si se omite el objeto primario, se asume que es la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] de destino. Esto genera un error si el elemento primario de un objeto principal no es la instancia de destino.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se crea una base de datos vacía denominada **base de datos de prueba** en un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
```  
  
      <Create xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
   <ObjectDefinition>  
      <Database xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
         <Name>Test Database</Name>  
         <Description>A test database.</Description>  
      </Database>  
   </ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>Vea también  
 [Comandos & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
