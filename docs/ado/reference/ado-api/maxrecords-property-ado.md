---
title: La propiedad MaxRecords (ADO) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 130a67f10e8b7deaf8f48e94f949b43682f61ca1
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707631"
---
# <a name="maxrecords-property-ado"></a>Propiedad MaxRecords (ADO)
Indica el número máximo de registros que se devuelven a un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) desde una consulta.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor que indica el número máximo de registros que se devuelven. Valor predeterminado es cero (**0**), lo que significa que no hay ningún límite.  
  
## <a name="remarks"></a>Comentarios  
 Use la **MaxRecords** propiedad para limitar el número de registros que devuelve el proveedor del origen de datos. El valor predeterminado de esta propiedad es cero, lo que significa que el proveedor devuelve que todos los registros solicitados.  
  
 El **MaxRecords** propiedad es de lectura/escritura cuando el **Recordset** está cerrado y de solo lectura cuando se abre.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad MaxRecords (VB)](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [Ejemplo de la propiedad MaxRecords (VC ++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   
