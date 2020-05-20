---
title: ConnectModeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
author: rothja
ms.author: jroth
ms.openlocfilehash: 6e78ab5988d88447539da7c492f0b02943693844
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762616"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
Especifica los permisos disponibles para modificar los datos de una [conexión](../../../ado/reference/ado-api/connection-object-ado.md), abrir un [registro](../../../ado/reference/ado-api/record-object-ado.md)o especificar valores para la propiedad [mode](../../../ado/reference/ado-api/mode-property-ado.md) de los objetos **Record** y [Stream](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|Indica permisos de solo lectura.|  
|**adModeReadWrite**|3|Indica permisos de lectura y escritura.|  
|**adModeRecursive**|0x400000|Se usa junto con los demás valores de * \* ShareDeny \* * (**adModeShareDenyNone**, **adModeShareDenyWrite**o **adModeShareDenyRead**) para propagar las restricciones de uso compartido a todos los subregistros del **registro**actual. No tiene ningún efecto si el **registro** no tiene ningún elemento secundario. Si solo se usa con **adModeShareDenyNone** , se genera un error en tiempo de ejecución. Sin embargo, se puede usar con **adModeShareDenyNone** cuando se combina con otros valores. Por ejemplo, puede usar "**adModeRead** o **adModeShareDenyNone** o **adModeRecursive**".|  
|**adModeShareDenyNone**|16|Permite que otros usuarios abran una conexión con cualquier permiso. No se puede negar a los demás el acceso de lectura ni el de escritura.|  
|**adModeShareDenyRead**|4|Impide que otros abran una conexión con permisos de lectura.|  
|**adModeShareDenyWrite**|8|Impide que otros abran una conexión con permisos de escritura.|  
|**adModeShareExclusive**|12|Impide que otros abran una conexión.|  
|**adModeUnknown**|0|Predeterminada. Indica que los permisos todavía no se han establecido o no se pueden determinar.|  
|**adModeWrite**|2|Indica permisos de solo escritura.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO/WFC  
 Paquete: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. ConnectMode. READ|  
|AdoEnums. ConnectMode. READWRITE|  
|(No hay ningún equivalente de AdoEnums. ConnectMode. RECURSIVE)|  
|AdoEnums. ConnectMode. SHAREDENYNONE|  
|AdoEnums. ConnectMode. SHAREDENYREAD|  
|AdoEnums. ConnectMode. SHAREDENYWRITE|  
|AdoEnums. ConnectMode. SHAREEXCLUSIVE|  
|AdoEnums. ConnectMode. UNKNOWN|  
|AdoEnums. ConnectMode. WRITE|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Propiedad Mode (ADO)](../../../ado/reference/ado-api/mode-property-ado.md)|[Open (método) (registro de ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Open (método) (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)|[Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|
