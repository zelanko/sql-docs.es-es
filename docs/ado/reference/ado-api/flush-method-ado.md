---
description: Flush (método) (ADO)
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
ms.openlocfilehash: 532a6bf973960e5c6a0a7d6f44ff8e0a2c2d1d09
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775144"
---
# <a name="flush-method-ado"></a>Flush (método) (ADO)
Fuerza el contenido de la [secuencia](./stream-object-ado.md) que queda en el búfer de ADO al objeto subyacente al que está asociada la **secuencia** .  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.Flush  
```  
  
## <a name="remarks"></a>Observaciones  
 Este método se puede usar para enviar el contenido del búfer de secuencia al objeto subyacente: por ejemplo, el nodo o el archivo representado por la dirección URL que es el origen del objeto de **secuencia** . Se debe llamar a este método cuando desee asegurarse de que se han escrito todos los cambios realizados en el contenido de una **secuencia** . Sin embargo, con ADO, normalmente no es necesario llamar a **Flush**, ya que ADO vacía el búfer continuamente lo máximo posible en segundo plano. Los cambios en el contenido de una **secuencia** se realizan automáticamente, no se almacenan en caché hasta que se llama a **Flush** .  
  
 Al cerrar una **secuencia** con el método [Close](./close-method-ado.md) , se vacía automáticamente el contenido de una **secuencia** . no es necesario llamar explícitamente a **Flush** inmediatamente antes de **cerrarse**.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](./stream-object-ado.md)