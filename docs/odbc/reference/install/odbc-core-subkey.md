---
title: Subclave de núcleo ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f05e36c59d674104dead92ecd7da63f5fb58588a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
