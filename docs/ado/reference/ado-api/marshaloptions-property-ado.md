---
description: Propiedad MarshalOptions (ADO)
title: MarshalOptions (propiedad) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: a3eb985c5940659f6d70c331dd860f0588398fb8
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774504"
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