---
title: get_oledbcommand (método) | Microsoft Docs
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
ms.openlocfilehash: e7b2668c3693078c7027b26fa61df73b81161970
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979357"
---
# <a name="getoledbcommand-method"></a>get_oledbcommand (método)
Devuelve el subyacente comando de OLE DB, en primer lugar propagar cualquier información de parámetro establecido en el comando de ADO para el comando de OLE DB.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ppOLEDBCommand*  
 [out] Un puntero a una ubicación del puntero donde se escribirá el puntero IUnknown del comando OLE DB subyacente.  
  
## <a name="applies-to"></a>Se aplica a  
 [IADOCommandConstruction](http://msdn.microsoft.com/d8e54333-00eb-4b72-bf4a-ca92c7ca5f86)
