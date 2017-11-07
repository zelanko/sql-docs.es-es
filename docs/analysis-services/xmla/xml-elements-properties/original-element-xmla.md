---
title: Elemento original (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Original Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.original
- http://schemas.microsoft.com/analysisservices/2003/engine#Original
- urn:schemas-microsoft-com:xml-analysis#Original
helpviewer_keywords:
- Original element
ms.assetid: c98a3700-ac19-4341-85d9-5afedf662601
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 75a0345459be5e065a7a737b8036e505f799d549
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="original-element-xmla"></a>Elemento Original (XMLA)
  Contiene la ubicación de almacenamiento de sistema de archivos original utilizada por un [carpeta](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Folder>  
   ...  
   <Original>...</Original>  
   ...  
</Folder>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Carpeta](../../../analysis-services/xmla/xml-elements-properties/folder-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El **Original** elemento contiene una ruta de acceso UNC que reemplazarse por el valor de la [New](../../../analysis-services/xmla/xml-elements-properties/new-element-xmla.md) elemento incluido en el elemento primario **carpeta** (elemento) para todos los objetos que se restaura o sincronizados, respectivamente, durante un [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) o [sincronizar](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) comando. El valor de este elemento se compara con el valor de la [StorageLocation](../../../analysis-services/scripting/properties/storagelocation-element-assl.md) (elemento) para cada cubo, grupo de medida o partición y, si se encuentra una coincidencia, el valor de la **New** elemento se utiliza para actualizar la  **StorageLocation** del objeto durante la restauración o sincronización.  
  
 Para obtener más información acerca de la copia de seguridad y restauración de objetos, consulte [realizar copias de seguridad, restauración y sincronizar bases de datos &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

