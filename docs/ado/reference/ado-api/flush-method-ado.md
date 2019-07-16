---
title: Flush (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Flush
- _Stream::raw_Flush
helpviewer_keywords:
- Flush method [ADO]
ms.assetid: 938522b4-f836-4c80-8d27-a598a000f0ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f3d9ab76d2f2ed1a6f5dbeaf58be7d2f919acd3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932544"
---
# <a name="flush-method-ado"></a>Flush (método) (ADO)
Fuerza que el contenido de la [Stream](../../../ado/reference/ado-api/stream-object-ado.md) permanecen en el búfer de ADO para el objeto subyacente con el que el **Stream** está asociado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>Comentarios  
 Este método puede usarse para enviar el contenido del búfer de secuencia al objeto subyacente: por ejemplo, el nodo o el archivo representado por la dirección URL que es el origen de la **Stream** objeto. Debe llamar a este método cuando desee asegurarse de que todos los cambios que se realizaron en el contenido de un **Stream** se han escrito. Sin embargo, con ADO normalmente no es necesario llamar a **vaciar**, como ADO vacía continuamente su búfer tanto como sea posible en segundo plano. Cambia el contenido de un **Stream** se realizan automáticamente, no se almacenan en caché hasta que **vaciar** se llama.  
  
 Cerrar un **Stream** con el [cerrar](../../../ado/reference/ado-api/close-method-ado.md) método vuelca el contenido de un **Stream** automáticamente, ya no es necesario llamar explícitamente a **vaciar**inmediatamente antes de **cerrar**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
