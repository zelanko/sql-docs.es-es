---
title: Seguimiento | Documentos de Microsoft
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
ms.topic: conceptual
helpviewer_keywords:
- tracing options [ODBC], about tracing
- driver manager [ODBC], tracing
ms.assetid: 77ed4c6c-d976-4eb2-8526-a12697b0ef83
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7549f0790aa13882dc04ead78f097cf0035993e6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="tracing"></a>Seguimiento
El Administrador de controladores ODBC tiene una utilidad de seguimiento que permite a la secuencia de llamadas a funciones realizadas por una aplicación ODBC se registran y transcripción en un archivo de registro. El seguimiento se realiza mediante una DLL de seguimiento que captura llamadas realizadas entre la aplicación y el Administrador de controladores y entre el Administrador de controladores y el controlador. Este método de creación de trazas sustituye el seguimiento realizado por la API ODBC 2 *.x* Administrador de controladores y el seguimiento se realizan en ODBC 2 *.x* por ODBC Spy.  
  
 Esta sección contiene los temas siguientes.  
  
-   [DLL de traza](../../../odbc/reference/develop-app/trace-dll.md)  
  
-   [Archivo de seguimiento](../../../odbc/reference/develop-app/trace-file.md)  
  
-   [La habilitación del seguimiento](../../../odbc/reference/develop-app/enabling-tracing.md)  
  
-   [Seguimiento dinámico](../../../odbc/reference/develop-app/dynamic-tracing.md)
