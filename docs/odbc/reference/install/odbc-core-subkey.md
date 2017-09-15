---
title: "Subclave de núcleo ODBC | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ad7a45f0f3272e1e2d7ae799ab1ca86bfb90b9be
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
