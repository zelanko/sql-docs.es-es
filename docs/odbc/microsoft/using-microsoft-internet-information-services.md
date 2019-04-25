---
title: Mediante Microsoft Internet Information Services | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 509979a38e6d7e71f979ce317b9e1626a85c5a54
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633395"
---
# <a name="using-microsoft-internet-information-services"></a>Con servicios de Microsoft Internet Information Server
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 Si tiene dificultades para conectarse desde dentro de una secuencia de comandos IIS (especialmente si se recibe un error ORA-12641), agregue la siguiente línea al archivo Sqlnet.ora:  
  
```  
SQLNET.AUTHENTICATION_SERVICES = (none)  
```  
  
 Esto deshabilitará los servicios de red seguro para que pueda conectarse mediante la autenticación anónima.
