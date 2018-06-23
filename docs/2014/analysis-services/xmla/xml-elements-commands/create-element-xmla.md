---
title: Elemento Create (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Create Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Create
- urn:schemas-microsoft-com:xml-analysis#Create
- microsoft.xml.analysis.create
helpviewer_keywords:
- Create command (XMLA)
ms.assetid: a623d362-a1ac-40e4-8816-65fac89cb391
caps.latest.revision: 17
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 19e7673c63d7e305d706efb910222f8ba0da7215
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200810"
---
# <a name="create-element-xmla"></a>Elemento Create (XMLA)
  Contiene elementos de Analysis Services Scripting Language (ASSL) utilizados por el `Execute` método para crear objetos en un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Create Scope="enum" AllowOverwrite="boolean">  
      <ParentObject>...</ParentObject>  
      <ObjectDefinition>...</ObjectDefinition>  
   </Create>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[ObjectDefinition](../xml-elements-properties/objectdefinition-element-xmla.md), [ParentObject](../xml-elements-properties/object-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|AllowOverwrite|Opcional `Boolean` atributo. Si está establecido en True, los objetos definidos en el elemento `ObjectDefinition` pueden sobrescribir objetos existentes en la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Si este atributo se omite o se establece en False, la presencia de un objeto existente genera un error.|  
|Ámbito|Opcional `Enum` atributo. Define la duración de objetos definidos en el elemento `ObjectDefinition`. Si se omite este atributo, los objetos definidos en el elemento `ObjectDefinition` se almacenan en la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Puede disponer de los siguientes valores:<br /><br /> -   *sesión*<br />     Los objetos definidos en el elemento `ObjectDefinition` solamente existen mientras dura la sesión de XML  for Analysis (XMLA). **Nota:** cuando se usa el *sesión* establecer, el `ObjectDefinition` solo puede contener el elemento [dimensión](../../scripting/objects/dimension-element-assl.md), [cubo](../../scripting/objects/cube-element-assl.md), o [MiningModel ](../../scripting/objects/miningmodel-element-assl.md) Elementos ASSL.|  
  
## <a name="remarks"></a>Notas  
 Cada operación `Create` crea un objeto principal bajo un elemento primario proporcionado por el elemento `ParentObject`. Si se omite el objeto primario, se asume que es la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] de destino. Esto genera un error si el elemento primario de un objeto principal no es la instancia de destino.  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se crea una base de datos vacía denominada `Test Database` en una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
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
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  