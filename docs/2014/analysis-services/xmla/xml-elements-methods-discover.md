---
title: Método Discover (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Discover Method
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#
- http://schemas.microsoft.com/analysisservices/2003/engine#
- microsoft.xml.analysis.discover
- urn:schemas-microsoft-com:xml-analysis#Discover
- Discover
helpviewer_keywords:
- Discover method
ms.assetid: 0eb52d88-c081-416e-a229-610e4373b0b3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 91ea30a495eb76c22075007f48e3ae721504ef49
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116325"
---
# <a name="discover-method-xmla"></a>Método Discover (XMLA)
  Recupera información, como la lista de bases de datos disponibles o datos sobre un objeto específico, desde una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los datos recuperados con el método `Discover` dependen de los valores de los parámetros que se le pasan.  
  
 **Espacio de nombres** urn:schemas-microsoft-com:xml-analysis  
  
 **Acción SOAP** "urn:schemas-microsoft-com:xml-analysis:Discover"  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Discover>  
   <RequestType>...</RequestType>  
   <Restrictions>...</Restrictions>  
   <Properties>...</Properties>  
</Discover>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|None|  
|Elementos secundarios|[Propiedades](xml-elements-properties/properties-element-xmla.md), [RequestType](xml-elements-properties/type-element-xmla.md), [restricciones](xml-elements-properties/restrictions-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El método `Discover` solicita los metadatos sobre las instancias y objetos [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los metadatos se devuelven utilizando XMLA [conjunto de filas](xml-data-types/rowset-data-type-xmla.md) tipo de datos.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo de código siguiente, el cliente envía la llamada a `Discover` para solicitar una lista de cubos de la base de datos de ejemplo [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>MDSCHEMA_CUBES</RequestType>  
   <Restrictions>  
      <RestrictionList>  
         <CATALOG_NAME>Adventure Works DW Multidimensional 2012</CATALOG_NAME>  
      </RestrictionList>  
   </Restrictions>  
   <Properties>  
      <PropertyList>  
         <DataSourceInfo>Provider=MSOLAP;Data Source=local;</DataSourceInfo>  
         <Catalog>Adventure Works DW Multidimensional 2012</Catalog>  
         <Format>Tabular</Format>  
      </PropertyList>  
   </Properties>  
</Discover>  
```  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML &#40;XMLA&#41;](xml-data-types/xml-data-types-xmla.md)   
 [Método Execute &#40;XMLA&#41;](xml-elements-methods-execute.md)   
 [Métodos &#40;XMLA&#41;](xml-elements-methods.md)   
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [Conjuntos de filas de esquema de Analysis Services](../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
