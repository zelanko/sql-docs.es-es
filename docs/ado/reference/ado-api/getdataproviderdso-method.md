---
title: "Método GetDataProviderDSO | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 40b23b500c50100b5a50f06566eeadd44e7f519c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getdataproviderdso-method"></a>GetDataProviderDSO (método)
Recupera el objeto de origen de datos OLE DB subyacente desde el proveedor de formas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ppDataProviderDSOIUnknown*  
 [out]  Un puntero a un puntero que devuelve la interfaz IUnknown del objeto de origen de datos OLE DB subyacente.  
  
## <a name="remarks"></a>Comentarios  
 Este método no hace no addref el puntero de interfaz. Si el llamador tiene previsto mantiene el puntero, el llamador debe hacer el necesario addref y release.  
  
## <a name="applies-to"></a>Se aplica a  
 [Interfaz IDSOShapeExtensions](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
