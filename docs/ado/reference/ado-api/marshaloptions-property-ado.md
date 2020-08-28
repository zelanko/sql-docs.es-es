---
description: Propiedad MarshalOptions (ADO)
title: MarshalOptions (propiedad) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MarshalOptions
helpviewer_keywords:
- MarshalOptions property [ADO]
ms.assetid: 390c8abf-133e-40da-8b99-8f748a983e4f
author: rothja
ms.author: jroth
ms.openlocfilehash: 2e7e574836f09df6f3bb8fdb078661c85cbf6355
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990676"
---
# <a name="marshaloptions-property-ado"></a>Propiedad MarshalOptions (ADO)
Indica los registros del [conjunto de registros](./recordset-object-ado.md) que se van a serializar en el servidor.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de [MarshalOptionsEnum](./marshaloptionsenum.md) . El valor predeterminado es **adMarshalAll**.  
  
## <a name="remarks"></a>Observaciones  
 Cuando se usa un conjunto de [registros](./recordset-object-ado.md)de cliente, los registros que se han modificado en el cliente se escriben de nuevo en el nivel intermedio o en el servidor Web mediante una técnica denominada serialización, el proceso de empaquetado y envío de parámetros de método de interfaz a través de los límites de subprocesos o procesos. El establecimiento de la propiedad **MarshalOptions** puede mejorar el rendimiento cuando se calculan las referencias de los datos remotos modificados para volver a actualizarlos en el nivel intermedio o en el servidor Web.  
  
> [!NOTE]
>  **Uso del servicio de datos remotos** Esta propiedad solo se usa en un **conjunto de registros**del lado cliente.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la propiedad MarshalOptions (VB)](./marshaloptions-property-example-vb.md)   
 [Ejemplo de la propiedad MarshalOptions (VC ++)](./marshaloptions-property-example-vc.md)