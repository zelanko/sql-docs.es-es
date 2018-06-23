---
title: Elemento DataSourceType (XMLA) | Documentos de Microsoft
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
- DataSourceType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DataSourceType
- microsoft.xml.analysis.datasourcetype
- http://schemas.microsoft.com/analysisservices/2003/engine#DataSourceType
helpviewer_keywords:
- DataSourceType element
ms.assetid: f5a348b1-911b-4139-832e-4bcb6d80a728
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: cc083742521abfe9114ea474fe0987861d12c04e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112535"
---
# <a name="datasourcetype-element-xmla"></a>Elemento DataSourceType (XMLA)
  Indica si un [ubicación](location-element-xmla.md) elemento especificado para una [restaurar](../xml-elements-commands/restore-element-xmla.md) o [sincronizar](../xml-elements-commands/synchronize-element-xmla.md) comando es local o remoto.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Location>  
   ...  
   <DataSourceType>...</DataSourceType>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Remoto*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Ubicación](location-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El elemento `DataSourceType` determina si el origen de datos definido por el elemento `Location` contiene un origen de datos local o un origen de datos remoto. Para obtener más información acerca de la copia de seguridad y restaurar las particiones remotas, consulte [realizar copias de seguridad, restaurar y sincronizar bases de datos &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Local*|El elemento `Location` define un origen de datos local. Si se utiliza este valor, los comandos `Restore` y `Synchronize` utilizan la información definida en el elemento `Location` para actualizar el origen de datos, recuperada del archivo de copia de seguridad especificado en el elemento `File` para el comando `Backup` o de la base de datos especificada en el elemento `Source` para el comando `Synchronize`, identificado en el elemento `DataSourceID` del elemento `Location`.<br /><br /> Este valor permite a objetos que utilizan el almacenamiento de OLAP (ROLAP) relacional, después de ser restaurados o sincronizados, utilizar una base de datos diferente para sus datos y metadatos. **Nota:** datos ROLAP, como datos de tablas de dimensiones o tablas de reescritura, no es restaurados o sincronizados. Solo se restauran o sincronizan los metadatos para los objetos ROLAP.|  
|*Remoto*|El elemento `Location` define un origen de datos remoto. Si se utiliza este valor, los comandos `Restore` y `Synchronize` utilizan la información definida en el elemento `Location` para restaurar o sincronizar particiones remotas, recuperadas del archivo de copia de seguridad especificado en el elemento `File` del comando `Backup` o de la base de datos especificada en el elemento `Source` para el comando `Synchronize`, a la instancia remota definida en el `DataSourceID` del elemento `Location`.|  
  
## <a name="see-also"></a>Vea también  
 [Elemento ConnectionString &#40;XMLA&#41;](connectionstring-element-xmla.md)   
 [Elemento DataSourceID &#40;XMLA&#41;](id-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  