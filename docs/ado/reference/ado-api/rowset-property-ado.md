---
description: Propiedad Rowset (ADO)
title: Propiedad Rowset (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction::PutRowset
- ADORecordsetConstruction::GetRowset
- ADORecordsetConstruction::Rowset
- ADORecordsetConstruction::put_Rowset
- ADORecordsetConstruction::get_Rowset
helpviewer_keywords:
- Rowset property [ADO]
ms.assetid: 7d359294-4ff2-47e0-8111-0c221b24d80e
author: rothja
ms.author: jroth
ms.openlocfilehash: 8f6342de5be5b2c6ba6e1bf58408cfabc6e31088
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442237"
---
# <a name="rowset-property-ado"></a>Propiedad Rowset (ADO)
Obtiene o establece un objeto de **conjunto de filas** OLE DB de/en un objeto **ADORecordsetConstruction** . Cuando se utiliza put_Rowset, el conjunto de filas se convierte en un objeto de **conjunto de registros** de ADO.  
  
 Lectura/escritura  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT get_Rowset([out, retval] IUnknown** ppRowset);  
HRESULT put_Rowset([in] IUnknown* pRowset);  
```  
  
## <a name="parameters"></a>Parámetros  
 *ppRowset*  
 Puntero a un objeto de **conjunto de filas** de OLE DB.  
  
 *PRowset*  
 Objeto de **conjunto de filas** OLE DB.  
  
## <a name="return-values"></a>Valores devueltos  
 Este método de propiedad devuelve los valores HRESULT estándar, incluidos S_OK y E_FAIL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Interfaz ADORecordsetConstruction](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
