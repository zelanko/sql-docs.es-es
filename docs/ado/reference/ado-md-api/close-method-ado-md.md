---
title: Método Close (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 09e83fd8645a5c0ab604a640478c4cced4870742
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949811"
---
# <a name="close-method-ado-md"></a>Close (método) (ADO MD)
Cierra un Cellset abierto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>Observaciones  
 Al utilizar el método **Close** para cerrar un objeto [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) , se liberarán los datos asociados, incluidos los datos de los objetos de [celda](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md), [posición](../../../ado/reference/ado-md-api/position-object-ado-md.md)o [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) relacionados. Al cerrar un **Cellset** no se quita de la memoria; puede cambiar la configuración de sus propiedades y volver a abrirla más tarde. Para eliminar completamente un objeto de la memoria, establezca la variable de objeto en **Nothing**.  
  
 Después, puede llamar al método [Open](../../../ado/reference/ado-md-api/open-method-ado-md.md) para volver a abrir el **Cellset** usando la misma cadena de origen u otra. Mientras se cierra el objeto **Cellset** , se produce un error al recuperar cualquier propiedad o llamar a cualquier método que haga referencia a los datos o metadatos subyacentes.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte también  
 [Objeto AXIS (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Objeto miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Método Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [Objeto Position (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [State (propiedad) (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
