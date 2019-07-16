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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918271"
---
# <a name="loadfromfile-method-ado"></a>LoadFromFile (método) (ADO)
Carga el contenido de un archivo existente en un [Stream](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>Parámetros  
 *FileName*  
 Un **cadena** valor que contiene el nombre de un archivo que se cargará en el **Stream**. *Nombre de archivo* puede contener cualquier ruta de acceso y nombre en formato UNC. Si el archivo especificado no existe, se produce un error en tiempo de ejecución.  
  
## <a name="remarks"></a>Comentarios  
 Este método puede utilizarse para cargar el contenido de un archivo local en un **Stream** objeto. Esto puede utilizarse para cargar el contenido de un archivo local en un servidor.  
  
 El **Stream** objeto ya debe estar abierto antes de llamar a **LoadFromFile**. Este método no cambia el enlace de la **Stream** objeto todavía se enlazará al objeto especificado por la dirección URL o **registro** con el que el **Stream** era originalmente puede abrir.  
  
 **LoadFromFile** sobrescribe el contenido actual de la **Stream** objeto con los datos leídos desde el archivo. Los bytes existentes en el **Stream** se sobrescriben con el contenido del archivo. Los bytes restantes y previamente existentes siguiendo el [EOS](../../../ado/reference/ado-api/eos-property.md) creado por **LoadFromFile**, se truncan.  
  
 Después de llamar a **LoadFromFile**, se establece la posición actual hasta el principio de la **Stream** ([posición](../../../ado/reference/ado-api/position-property-ado.md) es 0).  
  
 Dado que pueden agregarse 2 bytes al principio de la secuencia para la codificación, el tamaño de la secuencia es posible que no coincidan con el tamaño del archivo desde el que se cargó.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
