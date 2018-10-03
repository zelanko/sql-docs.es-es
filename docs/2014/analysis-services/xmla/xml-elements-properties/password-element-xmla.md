---
title: Elemento Password (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Password Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Password
- urn:schemas-microsoft-com:xml-analysis#Password
- microsoft.xml.analysis.password
helpviewer_keywords:
- Password element
ms.assetid: 8a0603bd-f6a1-4b86-84f1-c83d0b03951b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a72d111dd6bccec8b6b40440a0e40e5a6669d87e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159185"
---
# <a name="password-element-xmla"></a>Elemento Password (XMLA)
  Determina la contraseña que va a usar el elemento primario [copia de seguridad](../xml-elements-commands/backup-element-xmla.md) o [restaurar](../xml-elements-commands/restore-element-xmla.md) comando para cifrar o descifrar un archivo de copia de seguridad.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Backup> <!-- or Restore -->  
   ...  
   <Password>...</Password>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Copia de seguridad](../xml-elements-commands/backup-element-xmla.md), [restaurar](../xml-elements-commands/restore-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 Para los comandos `Backup`, si el elemento `Password` no está incluido o contiene una cadena vacía, no se cifra el archivo de copia de seguridad.  
  
 Para los comandos `Restore`, si el elemento `Password` no está incluido o contiene una cadena vacía y se intenta restaurar un archivo de copia de seguridad cifrado, se producirá un error.  
  
 Si los elementos `Location` están incluidos en un comando `Backup` o en un comando `Restore`, el mismo elemento `Password` se utiliza tanto para los archivos de copia de seguridad como para los archivos de copia de seguridad remota. Para obtener más información acerca de los archivos de copia de seguridad remotos, consulte [realizar copias de seguridad, restaurar y sincronizar bases de datos &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Elemento location &#40;XMLA&#41;](location-element-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
