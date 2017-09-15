---
title: Con servicios de Microsoft Internet Information Server | Documentos de Microsoft
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
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 75659769b4d0318fa21494a3f2ca3262836c69eb
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-microsoft-internet-information-services"></a>Con servicios de Microsoft Internet Information Server
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Si tiene dificultades para conectarse desde dentro de una secuencia de comandos IIS (especialmente si se recibe un error ORA-12641), agregue la siguiente línea al archivo Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 Esto deshabilitará los servicios de red seguros para que pueda conectarse mediante la autenticación anónima.
