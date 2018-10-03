---
title: Elemento location (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Location Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.location
- urn:schemas-microsoft-com:xml-analysis#Location
- http://schemas.microsoft.com/analysisservices/2003/engine#Location
helpviewer_keywords:
- Location element
ms.assetid: cea5e776-f435-425a-9bce-812d727a2b71
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a0277ab50eb7390d3272c309df8dc865ff088c89
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48107617"
---
# <a name="location-element-xmla"></a>Elemento Location (XMLA)
  Contiene información acerca de un servidor remoto para el elemento primario [copia de seguridad](../xml-elements-commands/backup-element-xmla.md), [restaurar](../xml-elements-commands/restore-element-xmla.md), o [Synchronize](../xml-elements-commands/synchronize-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Location>  
```  
  
```  
  
<File>...</File> <!-- for Backup and Restore only -->  
<DataSourceID>...</DataSourceID>  
<DataSourceType>...</DataSourceType> <!-- for Restore and Synchronize only -->  
<ConnectionString>...</ConnectionString> <!-- for Restore and Synchronize only -->  
<Folders>...</Folders> <!-- for Restore and Synchronize only -->  
```  
  
```  
  
   </Location>  
   ...  
</Backup>  
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
|Elementos primarios|[Copia de seguridad](../xml-elements-commands/backup-element-xmla.md), [restaurar](../xml-elements-commands/restore-element-xmla.md), [sincronizar](../xml-elements-commands/synchronize-element-xmla.md)|  
  
## <a name="child-elements"></a>Elementos secundarios  
  
|Antecesor o elemento primario|Elemento secundario|  
|------------------------|-------------------|  
|[Copia de seguridad](id-element-xmla.md), [archivo](file-element-xmla.md)|  
|[Restaurar](connectionstring-element-xmla.md), [DataSourceID](datasourceid-element-xmla.md), [DataSourceType](type-element-xmla.md), [archivo](file-element-xmla.md), [carpetas](folders-element-xmla.md)|  
|[Sincronizar](../xml-elements-commands/synchronize-element-xmla.md)|[ConnectionString](connectionstring-element-xmla.md), [DataSourceID](datasourceid-element-xmla.md), [DataSourceType](type-element-xmla.md), [carpetas](folders-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 Para `Backup` comandos, el `Location` elemento proporciona información sobre cómo crear un archivo de copia de seguridad remoto para una instancia remota de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Para los comandos `Restore`, el elemento `Location` proporciona información sobre cómo identificar y conectar con una instancia remota de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], así como el archivo de copia de seguridad remoto utilizado para restaurar las particiones remotas en esa instancia remota.  
  
 Para los comandos `Synchronize`, el elemento `Location` describe un origen de datos que va a utilizar la instancia de destino o una instancia remota definida en la instancia de origen que se debe sincronizar con la instancia de destino, dependiendo del valor del elemento `DataSourceType` para el comando primario `Synchronize`.  
  
 Para obtener más información acerca de la copia de seguridad y restauraciones de instancias remotas, consulte [copia de seguridad y restauración de objetos (XMLA)](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Elemento BackupRemotePartitions &#40;XMLA&#41;](backupremotepartitions-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
