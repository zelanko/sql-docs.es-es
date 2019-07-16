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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: debf6f9dc4ac1326caf9fbf32b65f15f34a19094
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933457"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
Especifica los permisos disponibles para modificar datos en un [conexión](../../../ado/reference/ado-api/connection-object-ado.md), abra un [registro](../../../ado/reference/ado-api/record-object-ado.md), o especificar valores para el [modo](../../../ado/reference/ado-api/mode-property-ado.md) propiedad de la  **Registro** y [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objetos.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|Indica los permisos de solo lectura.|  
|**adModeReadWrite**|3|Indica los permisos de lectura/escritura.|  
|**adModeRecursive**|0x400000|Usar junto con las demás *\*ShareDeny\** valores (**adModeShareDenyNone**, **adModeShareDenyWrite**, o **adModeShareDenyRead**) para propagar restricciones de uso compartido a todos los registros secundarios del elemento actual **registro**. No tiene ningún efecto si la **registro** no tiene ningún elemento secundario. Se genera un error de tiempo de ejecución si se usa con **adModeShareDenyNone** solo. Sin embargo, puede utilizarse con **adModeShareDenyNone** cuando se combina con otros valores. Por ejemplo, puede usar "**adModeRead** o **adModeShareDenyNone** o **adModeRecursive**".|  
|**adModeShareDenyNone**|16|Permite a otros usuarios abrir una conexión con los permisos. No se puede negar a los demás el acceso de lectura ni el de escritura.|  
|**adModeShareDenyRead**|4|Impide que otros usuarios abrir una conexión con permisos de lectura.|  
|**adModeShareDenyWrite**|8|Impide que otros usuarios abrir una conexión con permisos de escritura.|  
|**adModeShareExclusive**|12|Impide que otros usuarios abrir una conexión.|  
|**adModeUnknown**|0|Predeterminado: Indica que los permisos no se ha establecido o no se puede determinar.|  
|**adModeWrite**|2|Indica los permisos de solo escritura.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ConnectMode.READ|  
|AdoEnums.ConnectMode.READWRITE|  
|(No hay ningún equivalente de AdoEnums.ConnectMode.RECURSIVE)|  
|AdoEnums.ConnectMode.SHAREDENYNONE|  
|AdoEnums.ConnectMode.SHAREDENYREAD|  
|AdoEnums.ConnectMode.SHAREDENYWRITE|  
|AdoEnums.ConnectMode.SHAREEXCLUSIVE|  
|AdoEnums.ConnectMode.UNKNOWN|  
|AdoEnums.ConnectMode.WRITE|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Propiedad Mode (ADO)](../../../ado/reference/ado-api/mode-property-ado.md)|[Open (método) (registro de ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Open (método) (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)|[Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|
