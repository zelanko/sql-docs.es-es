---
title: Propiedad MaxRecords (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: b9e4beaaa4b38a26089d1136d1b32090ea12231f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82754378"
---
# <a name="maxrecords-property-ado"></a>Propiedad MaxRecords (ADO)
Indica el número máximo de registros que se van a devolver a un [conjunto](../../../ado/reference/ado-api/recordset-object-ado.md) de registros desde una consulta.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un valor **Long** que indica el número máximo de registros que se van a devolver. El valor predeterminado es cero (**0**), lo que significa que no hay límite.  
  
## <a name="remarks"></a>Comentarios  
 Utilice la propiedad **MaxRecords** para limitar el número de registros que devuelve el proveedor desde el origen de datos. La configuración predeterminada de esta propiedad es cero, lo que significa que el proveedor devuelve todos los registros solicitados.  
  
 La propiedad **MaxRecords** es de lectura y escritura cuando el **conjunto de registros** está cerrado y es de solo lectura cuando está abierto.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de la propiedad MaxRecords (VB)](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [Ejemplo de la propiedad MaxRecords (VC ++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   
