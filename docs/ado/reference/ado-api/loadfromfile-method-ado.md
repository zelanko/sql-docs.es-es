---
description: LoadFromFile (método) (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2f07bd7bc6b04dac8c5b352cc6281ce4eb851d3d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443357"
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
