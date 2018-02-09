---
title: ParentRow (propiedad) (ADO) | Documentos de Microsoft
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
apitype: COM
f1_keywords:
- ADORecordConstruction::put_ParentRow
- ADORecordConstruction::ParentRow
- ADORecordConstruction::putParentRow
helpviewer_keywords:
- ParentRow property [ADO]
ms.assetid: 5ea8029b-eda4-490b-ae84-2ad036fb582f
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1305304afaa06f8e96dc4160b466d87271f537d9
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="parentrow-property-ado"></a>ParentRow (propiedad) (ADO)
Establece el contenedor de OLE DB **fila** objeto en un **ADORecordConstruction** objeto, por lo que el elemento primario de la fila se convierte en ADO **registro** objeto.  
  
 De solo escritura.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
HRESULT put_ParentRow([in] IUnknown* pParent);  
```  
  
## <a name="parameters"></a>Parámetros  
 *pParent*  
 Un contenedor de una fila.  
  
## <a name="return-values"></a>Valores devueltos  
 Este método de propiedad devuelve los valores HRESULT estándar, incluidos S_OK y E_FAIL.  
  
## <a name="applies-to"></a>Se aplica a  
 [Interfaz ADORecordConstruction](../../../ado/reference/ado-api/adorecordconstruction-interface.md)
