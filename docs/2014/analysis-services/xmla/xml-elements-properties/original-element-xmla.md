---
title: Elemento original (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Original Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.original
- http://schemas.microsoft.com/analysisservices/2003/engine#Original
- urn:schemas-microsoft-com:xml-analysis#Original
helpviewer_keywords:
- Original element
ms.assetid: c98a3700-ac19-4341-85d9-5afedf662601
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b09f2388c47206b1b879a5c8dc98f10a28675342
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48212075"
---
# <a name="original-element-xmla"></a>Elemento Original (XMLA)
  Contiene la ubicación de almacenamiento de sistema de archivos original utilizada por un [carpeta](folder-element-xmla.md) elemento.  
  
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
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Carpeta](folder-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El `Original` elemento contiene una ruta de acceso UNC que se reemplazará por el valor de la [New](new-element-xmla.md) elemento incluido en el elemento primario `Folder` (elemento) para todos los objetos restaurados o sincronizados, respectivamente, durante un [restaurar ](../xml-elements-commands/restore-element-xmla.md) o [Synchronize](../xml-elements-commands/synchronize-element-xmla.md) comando. El valor de este elemento se compara con el valor de la [StorageLocation](../../scripting/properties/storagelocation-element-assl.md) (elemento) para cada cubo, grupo de medida o partición y, si se encuentra una coincidencia, el valor de la `New` elemento se usa para actualizar el `StorageLocation` de la objeto durante la restauración o sincronización.  
  
 Para obtener más información acerca de la copia de seguridad y restauración de objetos, consulte [realizar copias de seguridad, restaurar y sincronizar bases de datos &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
