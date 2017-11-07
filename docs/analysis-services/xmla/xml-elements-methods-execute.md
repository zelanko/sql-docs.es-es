---
title: "Método Execute (XMLA) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Execute Method
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- EXECUTE
- urn:schemas-microsoft-com:xml-analysis#
- http://schemas.microsoft.com/analysisservices/2003/engine#
- microsoft.xml.analysis.execute
- urn:schemas-microsoft-com:xml-analysis#Execute
helpviewer_keywords:
- Execute method
ms.assetid: 0fff5221-7164-4bbc-ab58-49cf04c52664
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 22bf60ae16e6b4e5f30bf694505e77857b6c0600
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="xml-elements---methods---execute"></a>Ejecutan elementos XML - métodos:
  Envía el XML para los comandos de Analysis (XMLA) a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Están incluidas las solicitudes que conllevan transferencia de datos, como recuperar o actualizar los datos del servidor.  
  
 **Espacio de nombres** urn:schemas-microsoft-com:xml-analysis  
  
 **Acción SOAP** "urn: schemas-microsoft-com-analysis: ejecutar"  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Execute>  
   <Command>...</Command>  
   <Properties>...</Properties>  
   <Parameters>...</Parameters>  
</Execute>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: elemento opcional que aparece una y solo una.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|Ninguno|  
|Elementos secundarios|[Comando](../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md), [parámetros](../../analysis-services/xmla/xml-elements-properties/parameters-element-xmla.md), [propiedades](../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El **Execute** método ejecuta comandos XMLA proporcionados en el **comando** elemento y devuelve cualquier dato resultante mediante XMLA [conjunto de filas](../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md) tipo de datos (de resultados tabulares establece) o el XMLA [MDDataSet](../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md) tipo de datos (para conjuntos de resultados multidimensionales.)  
  
## <a name="example"></a>Ejemplo  
 El ejemplo de código siguiente es un ejemplo de un **Execute** llamada al método que contiene una instrucción SELECT de expresiones multidimensionales (MDX).  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Statement>  
         SELECT [Measures].MEMBERS ON COLUMNS FROM [Adventure Works]  
      </Statement>  
   </Command>  
   <Properties>  
      <PropertyList>  
         <DataSourceInfo>Provider=MSOLAP;Data Source=local;</DataSourceInfo>  
         <Catalog>Adventure Works DW Multidimensional 2012</Catalog>  
         <Format>Multidimensional</Format>  
         <AxisFormat>ClusterFormat</AxisFormat>  
      </PropertyList>  
   </Properties>  
</Execute>  
```  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML &#40; XMLA &#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Detectar método &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [Métodos &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-methods.md)   
 [Elementos XML &#40; XMLA &#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Conjuntos de filas de esquema de Analysis Services](../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  

