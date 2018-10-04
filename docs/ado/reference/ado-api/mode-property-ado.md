---
title: Propiedad Mode (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords:
- Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0fc2a9dffe5dc22c1dadfa075b91d8a6b26215de
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47630963"
---
# <a name="mode-property-ado"></a>Propiedad Mode (ADO)
Indica los permisos disponibles para modificar datos en un [conexión](../../../ado/reference/ado-api/connection-object-ado.md), [registro](../../../ado/reference/ado-api/record-object-ado.md), o [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valor. El valor predeterminado para un **conexión** es **adModeUnknown**. El valor predeterminado para un **registro** objeto es **adModeRead**. El valor predeterminado para un **Stream** asociada a un origen subyacente (abierto con una dirección URL como el origen o como el valor predeterminado **Stream** de un **registro**) es  **adModeRead**. El valor predeterminado para un **Stream** no está asociado con una subyacente (crea una instancia en memoria) de origen es **adModeUnknown**.  
  
## <a name="remarks"></a>Comentarios  
 Utilice la **modo** propiedad para establecer o devolver los permisos de acceso en uso por el proveedor en la conexión actual. Puede establecer el **modo** propiedad solo cuando el **conexión** objeto está cerrado.  
  
 Para un **Stream** objeto, si no se especifica el modo de acceso, se hereda de la fuente utilizada para abrir el **Stream** objeto. Por ejemplo, si un **Stream** se abre desde una **registro** objeto, de forma predeterminada se abre en el mismo modo que el **registro**.  
  
 Esta propiedad es de lectura y escritura mientras el objeto está cerrado y de solo lectura mientras está abierto el objeto.  
  
> [!NOTE]
>  **Uso del servicio de datos remoto** cuando se usa en un cliente **conexión** objeto, el **modo** propiedad solo puede establecerse en **adModeUnknown**.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo IsolationLevel y Mode propiedades (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [Ejemplo IsolationLevel y Mode propiedades (VC ++)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
