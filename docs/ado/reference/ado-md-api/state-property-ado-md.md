---
title: Estado (propiedad, ADO MD) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- State
- Cellset::State
helpviewer_keywords:
- State property [ADO MD]
ms.assetid: 06d480ca-9eb6-4570-a45d-a73539bddd32
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 975a9354734e0f6e5d0a2502b89b43c886be5fa3
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35284564"
---
# <a name="state-property-ado-md"></a>State (propiedad) (ADO MD)
Indica el estado actual del conjunto de celdas.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un **largo** entero que indica el estado actual de la [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) de objetos y es de solo lectura. Los valores siguientes son válidos: **adStateClosed** (0) y **adStateOpen** (1).  
  
## <a name="remarks"></a>Notas  
 Para usar el [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) nombres de constantes, debe tener en su proyecto hace referencia a la biblioteca de tipos de ADO. Vea [utilizar ADO con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md) para obtener más información.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Close (método) (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Open (método) (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
