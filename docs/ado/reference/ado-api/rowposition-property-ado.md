---
description: RowPosition (propiedad, ADO)
title: RowPosition (propiedad, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0f5f78843e38c2a3ff6b21c90bc9ed7f2c573ee4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777614"
---
# <a name="rowposition-property-ado"></a>RowPosition (propiedad, ADO)
Obtiene o establece un objeto **RowPosition** OLE DB de/en un objeto **ADORecordsetConstruction** . Cuando se usa **put_RowPosition** para establecer el objeto **rowposition** , el objeto de **conjunto de registros** resultante utiliza el objeto **rowposition** para determinar la fila actual.  
  
 Lectura/escritura  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>Parámetros  
 *ppRowPos*  
 Puntero a un objeto **RowPosition** de OLE DB.  
  
 *PRowPos*  
 Objeto **RowPosition** OLE DB.  
  
## <a name="return-values"></a>Valores devueltos  
 Este método de propiedad devuelve los valores HRESULT estándar, incluidos S_OK y E_FAIL.  
  
## <a name="remarks"></a>Observaciones  
 Cuando se establece esta propiedad, si el objeto de **conjunto de filas** del objeto **RowPosition** es diferente del objeto de conjunto de **filas** del objeto de **conjunto de registros** , el primero invalida el último. También se aplica el mismo comportamiento al **capítulo** actual de **RowPosition** .  
  
## <a name="applies-to"></a>Se aplica a  
 [Interfaz ADORecordsetConstruction](./adorecordsetconstruction-interface.md)