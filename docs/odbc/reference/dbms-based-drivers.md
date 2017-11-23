---
title: Controladores basados en DBMS | Documentos de Microsoft
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
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7b806f4c887af3f1ba80ee3321820e97dd336fad
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="dbms-based-drivers"></a>Controladores basados en DBMS
Se utilizan controladores basados en DBMS con orígenes de datos como Oracle o SQL Server que proporcionan un motor de base de datos independiente para el controlador que se utilizará. Estos controladores de tener acceso a los datos físicos a través del motor independiente; es decir, que enviar instrucciones SQL y recuperar los resultados del motor de.  
  
 Dado que controladores basados en DBMS utilizan un motor de base de datos existente, son normalmente más fáciles de escribir que los controladores basados en archivos. Aunque un controlador basados en DBMS puede implementarse fácilmente mediante la traducción de llamadas ODBC a las llamadas API nativas, esto da como resultado un controlador más lento. Una mejor manera de implementar un controlador basados en DBMS es usar el protocolo de flujo de datos subyacente, que normalmente es lo que hace la API nativa. Por ejemplo, un controlador de SQL Server debe usar TDS (el protocolo flujo de datos para SQL Server) en lugar de la biblioteca de base de datos (la API nativa de SQL Server). Una excepción a esta regla es cuando ODBC es la API nativa. Por ejemplo, Watcom SQL es un motor independiente que se encuentra en el mismo equipo que la aplicación y se carga directamente como el controlador.  
  
 Controladores basados en DBMS actúan como el cliente en una configuración de cliente/servidor que el origen de datos actúa como el servidor. En la mayoría de los casos, el cliente (controlador) y el servidor (origen de datos) residen en equipos diferentes, aunque puede residir en el mismo equipo que ejecuta un sistema operativo multitarea. Una tercera posibilidad es un *puerta de enlace,* que se encuentra entre el controlador y el origen de datos. Una puerta de enlace es un fragmento de software que hace que un DBMS que se parezca a otro. Por ejemplo, las aplicaciones escritas para utilizar SQL Server pueden también tener acceso a datos de DB2 a través de la puerta de enlace de Micro Decisionware DB2; Este producto hace DB2 que se parezca a SQL Server.  
  
 La ilustración siguiente muestra tres distintas configuraciones de controladores basados en DBMS. En la primera configuración, el controlador y el origen de datos residen en el mismo equipo. En el segundo, el controlador y el origen de datos residen en equipos diferentes. En la tercera, el controlador y el origen de datos residen en equipos diferentes y una puerta de enlace se ubica entre ellos, que reside en otro equipo.  
  
 ![Tres configuraciones para DBMS &#45; controladores basados en](../../odbc/reference/media/pr07.gif "pr07")
