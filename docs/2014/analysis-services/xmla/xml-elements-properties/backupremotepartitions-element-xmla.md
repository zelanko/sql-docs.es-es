---
title: Elemento BackupRemotePartitions (XMLA) | Microsoft Docs
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
- BackupRemotePartitions Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.backupremotepartitions
- http://schemas.microsoft.com/analysisservices/2003/engine#BackupRemotePartitions
- urn:schemas-microsoft-com:xml-analysis#BackupRemotePartitions
helpviewer_keywords:
- BackupRemotePartitions element
ms.assetid: bd68bcf9-b324-4fa8-b6e5-1f5531f9992c
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d7cc7ccb441995d1c4aa3b22cccefcdc5224e486
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200075"
---
# <a name="backupremotepartitions-element-xmla"></a>Elemento BackupRemotePartitions (XMLA)
  Determina si el elemento primario [copia de seguridad](../xml-elements-commands/backup-element-xmla.md) comando realiza una copia de las particiones remotas asociadas al objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Backup>  
   ...  
   <BackupRemotePartitions>...</BackupRemotePartitions>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Boolean|  
|Valor predeterminado|False|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Copia de seguridad](../xml-elements-commands/backup-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Si `BackupRemotePartitions` se establece en `True`, se debe incluir un elemento `Locations` con uno o más elementos `Location` en el comando `Backup`, o se produce un error. Para obtener más información acerca de la copia de seguridad y restaurar particiones remotas, consulte [realizar copias de seguridad, restaurar y sincronizar bases de datos &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Elemento Locations &#40;XMLA&#41;](locations-element-xmla.md)   
 [Elemento location &#40;XMLA&#41;](location-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
