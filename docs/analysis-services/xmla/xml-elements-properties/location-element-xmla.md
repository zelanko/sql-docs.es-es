---
title: Elemento location (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4953981e7657706a986e9a2407f6786ff676a854
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38004497"
---
# <a name="location-element-xmla"></a>Elemento Location (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene información acerca de un servidor remoto para el elemento primario [copia de seguridad](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), o [Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element relationships table -->  
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
  
## <a name="element-relationships"></a>Relaciones de elementos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Copia de seguridad](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), [sincronizar](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|Elementos secundarios|Vea la tabla siguiente.|  
  
|Antecesor o elemento primario|Elemento secundario|  
|------------------------|-------------------|  
|[Copia de seguridad](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|[DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md), [archivo](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)|  
|[Restauración](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|[ConnectionString](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md), [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md), [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md), [archivo](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md), [carpetas](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
|[Sincronizar](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|[ConnectionString](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md), [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md), [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md), [carpetas](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 Para **copia de seguridad** comandos, el **ubicación** elemento proporciona información sobre cómo crear un archivo de copia de seguridad remoto para una instancia remota de Analysis Services.  
  
 Para **restaurar** comandos, el **ubicación** elemento proporciona información sobre cómo identificar y conectarse a un servidor remoto [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia, así como el archivo de copia de seguridad remoto utilizado para restaurar remoto particiones en esa instancia remota.  
  
 Para los comandos **Synchronize** , el elemento **Location** describe un origen de datos que va a utilizar la instancia de destino o una instancia remota definida en la instancia de origen que se debe sincronizar con la instancia de destino, dependiendo del valor del elemento **DataSourceType** para el comando primario **Synchronize** .  
  
 Para obtener más información acerca de la copia de seguridad y restauraciones de instancias remotas, consulte [copia de seguridad y restauración de objetos (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Vea también
 [Elemento BackupRemotePartitions &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
