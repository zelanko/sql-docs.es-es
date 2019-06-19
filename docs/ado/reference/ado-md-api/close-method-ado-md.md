---
title: Close (método) (ADO MD) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 4f01845752c0ee1f9187ea3d209a97509f87a5a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66709579"
---
# <a name="close-method-ado-md"></a>Close (método) (ADO MD)
Cierra un conjunto de celdas abierto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>Comentarios  
 Mediante el **cerrar** método para cerrar un [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto publicará los datos asociados, incluidos los datos en cualquier relacionados con [celda](../../../ado/reference/ado-md-api/cell-object-ado-md.md), [eje](../../../ado/reference/ado-md-api/axis-object-ado-md.md), [Posición](../../../ado/reference/ado-md-api/position-object-ado-md.md), o [miembro](../../../ado/reference/ado-md-api/member-object-ado-md.md) objetos. Cerrar un **Cellset** no se quita de la memoria; puede cambiar la configuración de sus propiedades y abrirlo de nuevo más tarde. Para eliminar completamente un objeto de la memoria, establezca la variable de objeto **nada**.  
  
 Posteriormente, puede llamar el [abierto](../../../ado/reference/ado-md-api/open-method-ado-md.md) método para volver a abrir el **Cellset** utilizando la misma u otra cadena de origen. Mientras el **Cellset** objeto está cerrado, recuperar las propiedades o llamar a los métodos que hacen referencia a los datos subyacentes o metadatos genera un error.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de celdas (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto Axis (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)   
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Objeto de miembro (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)   
 [Método Open (ADO MD)](../../../ado/reference/ado-md-api/open-method-ado-md.md)   
 [Objeto Position (ADO MD)](../../../ado/reference/ado-md-api/position-object-ado-md.md)   
 [State (propiedad) (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)
