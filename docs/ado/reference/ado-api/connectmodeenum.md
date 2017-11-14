---
title: ConnectModeEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bc9a29f1f46ab56a87b318761b4b0809fd76e6fd
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="connectmodeenum"></a>ConnectModeEnum
Especifica los permisos disponibles para modificar datos en un [conexión](../../../ado/reference/ado-api/connection-object-ado.md), abra un [registro](../../../ado/reference/ado-api/record-object-ado.md), o especificar valores para la [modo](../../../ado/reference/ado-api/mode-property-ado.md) propiedad de la  **Registro** y [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objetos.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|Indica los permisos de solo lectura.|  
|**adModeReadWrite**|3|Indica los permisos de lectura/escritura.|  
|**adModeRecursive**|0x400000|Usar junto con las demás  *\*ShareDeny\**  valores (**adModeShareDenyNone**, **adModeShareDenyWrite**, o **adModeShareDenyRead**) para propagar restricciones de uso compartido para todos los registros secundarios del elemento actual **registro**. No tiene ningún efecto si la **registro** no tiene ningún elemento secundario. Se genera un error de tiempo de ejecución si se utiliza con **adModeShareDenyNone** solo. Sin embargo, puede utilizarse con **adModeShareDenyNone** cuando se combina con otros valores. Por ejemplo, puede usar "**adModeRead** o **adModeShareDenyNone** o **adModeRecursive**".|  
|**adModeShareDenyNone**|16|Permite a otros usuarios abrir una conexión con los permisos. No se puede negar a los demás el acceso de lectura ni el de escritura.|  
|**adModeShareDenyRead**|4|Se evita que otros puedan abrir una conexión con permisos de lectura.|  
|**adModeShareDenyWrite**|8|Se evita que otros puedan abrir una conexión con permisos de escritura.|  
|**adModeShareExclusive**|12|Se evita que otros puedan abrir una conexión.|  
|**adModeUnknown**|0|Predeterminado: Indica que los permisos no se ha establecido o no se puede determinar.|  
|**adModeWrite**|2|Indica los permisos de solo escritura.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
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

