---
title: Propiedad Mode (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords:
- Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ee4463749e231b6ecd48a1fa24af1a72b3766ef
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="mode-property-ado"></a>Propiedad Mode (ADO)
Indica los permisos disponibles para modificar datos en un [conexión](../../../ado/reference/ado-api/connection-object-ado.md), [registro](../../../ado/reference/ado-api/record-object-ado.md), o [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) valor. El valor predeterminado para un **conexión** es **adModeUnknown**. El valor predeterminado para un **registro** objeto es **adModeRead**. El valor predeterminado para un **flujo** asociada a un origen subyacente (abierto con una dirección URL como el origen o como el valor predeterminado **flujo** de un **registro**) es ** adModeRead**. El valor predeterminado para un **flujo** no esté asociado a una subyacente (crea una instancia en memoria) de origen es **adModeUnknown**.  
  
## <a name="remarks"></a>Comentarios  
 Utilice la **modo** propiedad para establecer o devolver los permisos de acceso en uso por el proveedor en la conexión actual. Puede establecer la **modo** propiedad solo cuando la **conexión** objeto está cerrado.  
  
 Para una **flujo** objeto, si no se especifica el modo de acceso, se hereda del origen utilizado para abrir el **flujo** objeto. Por ejemplo, si un **flujo** se abre desde una **registro** objeto, de forma predeterminada, se abre en el mismo modo que la **registro**.  
  
 Esta propiedad es de lectura y escritura mientras el objeto está cerrado y de sólo lectura mientras el objeto está abierto.  
  
> [!NOTE]
>  **Uso de servicios de datos remoto** cuando se utiliza en un lado del cliente **conexión** objeto, el **modo** propiedad solo puede establecerse en **adModeUnknown**.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto de registro (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo IsolationLevel y Mode propiedades (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [Ejemplo IsolationLevel y Mode propiedades (VC ++)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   

