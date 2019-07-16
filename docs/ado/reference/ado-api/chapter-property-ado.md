---
title: Capítulo (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::Chapter
- ADORecordsetConstruction::put_Chapter
- ADORecordsetConstruction::get_Chapter
helpviewer_keywords:
- Chapter property [ADO]
ms.assetid: 8aa90cb0-f588-4141-9dc9-3b22918394ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2791bc1a89f8cec1362ab1f00c3be739f7d56b96
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920107"
---
# <a name="chapter-property-ado"></a>Capítulo (propiedad, ADO)
Obtiene o establece OLE DB **capítulo** objeto desde/en un [interfaz ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md) objeto. Cuando usas **put_Chapter** para establecer el **capítulo** objeto, un subconjunto de filas se convierte en ADO [objeto Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto. Esto establece el capítulo actual de la **conjunto de filas**objeto. Esta propiedad es de lectura y escritura.  
  
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
