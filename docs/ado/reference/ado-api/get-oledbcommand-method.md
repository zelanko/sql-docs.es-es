---
description: get_OLEDBCommand (método)
title: Método get_OLEDBCommand | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- get_OLEDBCommand method [ADO]
ms.assetid: 23d551f5-3d5b-434b-ade6-fef15f1710e7
author: rothja
ms.author: jroth
ms.openlocfilehash: 56148afcd3c7d3e18e856c6e50a44f35aaa1bc64
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775134"
---
# <a name="get_oledbcommand-method"></a>get_OLEDBCommand (método)
Devuelve el comando de OLE DB subyacente, propagando primero cualquier información de parámetros establecida en el comando de ADO al comando OLE DB.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
HRESULT get_OLEDBCommand(  
      IUnknown **ppOLEDBCommand  
);  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ppOLEDBCommand*  
 enuncia Puntero a una ubicación de puntero en la que se escribirá el puntero IUnknown del comando de OLE DB subyacente.  
  
## <a name="applies-to"></a>Se aplica a  
 [IADOCommandConstruction](/previous-versions/windows/desktop/aa965677(v=vs.85))