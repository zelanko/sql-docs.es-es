---
title: Fila (propiedad, ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::PutRow
- ADORecordConstruction::GetRow
- ADORecordConstruction::get_Row
- ADORecordConstruction::Row
- ADORecordConstruction::put_Row
helpviewer_keywords:
- Row property [ADO]
ms.assetid: 21019d89-2dd1-4a26-ac6f-384b81d66949
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8b62cd50996a98c94261454e069a8f8a2d2bb9ba
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="row-property-ado"></a>Propiedad de las filas (ADO)
Obtiene o establece OLE DB **fila** objeto desde o en un [Interfaz ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md) objeto. Cuando usas **put_Row** para establecer un **fila** objeto, una fila se convierte en ADO **registro** objeto.  
  
## <a name="readwritesyntax"></a>Lectura/escritura. Sintaxis  
  
```  
HRESULT get_Row([out, retval] IUnknown** ppRow);  
HRESULT put_Row([in] IUnknown* pRow);  
```  
  
## <a name="parameters"></a>Parámetros  
 *ppRow*  
 Puntero a OLE DB **fila** objeto.  
  
 *PRow*  
 OLE DB **fila** objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Este método de propiedad devuelve los valores HRESULT estándar, incluidos S_OK y E_FAIL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Interfaz ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
