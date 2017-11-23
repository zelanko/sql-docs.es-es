---
title: "Subclave de núcleo ODBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 85c4e842ef48f412696c4a0c851480915f5d9b27
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-core-subkey"></a>Subclave de núcleo ODBC
El valor bajo la subclave de núcleo de ODBC proporciona el contador de uso para los componentes principales (Administrador de controladores, biblioteca de cursores, installer DLL y así sucesivamente). El formato de este valor se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*Recuento*|  
  
 Por ejemplo, suponga que ha instalado los componentes de núcleo de ODBC por los programas de instalación de controladores diferentes dos y tres aplicaciones diferentes. El valor bajo la subclave de núcleo de ODBC sería:  
  
```  
UsageCount : REG_DWORD : 0x5  
```
