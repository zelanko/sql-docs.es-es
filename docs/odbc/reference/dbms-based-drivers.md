---
title: Controladores basados en DBMS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drivers [ODBC], DBMS-based drivers
- DBMS-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
ms.assetid: e2208ee0-4cd6-4f0d-bb71-a0b54f7d9330
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc35f7bceff2d9e92b70448040bb602117b76c84
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47629643"
---
# <a name="dbms-based-drivers"></a>Controladores basados en DBMS
Se utilizan controladores basados en DBMS con orígenes de datos, como Oracle o SQL Server que proporcionan un motor de base de datos independiente para que use el controlador. Estos controladores, tener acceso a los datos físicos a través del motor independiente; es decir, que enviar instrucciones SQL para y recuperar los resultados del motor.  
  
 Dado que los controladores basados en DBMS utilizan un motor de base de datos existente, son normalmente más fáciles de escribir que controladores basados en archivos. Aunque un controlador basados en DBMS puede implementarse fácilmente mediante la traducción de las llamadas ODBC a llamadas API nativas, esto da como resultado un controlador más lento. Una mejor manera de implementar un controlador basados en DBMS es usar el protocolo de flujo de datos subyacente, que normalmente es lo que hace la API nativa. Por ejemplo, un controlador de SQL Server debe usar TDS (el protocolo flujo de datos para SQL Server) en lugar de la biblioteca de base de datos (la API nativa para SQL Server). Una excepción a esta regla es cuando ODBC es la API nativa. Por ejemplo, Watcom SQL es un motor independiente que reside en el mismo equipo que la aplicación y se carga directamente como el controlador.  
  
 Controladores basados en DBMS actúen como el cliente en una configuración de cliente/servidor donde el origen de datos actúa como el servidor. En la mayoría de los casos, el cliente (controlador) y el servidor (origen de datos) residen en equipos diferentes, aunque puede residir en el mismo equipo que ejecuta un sistema operativo multitarea. Una tercera posibilidad es un *puerta de enlace,* que se encuentra entre el controlador y el origen de datos. Una puerta de enlace es un componente de software que hace que un sistema DBMS sea similar a otro. Por ejemplo, las aplicaciones escritas para utilizar SQL Server también pueden acceder a datos de DB2 a través de la puerta de enlace de Micro Decisionware DB2; Este producto hace que DB2 sea similar a SQL Server.  
  
 La ilustración siguiente muestra tres configuraciones diferentes de controladores basados en DBMS. En la primera configuración, el controlador y el origen de datos residen en el mismo equipo. En el segundo, el controlador y el origen de datos residen en distintas máquinas. En la tercera, el controlador y el origen de datos residen en equipos diferentes y una puerta de enlace se encuentra entre ellos, que reside en otro equipo.  
  
 ![Las tres configuraciones de DBMS&#45;en función de los controladores](../../odbc/reference/media/pr07.gif "pr07")
