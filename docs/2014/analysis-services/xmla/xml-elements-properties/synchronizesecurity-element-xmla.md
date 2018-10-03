---
title: Elemento SynchronizeSecurity (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- SynchronizeSecurity Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.synchronizesecurity
- http://schemas.microsoft.com/analysisservices/2003/engine#SynchronizeSecurity
- urn:schemas-microsoft-com:xml-analysis#SynchronizeSecurity
helpviewer_keywords:
- SynchronizeSecurity element
ms.assetid: d37dbb95-f4a4-44ac-8eb9-f661d5bb5018
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 95e43831854720e8a2525edae06165334443dad3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224550"
---
# <a name="synchronizesecurity-element-xmla"></a>Elemento SynchronizeSecurity (XMLA)
  Especifica cómo sincronizar definiciones de seguridad, como roles y permisos, durante un [Synchronize](../xml-elements-commands/synchronize-element-xmla.md) comando.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Synchronize>  
   ...  
   <SynchronizeSecurity>...</SynchronizeSecurity>  
   ...  
</Synchronize>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|*skipMembership*|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Sincronizar](../xml-elements-commands/synchronize-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El `Security` elemento determina si las definiciones de seguridad, como roles y permisos, definen en un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos se sincronizan durante un `Synchronize` comando. Este elemento determina también si las cuentas de usuario de Windows y los grupos definidos como miembros de las definiciones de seguridad se incluyen como parte del comando `Synchronize`.  
  
 El valor de este elemento se limita a una de las cadenas enumeradas en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*skipMembership*|Incluye las definiciones de seguridad, pero excluye la información de suscripción, durante un comando `Synchronize`.|  
|*CopyAll*|Incluye las definiciones de seguridad y la información de suscripción durante un comando `Synchronize`.|  
|*IgnoreSecurity*|Excluye las definiciones de seguridad durante un comando `Synchronize`.|  
  
## <a name="see-also"></a>Vea también  
 [Elemento de seguridad &#40;XMLA&#41;](security-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
