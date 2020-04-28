---
title: Mode (propiedad) (ADO) | Microsoft Docs
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
ms.openlocfilehash: bc5b2e2bce410309656bad5591a3df90781cc8bc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932223"
---
# <a name="mode-property-ado"></a>Propiedad Mode (ADO)
Indica los permisos disponibles para modificar los datos de un objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md), [registro](../../../ado/reference/ado-api/record-object-ado.md)o [secuencia](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de [ConnectModeEnum](../../../ado/reference/ado-api/connectmodeenum.md) . El valor predeterminado de una **conexión** es **adModeUnknown**. El valor predeterminado de un objeto de **registro** es **adModeRead**. El valor predeterminado de una **secuencia** asociada a un origen subyacente (abierto con una dirección URL como origen o como la **secuencia** predeterminada de un **registro**) es **adModeRead**. El valor predeterminado de una **secuencia** que no está asociada a un origen subyacente (con instancias en memoria) es **adModeUnknown**.  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **mode** para establecer o devolver los permisos de acceso que utiliza el proveedor en la conexión actual. Solo puede establecer la propiedad **mode** cuando el objeto de **conexión** está cerrado.  
  
 Para un objeto de **secuencia** , si no se especifica el modo de acceso, se hereda del origen que se usa para abrir el objeto de **secuencia** . Por ejemplo, si se abre un **flujo** desde un objeto de **registro** , se abre de forma predeterminada en el mismo modo que el **registro**.  
  
 Esta propiedad es de lectura/escritura mientras el objeto está cerrado y es de solo lectura mientras el objeto está abierto.  
  
> [!NOTE]
>  **Uso del servicio de datos remotos** Cuando se usa en un objeto de **conexión** del lado cliente, la propiedad **mode** solo se puede establecer en **adModeUnknown**.  
  
## <a name="applies-to"></a>Se aplica a  
  
||||  
|-|-|-|  
|[Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|[Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades IsolationLevel y MODE (VB)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [Ejemplo de las propiedades IsolationLevel y MODE (VC + +)](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
