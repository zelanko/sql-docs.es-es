---
description: Capítulo (propiedad, ADO)
title: Chapter (propiedad, ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 04469dc7cc888a167135ad18a77469200614e925
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776304"
---
# <a name="chapter-property-ado"></a>Capítulo (propiedad, ADO)
Obtiene o establece un objeto **Chapter** de OLE DB desde/en un objeto de [interfaz ADORecordsetConstruction](./adorecordsetconstruction-interface.md) . Cuando se usa **put_Chapter** para establecer el objeto **Chapter** , se convierte un subconjunto de filas en un objeto [Recordset](./recordset-object-ado.md) de ADO. Esto establece el capítulo actual del objeto de **conjunto de filas**. Esta propiedad es de lectura y escritura.  
  
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
 [Interfaz ADORecordsetConstruction](./adorecordsetconstruction-interface.md)