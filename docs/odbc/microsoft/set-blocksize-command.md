---
title: Comando BLOCKSIZE | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- set blocksize command [ODBC]
ms.assetid: 0c11580f-37f5-4a8e-99be-9fb9c44bb433
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee5b55501d055d3bea09903a5486e88de3cdc993
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="set-blocksize-command"></a>Comando BLOCKSIZE Set.
Especifica cómo se asigna espacio en disco para el almacenamiento de los campos de memorando.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET BLOCKSIZE TO nBytes  
```  
  
## <a name="arguments"></a>Argumentos  
 *nBytes*  
 Especifica el tamaño de bloque en el que se asigna espacio en disco para los campos de memorando. Si *nBytes* es 0, se asigna espacio en disco en un solo byte (bloques de 1 byte). Si *nBytes* es un número entero entre 1 y 32, espacio en disco se asigna en bloques de *nBytes* bytes multiplican por 512. Si *nBytes* es mayor que 32, se asigna espacio en disco en bloques de *nBytes* bytes. Si especifica un valor de tamaño de bloque mayor que 32, puede ahorrar espacio en disco considerable.  
  
## <a name="remarks"></a>Comentarios  
 El valor predeterminado para establecer el tamaño de bloque es 64. Para restablecer el tamaño de bloque en un valor diferente después de que se ha creado el archivo, establézcalo en un nuevo valor y, a continuación, usar la copia para crear una nueva tabla. La nueva tabla tiene un tamaño de bloque especificado.
