---
title: "Método get_OLEDBCommand | Documentos de Microsoft"
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
- get_OLEDBCommand method [ADO]
ms.assetid: 23d551f5-3d5b-434b-ade6-fef15f1710e7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c78a0b7bd79da2bc75c3bcccbcb2bc9acbde8e35
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
