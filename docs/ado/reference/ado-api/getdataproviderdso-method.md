---
description: GetDataProviderDSO (método)
title: Método GetDataProviderDSO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- GetDataProviderDSO Method [ADO]
ms.assetid: 5a4c6bd5-0c79-4f81-a977-0561392d8d50
author: rothja
ms.author: jroth
ms.openlocfilehash: e21e45d72cd5140c542fb6d6d0b150c414fb9832
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775074"
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