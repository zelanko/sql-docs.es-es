---
title: "Método GetDataProviderDSO | Documentos de Microsoft"
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
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0a5c5ff974b6f99323de04ea274f635c52ca2755
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
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
