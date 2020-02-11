---
title: Uso de Microsoft Internet Information Services | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], IIS
- internet information services [ODBC]
- IIS [ODBC]
ms.assetid: 3328f2f1-b34a-472f-82cf-ad49768ff061
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9e531149af21facd80e9e6ddab19a76c3bdc0fa6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088140"
---
# <a name="using-microsoft-internet-information-services"></a>Con servicios de Microsoft Internet Information Server
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Si tiene dificultades para conectarse desde un script de IIS (especialmente si recibe un error ORA-12641), agregue la línea siguiente al archivo archivo sqlnet. ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 Esto deshabilitará la Network Services segura para que pueda conectarse mediante la autenticación anónima.
