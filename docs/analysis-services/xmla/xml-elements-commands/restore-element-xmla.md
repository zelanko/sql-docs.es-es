---
title: Elemento restore (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ea1bd6b12c605309f9c6c78151bed08c37149372
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34577018"
---
# <a name="restore-element-xmla"></a>Elemento Restore (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Restaura una base de datos de Analysis Services desde un archivo de copia de seguridad.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Restore>  
      <DatabaseName>...</DatabaseName>  
      <DatabaseID>...</DatabaseID>  
      <File>...</File>  
      <Security>...</Security>  
      <AllowOverwrite>...</AllowOverwrite>  
      <Password>...</Password>  
      <Locations>...</Locations>  
      <DbStorageLocation>...</DbStorageLocation>  
   </Restore>  
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
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[AllowOverwrite](../../../analysis-services/xmla/xml-elements-properties/allowoverwrite-element-xmla.md), [DatabaseName](../../../analysis-services/xmla/xml-elements-properties/databasename-element-xmla.md), [DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md), [archivo](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md), [ubicaciones](../../../analysis-services/xmla/xml-elements-properties/locations-element-xmla.md), [contraseña](../../../analysis-services/xmla/xml-elements-properties/password-element-xmla.md), [Seguridad](../../../analysis-services/xmla/xml-elements-properties/security-element-xmla.md), [DbStorageLocation](../../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)|  
  
## <a name="remarks"></a>Notas  
 El **restaurar** comando restaura un [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos especificada en el **DatabaseName** elemento desde un archivo de copia de seguridad y, opcionalmente, restaurar particiones remotas desde archivos de copia de seguridad remotos.  
  
 Dependiendo del modo de almacenamiento utilizado por los objetos guardados en el archivo de copia de seguridad, el comando **Restore** restaura la información tal y como se indica en la tabla siguiente.  
  
|Modo de almacenamiento|Información|  
|------------------|-----------------|  
|OLAP multidimensional (MOLAP)|Datos de origen, agregaciones y metadatos|  
|OLAP híbrido (HOLAP)|Agregaciones y metadatos|  
|OLAP relacional (ROLAP)|Metadatos|  
  
 Durante una **restaurar** comando, se coloca un bloqueo exclusivo en el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos especificada en el **DatabaseName** elemento. El bloqueo se anula después de que se haya completado la ejecución del comando **Restore** .  
  
 Para obtener más información acerca de la copia de seguridad y restaurar bases de datos, vea [realizar copias de seguridad, restaurar y sincronizar bases de datos &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
> [!IMPORTANT]  
>  Para cada archivo de copia de seguridad, el usuario que ejecuta el comando de restauración debe tener permiso para leer desde la ubicación de la copia de seguridad especificada. Para restaurar una base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que no está instalada en el servidor, el usuario también debe ser miembro del rol de servidor para dicha instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] . Para sobrescribir una base de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , el usuario debe tener uno de los roles siguientes: miembro del rol de servidor para la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o miembro de un rol de base de datos con permisos de Control total (Administrador) en la base de datos que se va a restaurar.  
  
> [!NOTE]  
>  Después de restaurar una base de datos existente, el usuario que restauró la base de datos podría perder el acceso a la base de datos restaurada. Esta pérdida de acceso puede producirse si, en el momento en que se realizó la copia de seguridad, el usuario no era miembro del rol de servidor o no era miembro de rol de base de datos con permisos de Control total (Administrador).  
  
## <a name="see-also"></a>Vea también
 [Elemento de la copia de seguridad &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)   
 [Elemento de lote &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [Elemento en paralelo &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)   
 [Elemento Synchronize &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
