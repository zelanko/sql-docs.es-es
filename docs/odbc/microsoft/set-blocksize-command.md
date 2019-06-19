---
title: Comando BLOCKSIZE SET | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set blocksize command [ODBC]
ms.assetid: 0c11580f-37f5-4a8e-99be-9fb9c44bb433
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e904d341513047b3940cf5b3fc2ba9538cdb5c8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127843"
---
# <a name="set-blocksize-command"></a>Comando BLOCKSIZE Set
Especifica cómo se asigna espacio en disco para el almacenamiento de los campos de memorando.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>Argumentos  
 *nBytes*  
 Especifica el tamaño de bloque en el que se asigna espacio en disco para los campos de memorando. Si *nBytes* es 0, se asigna espacio en disco en un solo byte (bloques de 1 byte). Si *nBytes* es un entero entre 1 y 32, espacio en disco se asigna en bloques de *nBytes* bytes multiplican por 512. Si *nBytes* es mayor que 32, se asigna espacio en disco en bloques de *nBytes* bytes. Si especifica un valor de tamaño de bloque mayor que 32, se puede ahorrar espacio en disco considerable.  
  
## <a name="remarks"></a>Comentarios  
 El valor predeterminado para establecer el tamaño de bloque es 64. Para restablecer el tamaño de bloque en un valor diferente una vez creado el archivo, establézcalo en un nuevo valor y, a continuación, usar la copia para crear una nueva tabla. La nueva tabla tiene el tamaño de bloque especificado.
