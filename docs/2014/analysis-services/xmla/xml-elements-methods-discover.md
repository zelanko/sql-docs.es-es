---
title: Método Discover (XMLA) | Documentos de Microsoft
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
caps.latest.revision: 36
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: ead875bbe88ea71c8741450f8a3127efcf4b313d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197017"
---
# <a name="discover-method-xmla"></a>Método Discover (XMLA)
  Recupera información, como la lista de bases de datos disponibles o los detalles sobre un objeto concreto, desde una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los datos recuperados con el método `Discover` dependen de los valores de los parámetros que se le pasan.  
  
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
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
  
## <a name="remarks"></a>Notas  
 El método `Discover` solicita los metadatos sobre las instancias y objetos [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los metadatos se devuelven utilizando el XMLA [conjunto de filas](xml-data-types/rowset-data-type-xmla.md) tipo de datos.  
  
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
 [Ejecutar el método &#40;XMLA&#41;](xml-elements-methods-execute.md)   
 [Métodos &#40;XMLA&#41;](xml-elements-methods.md)   
 [Elementos XML &#40;XMLA&#41;](../dev-guide/xml-elements-xmla.md)   
 [Conjuntos de filas de esquema de Analysis Services](../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  