---
title: LoadFromFile (método) (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_LoadFromFile
helpviewer_keywords:
- LoadFromFile method [ADO]
ms.assetid: b18d8d38-7354-4a94-b637-6ac035faa433
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ce90b13a677246fb64462fbe691eb9e3efaa3c7f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918271"
---
# <a name="loadfromfile-method-ado"></a>LoadFromFile (método) (ADO)
Carga el contenido de un archivo existente en una [secuencia](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>Parámetros  
 *FileName*  
 Valor de **cadena** que contiene el nombre de un archivo que se va a cargar en la **secuencia**. *Filename* puede contener cualquier nombre y ruta de acceso válidos en formato UNC. Si el archivo especificado no existe, se produce un error en tiempo de ejecución.  
  
## <a name="remarks"></a>Observaciones  
 Este método se puede utilizar para cargar el contenido de un archivo local en un objeto de **flujo** . Se puede usar para cargar el contenido de un archivo local en un servidor.  
  
 El objeto de **secuencia** debe estar abierto antes de llamar a **LoadFromFile**. Este método no cambia el enlace del objeto de **secuencia** . todavía se enlazará al objeto especificado por la dirección URL o el **registro** con el que se abrió originalmente la **secuencia** .  
  
 **LoadFromFile** sobrescribe el contenido actual del objeto de **secuencia** con los datos leídos del archivo. El contenido del archivo sobrescribe cualquier byte existente en la **secuencia** . Se truncan todos los bytes anteriores y restantes que siguen al [EOS](../../../ado/reference/ado-api/eos-property.md) creado por **LoadFromFile**.  
  
 Después de una llamada a **LoadFromFile**, la posición actual se establece en el principio de la **secuencia** (la[posición](../../../ado/reference/ado-api/position-property-ado.md) es 0).  
  
 Dado que se pueden agregar 2 bytes al principio de la secuencia para la codificación, el tamaño de la secuencia puede no coincidir exactamente con el tamaño del archivo desde el que se cargó.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
