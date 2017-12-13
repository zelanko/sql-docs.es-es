---
title: Elemento DataSourceType (XMLA) | Documentos de Microsoft
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
apiname: DataSourceType Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#DataSourceType
- microsoft.xml.analysis.datasourcetype
- http://schemas.microsoft.com/analysisservices/2003/engine#DataSourceType
helpviewer_keywords: DataSourceType element
ms.assetid: f5a348b1-911b-4139-832e-4bcb6d80a728
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 82f56e57b6576bd94c4ba2f88c53895efcc187c3
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="datasourcetype-element-xmla"></a>Elemento DataSourceType (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Indica si un [ubicación](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) elemento especificado para una [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) o [sincronizar](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md) comando es local o remoto.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Location>  
   ...  
   <DataSourceType>...</DataSourceType>  
   ...  
</Location>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*Remoto*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Ubicación](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El elemento **DataSourceType** determina si el origen de datos definido por el elemento **Location** contiene un origen de datos local o un origen de datos remoto. Para obtener más información acerca de la copia de seguridad y restaurar las particiones remotas, consulte [realizar copias de seguridad, restauración y sincronizar bases de datos &#40; XMLA &#41; ](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Description|  
|-----------|-----------------|  
|*Local*|El elemento **Location** define un origen de datos local. Si se utiliza este valor, los comandos **Restore** y **Synchronize** utilizan la información definida en el elemento **Location** para actualizar el origen de datos, recuperada del archivo de copia de seguridad especificado en el elemento **File** para el comando **Backup** o de la base de datos especificada en el elemento **Source** para el comando **Synchronize** , identificado en el elemento **DataSourceID** del elemento **Location** .<br /><br /> Este valor permite a objetos que utilizan el almacenamiento de OLAP (ROLAP) relacional, después de ser restaurados o sincronizados, utilizar una base de datos diferente para sus datos y metadatos.<br /><br /> Nota: Datos ROLAP, como datos de tablas de dimensiones o tablas de reescritura, no se restaura o sincronizados. Solo se restauran o sincronizan los metadatos para los objetos ROLAP.|  
|*Remoto*|El elemento **Location** define un origen de datos remoto. Si se utiliza este valor, los comandos **Restore** y **Synchronize** utilizan la información definida en el elemento **Location** para restaurar o sincronizar particiones remotas, recuperadas del archivo de copia de seguridad especificado en el elemento **File** del comando **Backup** o de la base de datos especificada en el elemento **Source** para el comando **Synchronize** , a la instancia remota definida en el **DataSourceID** del elemento **Location** .|  
  
## <a name="see-also"></a>Vea también  
 [Elemento ConnectionString &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/connectionstring-element-xmla.md)   
 [DataSourceID, elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/datasourceid-element-xmla.md)   
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
