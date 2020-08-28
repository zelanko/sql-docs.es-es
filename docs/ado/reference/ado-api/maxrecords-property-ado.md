---
description: Propiedad MaxRecords (ADO)
title: Propiedad MaxRecords (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MaxRecords
helpviewer_keywords:
- MaxRecords property [ADO]
ms.assetid: 20c76571-8c9a-482c-a99e-726ab1d93f8b
author: rothja
ms.author: jroth
ms.openlocfilehash: 31870c4df71b20c162f95f1f1d942dde63885227
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990646"
---
# <a name="maxrecords-property-ado"></a>Propiedad MaxRecords (ADO)
Indica el número máximo de registros que se van a devolver a un [conjunto](./recordset-object-ado.md) de registros desde una consulta.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor **Long** que indica el número máximo de registros que se van a devolver. El valor predeterminado es cero (**0**), lo que significa que no hay límite.  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **MaxRecords** para limitar el número de registros que devuelve el proveedor desde el origen de datos. La configuración predeterminada de esta propiedad es cero, lo que significa que el proveedor devuelve todos los registros solicitados.  
  
 La propiedad **MaxRecords** es de lectura y escritura cuando el **conjunto de registros** está cerrado y es de solo lectura cuando está abierto.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la propiedad MaxRecords (VB)](./maxrecords-property-example-vb.md)   
 [Ejemplo de la propiedad MaxRecords (VC ++)](./maxrecords-property-example-vc.md)