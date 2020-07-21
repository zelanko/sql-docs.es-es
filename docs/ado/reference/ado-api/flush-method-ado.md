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
author: rothja
ms.author: jroth
ms.openlocfilehash: c00f3c92d3d2bd3111201d6f1536884e3e9dceb5
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760091"
---
# <a name="flush-method-ado"></a>Flush (método) (ADO)
Fuerza el contenido de la [secuencia](../../../ado/reference/ado-api/stream-object-ado.md) que queda en el búfer de ADO al objeto subyacente al que está asociada la **secuencia** .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>Observaciones  
 Este método se puede usar para enviar el contenido del búfer de secuencia al objeto subyacente: por ejemplo, el nodo o el archivo representado por la dirección URL que es el origen del objeto de **secuencia** . Se debe llamar a este método cuando desee asegurarse de que se han escrito todos los cambios realizados en el contenido de una **secuencia** . Sin embargo, con ADO, normalmente no es necesario llamar a **Flush**, ya que ADO vacía el búfer continuamente lo máximo posible en segundo plano. Los cambios en el contenido de una **secuencia** se realizan automáticamente, no se almacenan en caché hasta que se llama a **Flush** .  
  
 Al cerrar una **secuencia** con el método [Close](../../../ado/reference/ado-api/close-method-ado.md) , se vacía automáticamente el contenido de una **secuencia** . no es necesario llamar explícitamente a **Flush** inmediatamente antes de **cerrarse**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
