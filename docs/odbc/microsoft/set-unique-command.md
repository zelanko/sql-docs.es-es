---
title: CONJUNTO único comando | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7f58eb771245b9820e27ca4d14c2f69035effa44
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63159314"
---
# <a name="set-unique-command"></a>CONJUNTO único comando
Especifica si se mantienen registros con valores de clave de índice duplicados en un archivo de índice.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 Especifica que cualquier registro con un valor de clave de índice duplicados no se incluirán en el archivo de índice. Solo el primer registro con el valor de clave de índice original se incluye en el archivo de índice.  
  
 OFF  
 (Valor predeterminado). Especifica que se incluirán registros con valores de clave de índice duplicados en el archivo de índice.  
  
## <a name="remarks"></a>Comentarios  
 Un archivo de índice mantiene su conjunto exclusivo al emitir REINDEX. Para obtener más información, consulte [índice](../../odbc/microsoft/index-command.md).
