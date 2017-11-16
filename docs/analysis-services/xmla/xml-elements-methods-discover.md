---
title: "Método Discover (XMLA) | Documentos de Microsoft"
ms.custom: 
ms.date: 09/14/2016
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Discover Method
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#
- http://schemas.microsoft.com/analysisservices/2003/engine#
- microsoft.xml.analysis.discover
- urn:schemas-microsoft-com:xml-analysis#Discover
- Discover
helpviewer_keywords:
- Discover method
ms.assetid: 0eb52d88-c081-416e-a229-610e4373b0b3
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 60a101afa2953d62e2910b4523a0213e4e786490
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="xml-elements---methods---discover"></a>Detección elementos XML - métodos:
  Recupera información, como la lista de bases de datos disponibles o los detalles sobre un objeto concreto, desde una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los datos recuperados con el método **Discover** dependen de los valores de los parámetros que se le pasan.  
  
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
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|Ninguno|  
|Elementos secundarios|[Propiedades](../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md), [RequestType](../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md), [restricciones](../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El **Discover** método solicita los metadatos sobre [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instancias y objetos. Los metadatos se devuelven utilizando el XMLA [conjunto de filas](../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) tipo de datos.  
 
> [!TIP] 
> Si no está familiarizado con los comandos XML, haga clic en la plantilla de consulta XMLA en el **consulta** barra de herramientas en Management Studio, para generar la consulta y agregar parámetros. Para más información, consulte [Use Analysis Services Templates in SQL Server Management Studio](../../analysis-services/instances/use-analysis-services-templates-in-sql-server-management-studio.md). 
  
## <a name="example"></a>Ejemplo  
 En el ejemplo de código siguiente, el cliente envía el **Discover** llamada para solicitar una lista de cubos de la [!INCLUDE[ssAWDWsp](../../includes/ssawdwsp-md.md)] ejemplo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos:  
  
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
 [Tipos de datos XML &#40; XMLA &#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Ejecutar método &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)   
 [Métodos &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods.md)   
 [Elementos XML &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Conjuntos de filas de esquema de Analysis Services](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  

