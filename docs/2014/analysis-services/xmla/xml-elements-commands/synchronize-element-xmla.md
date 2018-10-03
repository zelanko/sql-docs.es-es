---
title: Elemento Synchronize (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Synchronize Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.synchronize
- urn:schemas-microsoft-com:xml-analysis#Synchronize
- http://schemas.microsoft.com/analysisservices/2003/engine#Synchronize
helpviewer_keywords:
- Synchronize command
ms.assetid: 9401323c-feff-409a-a9da-94aee47e0563
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 13bdb64dbc3ba0b034af3a54ae10a50c403555a7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48225825"
---
# <a name="synchronize-element-xmla"></a>Elemento Synchronize (XMLA)
  Sincroniza un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos con otra base de datos existente.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Synchronize>  
      <Source>...</Source>  
      <SynchronizeSecurity>...</SynchronizeSecurity>  
      <ApplyCompression>...</ApplyCompression>  
      <Locations>...</Locations>  
   </Synchronize>  
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
|Elementos primarios|[Command](../xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[ApplyCompression](../xml-elements-properties/applycompression-element-xmla.md), [ubicaciones](../xml-elements-properties/locations-element-xmla.md), [origen](../xml-elements-properties/source-element-synchronize-xmla.md), [SynchronizeSecurity](../xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 El comando `Synchronize` sincroniza la base de datos de destino con una instancia de origen y con la base de datos especificadas en el elemento `Source`. Opcionalmente, el comando `Synchronize` sincroniza particiones remotas definidas en la base de datos de origen.  
  
 Dependiendo del modo de almacenamiento utilizado por los objetos guardados en el archivo de copia de seguridad, el comando `Synchronize` sincroniza la información tal y como se indica en la tabla siguiente.  
  
|Modo de almacenamiento|Información|  
|------------------|-----------------|  
|OLAP multidimensional (MOLAP)|Datos de origen, agregaciones y metadatos|  
|OLAP híbrido (HOLAP)|Agregaciones y metadatos|  
|OLAP relacional (ROLAP)|Metadatos|  
  
 Durante la ejecución de un comando `Synchronize`, se establece un bloqueo de lectura en la base de datos de origen y un bloqueo de escritura en la base de datos de destino. Ambos bloqueos se liberan una vez se haya completado la ejecución del comando `Synchronize`.  
  
 Para obtener más información acerca de cómo sincronizar las bases de datos, vea [realizar copias de seguridad, restaurar y sincronizar bases de datos &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Elemento de copia de seguridad &#40;XMLA&#41;](backup-element-xmla.md)   
 [Elemento de lote &#40;XMLA&#41;](batch-element-xmla.md)   
 [Elemento en paralelo &#40;XMLA&#41;](../xml-elements-properties/parallel-element-xmla.md)   
 [Elemento restore &#40;XMLA&#41;](restore-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
