---
title: Comando SET BLOCKSIZE (Set BLOCKSIZE Command) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3eb9fbe9df90f7ddafebc6baa029164a578a6da3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300905"
---
# <a name="set-blocksize-command"></a>Comando BLOCKSIZE Set
Especifica cómo se asigna el espacio en disco para el almacenamiento de campos de nota.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>Argumentos  
 *nBytes*  
 Especifica el tamaño de bloque en el que se asigna espacio en disco para los campos de nota. Si *nBytes* es 0, el espacio en disco se asigna en bytes únicos (bloques de 1 byte). Si *nBytes* es un entero entre 1 y 32, el espacio en disco se asigna en bloques de *nBytes* bytes multiplicados por 512. Si *nBytes* es mayor que 32, el espacio en disco se asigna en bloques de *nBytes* bytes. Si especifica un valor de tamaño de bloque mayor que 32, puede ahorrar espacio sustancial en disco.  
  
## <a name="remarks"></a>Observaciones  
 El valor predeterminado para SET BLOCKSIZE es 64. Para restablecer el tamaño de bloque a un valor diferente después de crear el archivo, establézco en un nuevo valor y, a continuación, utilice COPY para crear una nueva tabla. La nueva tabla tiene el tamaño de bloque especificado.
