---
title: Método get_OLEDBCommand | Documentos de Microsoft
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
- get_OLEDBCommand method [ADO]
ms.assetid: 23d551f5-3d5b-434b-ade6-fef15f1710e7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ec269e224dd87d430993e57b89c56a8701da407
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278710"
---
# <a name="getoledbcommand-method"></a>get_OLEDBCommand (método)
Devuelve el subyacente comando de OLE DB, en primer lugar propagar cualquier información de parámetro establecida en el comando de ADO para el comando de OLE DB.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ppOLEDBCommand*  
 [out] Un puntero a una ubicación del puntero donde se escribirá el puntero IUnknown para el comando OLE DB subyacente.  
  
## <a name="applies-to"></a>Se aplica a  
 [IADOCommandConstruction](http://msdn.microsoft.com/en-us/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)
