---
description: GetDataProviderDSO (método)
title: Método GetDataProviderDSO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
author: rothja
ms.author: jroth
ms.openlocfilehash: 85e701cb7ce725aa9afa9d682467c1a97f5dd378
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88972906"
---
# <a name="getdataproviderdso-method"></a>GetDataProviderDSO (método)
Recupera el objeto de origen de datos OLE DB subyacente del proveedor de formas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT GetDataProviderDSO(  
      IUnknown **ppDataProviderDSOIUnknown  
);  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ppDataProviderDSOIUnknown*  
 enuncia  Un puntero a un puntero que devuelve el IUnknown del objeto de origen de datos de la OLE DB subyacente.  
  
## <a name="remarks"></a>Observaciones  
 Este método no hace AddRef el puntero de interfaz. Si el llamador tiene previsto mantener el puntero, el autor de la llamada debe realizar las llamadas AddRef y Release necesarias.  
  
## <a name="applies-to"></a>Se aplica a  
 [Interfaz IDSOShapeExtensions](./idsoshapeextensions-interface.md)