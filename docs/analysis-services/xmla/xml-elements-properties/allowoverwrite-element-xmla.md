---
title: Elemento AllowOverwrite (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AllowOverwrite Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.allowoverwrite
- urn:schemas-microsoft-com:xml-analysis#EndSession
helpviewer_keywords:
- AllowOverwrite element
ms.assetid: e7e92481-5f29-47f2-9efd-4e5e60c002bb
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c47939bfc376589512fad8d4eb5367c9dc7fe5fb
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="allowoverwrite-element-xmla"></a>Elemento AllowOverwrite (XMLA)
  Determina si el elemento primario [copia de seguridad](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) o [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md) comando intenta sobrescribir el archivo de destino o la base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <AllowOverwrite>...</AllowOverwrite>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Booleano|  
|Valor predeterminado|False|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Copia de seguridad](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Para los comandos **Backup** , el elemento **AllowOverwrite** determina si el comando puede sobrescribir el archivo de copia de seguridad especificado en el elemento **File** .  
  
 Para **restaurar** elementos, el **AllowOverwrite** elemento determina si el comando puede sobrescribir el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos especificada en el **DatabaseName** elemento.  
  
## <a name="see-also"></a>Vea también  
 [DatabaseName, elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/databasename-element-xmla.md)   
 [Elemento File &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/file-element-xmla.md)   
 [Propiedades &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

