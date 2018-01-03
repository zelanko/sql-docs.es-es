---
title: "CONJUNTO único comando | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SET UNIQUE command [ODBC]
ms.assetid: 1f69e31e-4599-47cc-ac89-b86fba8703c5
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0ba0921d2bfab8911d129ac4d1430e6d8d9bd6fe
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="set-unique-command"></a>CONJUNTO único comando
Especifica si los registros con valores de clave de índice duplicados se mantienen en un archivo de índice.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SET UNIQUE ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ON  
 Especifica que todos los registros con un valor de clave de índice duplicados no se incluirán en el archivo de índice. Solo el primer registro con el valor de clave de índice original se incluye en el archivo de índice.  
  
 OFF  
 (Valor predeterminado). Especifica que los registros con valores de clave de índice duplicados se incluirán en el archivo de índice.  
  
## <a name="remarks"></a>Comentarios  
 Un archivo de índice mantiene su conjunto único cuando se emite REINDIZACIÓN. Para obtener más información, consulte [índice](../../odbc/microsoft/index-command.md).
