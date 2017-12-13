---
title: Elemento Folder (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Folder Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.folder
- http://schemas.microsoft.com/analysisservices/2003/engine#Folder
- urn:schemas-microsoft-com:xml-analysis#Folder
helpviewer_keywords: Folder element
ms.assetid: 87b305b0-57e3-4ec3-9d80-f1bcf3ce7540
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dfb0345491cb1276711581565d91b8f0185bf97c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="folder-element-xmla"></a>Elemento Folder (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Contiene una ubicación de almacenamiento del sistema de archivos que deben actualizarse para un [ubicación](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) elemento durante un [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) o [sincronizar](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Folders>  
   ...  
   <Folder>  
      <Original>...</Original>  
      <New>...</New>  
   </Folder>  
   ...  
</Folders>  
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
|Elementos primarios|[Carpetas](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
|Elementos secundarios|[Nueva](../../../analysis-services/xmla/xml-elements-properties/new-element-xmla.md), [Original](../../../analysis-services/xmla/xml-elements-properties/original-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El elemento **Folder** , si se especifica, cambia las ubicaciones de almacenamiento de objetos contenidos en el archivo de copia de seguridad (para los comandos **Restore** ) o en la base de datos ubicada en la instancia de origen (para los comandos **Synchronize** ) y en los que coinciden el valor del elemento **Original** y el valor del elemento **New** .  
  
 Para obtener más información acerca de la copia de seguridad y restauración de objetos, consulte [realizar copias de seguridad, restauración y sincronizar bases de datos &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Storagelocation, elemento &#40; ASSL &#41;](../../../analysis-services/scripting/properties/storagelocation-element-assl.md)   
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
