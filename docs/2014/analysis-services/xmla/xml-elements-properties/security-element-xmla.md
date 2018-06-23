---
title: Elemento Security (XMLA) | Documentos de Microsoft
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
- Security Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.security
- urn:schemas-microsoft-com:xml-analysis#Security
- http://schemas.microsoft.com/analysisservices/2003/engine#Security
helpviewer_keywords:
- Security element
ms.assetid: 0b601f69-d16d-4d10-9361-b8afaa6ed357
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 4811ae03eb6f30c4b9f4557e791339920161b4ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204247"
---
# <a name="security-element-xmla"></a>Elemento Security (XMLA)
  Especifica cómo hacer una copia o restaurar definiciones de seguridad, como los roles y permisos, durante un [copia de seguridad](../xml-elements-commands/backup-element-xmla.md) o [restaurar](../xml-elements-commands/restore-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <Security>...</Security>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*SkipMembership*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Copia de seguridad](../xml-elements-commands/backup-element-xmla.md), [restaurar](../xml-elements-commands/restore-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El `Security` elemento determina si las definiciones de seguridad, como los roles y permisos, definidas en una [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos se copia o se restauran durante, respectivamente, un `Backup` o `Restore` comando. Este elemento determina también si las cuentas de usuario de Windows y los grupos definidos como miembros de las definiciones de seguridad se incluyen como parte del comando `Backup` o `Restore`.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*SkipMembership*|Incluye las definiciones de seguridad, pero excluye la información de suscripción, durante un comando `Backup` o `Restore`.|  
|*CopyAll*|Incluye las definiciones de seguridad y la información de suscripción durante un comando `Backup` o `Restore`.|  
|*IgnoreSecurity*|Excluye las definiciones de seguridad durante un comando `Backup` o `Restore`.|  
  
## <a name="see-also"></a>Vea también  
 [Elemento SynchronizeSecurity &#40;XMLA&#41;](security-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  