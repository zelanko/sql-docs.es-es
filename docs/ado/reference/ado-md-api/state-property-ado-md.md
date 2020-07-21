---
title: Propiedad State (ADO MD) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9722bdc585920fb5dcc70ac95afcf2e854a0fa50
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764986"
---
# <a name="state-property-ado-md"></a>State (propiedad) (ADO MD)
Indica el estado actual del Cellset.  
  
## <a name="return-values"></a>Valores devueltos  
 Devuelve un entero **largo** que indica la condición actual del objeto [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) y es de solo lectura. Los valores siguientes son válidos: **adStateClosed** (0) y **adStateOpen** (1).  
  
## <a name="remarks"></a>Comentarios  
 Para usar los nombres de constantes [ObjectStateEnum](../../../ado/reference/ado-api/objectstateenum.md) , debe tener la biblioteca de tipos ADO a la que se hace referencia en el proyecto. Vea [usar ado con ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md) para obtener más información.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Método Close (ADO MD)](../../../ado/reference/ado-md-api/close-method-ado-md.md)   
 [Open (método) (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)
