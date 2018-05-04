---
title: Elemento location (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Location Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.location
- urn:schemas-microsoft-com:xml-analysis#Location
- http://schemas.microsoft.com/analysisservices/2003/engine#Location
helpviewer_keywords:
- Location element
ms.assetid: cea5e776-f435-425a-9bce-812d727a2b71
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 628e30402c5922f744235aa7dbcc8da7c423abb9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="location-element-xmla"></a>Elemento Location (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contiene información sobre un servidor remoto para el comando primario [Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [Restore](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)o [Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) .  
  
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
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [Restore](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), [Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|  
|Elementos secundarios|Vea la tabla siguiente.|  
  
|Antecesor o elemento primario|Elemento secundario|  
|------------------------|-------------------|  
|[Copia de seguridad](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|[DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md), [File](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)|  
|[Restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|[ConnectionString](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md), [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md), [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md), [File](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md), [Folders](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
|[Sincronizar](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|[ConnectionString](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md), [DataSourceID](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md), [DataSourceType](../../../analysis-services/xmla/xml-elements-properties/datasourcetype-element-xmla.md), [Folders](../../../analysis-services/xmla/xml-elements-properties/folders-element-xmla.md)|  
  
## <a name="remarks"></a>Comentarios  
 Para **copia de seguridad** comandos, el **ubicación** elemento proporciona información acerca de cómo crear un archivo de copia de seguridad remoto para una instancia remota de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Para **restaurar** comandos, el **ubicación** elemento proporciona información sobre cómo identificar y conectarse a un servidor remoto [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia, así como el archivo de copia de seguridad remoto usado para restaurar remoto particiones en esa instancia remota.  
  
 Para los comandos **Synchronize** , el elemento **Location** describe un origen de datos que va a utilizar la instancia de destino o una instancia remota definida en la instancia de origen que se debe sincronizar con la instancia de destino, dependiendo del valor del elemento **DataSourceType** para el comando primario **Synchronize** .  
  
 Para obtener más información sobre las copias de seguridad y restauraciones de instancias remotas, vea [Copia de seguridad y restauración de objetos (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Backupremotepartitions, elemento & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md)   
 [Propiedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
