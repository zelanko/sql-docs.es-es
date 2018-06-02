---
title: Archivo de elemento (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb80a091c9b9585a6efc29088d15139db7033efb
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575197"
---
# <a name="file-element-xmla"></a>Elemento File (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Identifica un archivo que va a usar el elemento primario [copia de seguridad](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) o [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) comando, o por el elemento primario [ubicación](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Backup> <!-- or one of the elements listed below in the Element relationships table -->  
   ...  
   <File>...</File>  
   ...  
</Backup>  
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
|Elementos primarios|[Copia de seguridad](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [ubicación](../../../analysis-services/xmla/xml-elements-properties/location-element-xmla.md), [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El **archivo** elemento contiene un nombre de archivo UNC y el elemento primario determina el uso de la **archivo** elemento.  
  
 Para **copia de seguridad** comandos, el **archivo** elemento determina el nombre del archivo de copia de seguridad creado por el **copia de seguridad** comando. Si no se especifica una ruta de acceso como parte del nombre de archivo, la ruta de acceso especificada en el **BackupDir** se utiliza la propiedad de configuración para la instancia de Analysis Services. Si el archivo especificado ya existe, se produce un error a menos que la **AllowOverwrite** elemento del elemento primario **copia de seguridad** comando está establecido en **True**.  
  
 Para **restaurar** comandos, el **archivo** elemento determina el nombre del archivo de copia de seguridad que se restaurarán por la **restaurar** comando.  
  
 Para **ubicación** elementos, el **archivo** elemento describe un archivo de copia de seguridad remoto para un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia que contiene las particiones remotas. Para obtener más información acerca de la copia de seguridad y restaurar las particiones remotas, consulte [realizar copias de seguridad, restaurar y sincronizar bases de datos &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Vea también
 [Elemento AllowOverwrite &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
