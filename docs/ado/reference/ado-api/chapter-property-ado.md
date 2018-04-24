---
title: Propiedad de capítulo (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7cfa863254391760a45f8857f002ac92f25dd07
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="chapter-property-ado"></a>Capítulo (propiedad, ADO)
Obtiene o establece OLE DB **capítulo** objeto de/en un [interfaz ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md) objeto. Cuando usas **put_Chapter** para establecer el **capítulo** objeto, un subconjunto de filas se convierte en ADO [objeto Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Esto establece el capítulo actual de la **conjunto de filas**objeto. Esta propiedad es de lectura y escritura.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT get_Chapter([out, retval] long* plChapter);  
HRESULT put_Chapter([in] long lChapter);  
```  
  
## <a name="parameters"></a>Parámetros  
 *plChapter*  
 Puntero al identificador de un capítulo.  
  
 *LChapter*  
 Identificador de un capítulo.  
  
## <a name="return-values"></a>Valores devueltos  
 Este método de propiedad devuelve los valores HRESULT estándar, incluidos S_OK y E_FAIL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Interfaz ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
