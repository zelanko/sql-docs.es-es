---
description: ParentRow (propiedad) (ADO)
title: Propiedad ParentRow (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction::put_ParentRow
- ADORecordConstruction::ParentRow
- ADORecordConstruction::putParentRow
helpviewer_keywords:
- ParentRow property [ADO]
ms.assetid: 5ea8029b-eda4-490b-ae84-2ad036fb582f
author: rothja
ms.author: jroth
ms.openlocfilehash: b81fc704c78b620c1319aa592336aba0489a3d37
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442747"
---
# <a name="parentrow-property-ado"></a>ParentRow (propiedad) (ADO)
Establece el contenedor de un objeto de **fila** OLE DB en un objeto **ADORecordConstruction** , de modo que el elemento primario de la fila se convierta en un objeto **Record** de ADO.  
  
 De solo escritura.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT put_ParentRow([in] IUnknown* pParent);  
```  
  
## <a name="parameters"></a>Parámetros  
 *pParent*  
 Contenedor de una fila.  
  
## <a name="return-values"></a>Valores devueltos  
 Este método de propiedad devuelve los valores HRESULT estándar, incluidos S_OK y E_FAIL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Interfaz ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
