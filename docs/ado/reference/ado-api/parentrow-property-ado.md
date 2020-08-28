---
description: ParentRow (propiedad) (ADO)
title: Propiedad ParentRow (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 03ef3135e72cac39f91dc1393458c36d63458db6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990096"
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
 [Interfaz ADORecordConstruction](./adorecordconstruction-interface.md)