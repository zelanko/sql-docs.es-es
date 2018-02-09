---
title: Interfaz IDSOShapeExtensions | Documentos de Microsoft
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
- IDSOShapeExtensions interface [ADO]
ms.assetid: ad4ba313-1161-4bc7-b8f6-4083305bc81e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 454dc39046b33e2b621f77ea2a31bddc16b742ea
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="idsoshapeextensions-interface"></a>Interfaz IDSOShapeExtensions
Obtiene el objeto de origen de datos OLE DB subyacente para el proveedor de formas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
interface IDSOShapeExtensions: public IUnknown {  
public:  
      HRESULT  GetDataProviderDSO(  
            IUnknown **ppDataProviderDSOIUnknown  
      );  
};  
```  
  
## <a name="methods"></a>Métodos  
  
|||  
|-|-|  
|[GetDataProviderDSO (método)](../../../ado/reference/ado-api/getdataproviderdso-method.md)|Recupera el objeto de origen de datos OLE DB subyacente desde el proveedor de formas.|  
  
## <a name="requirements"></a>Requisitos  
 **Versión:** ADO 2.0 y versiones posteriores  
  
 **Library:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4
