---
title: Una propiedad de secuencia | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9318e52eac9301cdcf2d3cf02bbc88ad917b4669
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282554"
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
