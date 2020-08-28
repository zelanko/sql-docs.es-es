---
description: Propiedad DefaultDatabase
title: Propiedad DefaultDatabase | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::DefaultDatabase
helpviewer_keywords:
- DefaultDatabase property
ms.assetid: 41e8a8dd-e69c-4a09-8736-93502e01961c
author: rothja
ms.author: jroth
ms.openlocfilehash: 86a8b283880f0765100c5a36eb63954f232c565a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974196"
---
# <a name="defaultdatabase-property"></a>Propiedad DefaultDatabase
Indica la base de datos predeterminada para un objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor de **cadena** que se evalúa como el nombre de una base de datos disponible en el proveedor.  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **DefaultDatabase** para establecer o devolver el nombre de la base de datos predeterminada en un objeto de **conexión** específico.  
  
 Si hay una base de datos predeterminada, las cadenas SQL pueden usar una sintaxis incompleta para tener acceso a los objetos de esa base de datos. Para obtener acceso a los objetos de una base de datos distinta de la especificada en la propiedad **DefaultDatabase** , debe calificar los nombres de objeto con el nombre de base de datos deseado. Tras la conexión, el proveedor escribirá información de base de datos predeterminada en la propiedad **DefaultDatabase** . Algunos proveedores solo permiten una base de datos por conexión, en cuyo caso no se puede cambiar la propiedad **DefaultDatabase** .  
  
 Es posible que algunos orígenes de datos y proveedores no admitan esta característica y que devuelvan un error o una cadena vacía.  
  
> [!NOTE]
>  **Uso del servicio de datos remotos** Esta propiedad no está disponible en un objeto de **conexión** del lado cliente.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades Provider y DefaultDatabase (VB)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vb.md)   
 [Ejemplo de las propiedades Provider y DefaultDatabase (VC ++)](../../../ado/reference/ado-api/provider-and-defaultdatabase-properties-example-vc.md)   
