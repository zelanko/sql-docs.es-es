---
title: Método GetDataProviderDSO | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 40cf12ab80faf3c32da98c1fb97b7ec7d9ca373f
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278824"
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
  
## <a name="remarks"></a>Notas  
 Este método no hace no addref el puntero de interfaz. Si el llamador tiene previsto mantiene el puntero, el llamador debe hacer el necesario addref y release.  
  
## <a name="applies-to"></a>Se aplica a  
 [Interfaz IDSOShapeExtensions](../../../ado/reference/ado-api/idsoshapeextensions-interface.md)
