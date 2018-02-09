---
title: RowPosition (propiedad, ADO) | Documentos de Microsoft
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
- ADORecordConstruction::put_RowPosition
- ADORecordConstruction::PutRowPosition
- ADORecordConstruction::GetRowPosition
- ADORecordConstruction::RowPosition
- ADORecordConstruction::get_RowPosition
helpviewer_keywords:
- RowPosition property [ADO]
ms.assetid: 9d068fed-39bf-4842-afc3-686a2af2145d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0e384d850a51cc94439a896040951ec3c23f2f6a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="rowposition-property-ado"></a>RowPosition (propiedad, ADO)
Obtiene o establece OLE DB **RowPosition** objeto de/en un **ADORecordsetConstruction** objeto. Cuando se usa **put_RowPosition** para establecer el **RowPosition** objeto resultante **Recordset** de objeto usa la **RowPosition** objeto determinar la fila actual.  
  
 Lectura/escritura  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>Parámetros  
 *ppRowPos*  
 Puntero a OLE DB **RowPosition** objeto.  
  
 *PRowPos*  
 OLE DB **RowPosition** objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Este método de propiedad devuelve los valores HRESULT estándar, incluidos S_OK y E_FAIL.  
  
## <a name="remarks"></a>Comentarios  
 Cuando se establece esta propiedad, si el **conjunto de filas** objeto en el **RowPosition** objeto es diferente de la **conjunto de filas** objeto en el **delconjuntoderegistros**objeto, el primero sobrescribe al segundo. El mismo comportamiento se aplica a la corriente **capítulo** de la **RowPosition** así.  
  
## <a name="applies-to"></a>Se aplica a  
 [Interfaz ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
