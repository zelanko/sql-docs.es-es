---
title: Copia de seguridad de elemento (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4e00a4991226779a91e16806dbe15973d946ec69
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38007155"
---
# <a name="backup-element-xmla"></a>Elemento Backup (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Realiza una copia de seguridad de una base de datos de Analysis Services en un archivo de copia de seguridad.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Backup>  
      <Object>...</Object>  
      <File>...</File>  
      <Security>...</Security>  
      <ApplyCompression>...</ApplyCompression>  
      <AllowOverwrite>...</AllowOverwrite>  
      <Password>...</Password>  
      <BackupRemotePartitions>...</BackupRemotePartitions>  
      <Locations>...</Locations>  
   </Backup>  
</Command>  
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
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[AllowOverwrite](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md), [ApplyCompression](../../../analysis-services/xmla/xml-elements-properties/applycompression-element-xmla.md), [BackupRemotePartitions](../../../analysis-services/xmla/xml-elements-properties/backupremotepartitions-element-xmla.md), [archivo](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md), [ubicaciones](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md), [ Objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md), [contraseña](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md), [seguridad](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 El **copia de seguridad** comando realiza una copia del [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos especificada en el [objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) elemento a un archivo de copia de seguridad y, opcionalmente, realiza copias de seguridad de las particiones remotas a los archivos de copia de seguridad remotos. Si el **objeto** elemento hace referencia a un objeto distinto una [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] de base de datos, se produce un error.  
  
 La información de la que hace copia de seguridad el comando **Backup** depende del modo del almacenamiento que utilicen los objetos de la base de datos. La tabla siguiente identifica la información de la que se hace copia de seguridad en función del modo de almacenamiento utilizado.  
  
|Modo de almacenamiento|Información de la que se hace copia de seguridad|  
|------------------|-----------------------------------|  
|OLAP multidimensional (MOLAP)|Datos de origen, agregaciones y metadatos|  
|OLAP híbrido (HOLAP)|Agregaciones y metadatos|  
|OLAP relacional (ROLAP)|Metadatos|  
  
 Durante una **copia de seguridad** comando, se coloca un bloqueo compartido en el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos especificada en el **objeto** elemento. El bloqueo compartido se anula después de que se haya completado la ejecución del comando **Backup** .  
  
 Varios **copia de seguridad** comandos se pueden ejecutar en paralelo, si los comandos están incluidos en el [paralelo](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md) colección de un [Batch](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) comando. La colección **Parallel** permite hacer copia de seguridad de una base de datos al mismo tiempo en varios archivos de copia de seguridad.  
  
 Para obtener más información acerca de la copia de seguridad y restaurar bases de datos, vea [realizar copias de seguridad, restaurar y sincronizar bases de datos &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
> [!IMPORTANT]  
>  Para cada archivo de copia de seguridad, el usuario que ejecuta el comando de copia de seguridad debe tener permiso para escribir en la ubicación de copia de seguridad especificada. Además, el usuario debe tener uno de los roles siguientes: miembro de un rol de servidor para la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o miembro de un rol de base de datos con permisos de Control total (Administrador) en la base de datos de la que se va a hacer una copia de seguridad.  
  
## <a name="see-also"></a>Vea también
 [Elemento restore &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)   
 [Elemento Synchronize &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
