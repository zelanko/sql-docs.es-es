---
title: Estado (propiedad, ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 87440d545d39bf1d260a20f38f230b493230cfed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708675"
---
# <a name="state-property-ado-md"></a>State (propiedad) (ADO MD)
Indica el estado actual del conjunto de celdas.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **largo** entero que indica el estado actual de la [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) de objetos y es de solo lectura. Los valores siguientes son válidos: **adStateClosed** (0) y **adStateOpen** (1).  
  
## <a name="remarks"></a>Comentarios  
 Para usar el [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) los nombres de constantes, debe tener en el proyecto hace referencia a la biblioteca de tipos de ADO. Consulte [utilizar ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md) para obtener más información.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Close (método) (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Open (método) (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
