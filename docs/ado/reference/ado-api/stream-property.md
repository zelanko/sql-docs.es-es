---
title: Una propiedad de secuencia | Documentos de Microsoft
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
- ADOStreamConstruction::GetStream
- ADOStreamConstruction::PutStream
- ADOStreamConstruction::put_Stream
- ADOStreamConstruction::Stream
- ADOStreamConstruction::get_Stream
helpviewer_keywords:
- Stream property
ms.assetid: 4a44f9f6-0265-4c00-8def-d85b6af923b1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dc56c9a655c4e85f76cae877579b9a344c11ff4d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="stream-property"></a>Propiedad de la secuencia
Obtiene o establece OLE DB **flujo** objeto de/en un **ADOStreamConstruction** objeto.  
  
 Lectura/escritura  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT get_Stream([out, retval] IUnknown** ppStream);  
HRESULT put_Stream([in] IUnknown* pStream);  
```  
  
## <a name="parameters"></a>Parámetros  
 *ppStream*  
 Puntero a OLE DB **flujo** objeto.  
  
 *pStream*  
 OLE DB **flujo** objeto.  
  
## <a name="return-values"></a>Valores devueltos  
 Este método de propiedad devuelve los valores HRESULT estándar. Esto incluye S_OK y E_FAIL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Interfaz ADOStreamConstruction](../../../ado/reference/ado-api/adostreamconstruction-interface.md)
