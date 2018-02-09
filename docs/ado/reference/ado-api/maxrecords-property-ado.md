---
title: Propiedad MaxRecords (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
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
- Recordset15::MaxRecords
helpviewer_keywords:
- MaxRecords property [ADO]
ms.assetid: 20c76571-8c9a-482c-a99e-726ab1d93f8b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7d6991928fdf3c284f7039b75f96a95fd93e0be3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="maxrecords-property-ado"></a>Propiedad MaxRecords (ADO)
Indica el número máximo de registros que se devuelven a un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) desde una consulta.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor que indica el número máximo de registros que se va a devolver. Valor predeterminado es cero (**0**), lo que significa que no hay ningún límite.  
  
## <a name="remarks"></a>Comentarios  
 Use la **MaxRecords** propiedad para limitar el número de registros que devuelve el proveedor del origen de datos. El valor predeterminado de esta propiedad es cero, lo que significa que el proveedor devuelve que todos los registros solicitados.  
  
 El **MaxRecords** propiedad es de lectura y escritura cuando el **Recordset** está cerrado y de solo lectura cuando se abre.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad MaxRecords (VB)](../../../ado/reference/ado-api/maxrecords-property-example-vb.md)   
 [Ejemplo de la propiedad MaxRecords (VC ++)](../../../ado/reference/ado-api/maxrecords-property-example-vc.md)   
