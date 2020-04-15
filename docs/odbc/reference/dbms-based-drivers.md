---
title: Controladores basados en DBMS (DBMS-Based Drivers) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e7b7b153d0b0cb0a3e6a3d738908b0039b95679
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306491"
---
# <a name="dbms-based-drivers"></a>Controladores basados en DBMS
Los controladores basados en DBMS se utilizan con orígenes de datos como Oracle o SQL Server QUE proporcionan un motor de base de datos independiente para que el controlador lo use. Estos controladores acceden a los datos físicos a través del motor independiente; es decir, envían instrucciones SQL y recuperan resultados del motor.  
  
 Dado que los controladores basados en DBMS utilizan un motor de base de datos existente, suelen ser más fáciles de escribir que los controladores basados en archivos. Aunque un controlador basado en DBMS se puede implementar fácilmente mediante la traducción de llamadas ODBC a llamadas API nativas, esto da como resultado un controlador más lento. Una mejor manera de implementar un controlador basado en DBMS es usar el protocolo de flujo de datos subyacente, que suele ser lo que hace la API nativa. Por ejemplo, un controlador de SQL Server debe usar TDS (el protocolo de secuencia de datos para SQL Server) en lugar de la biblioteca de base de datos (la API nativa para SQL Server). Una excepción a esta regla es cuando ODBC es la API nativa. Por ejemplo, Watcom SQL es un motor independiente que reside en el mismo equipo que la aplicación y se carga directamente como controlador.  
  
 Los controladores basados en DBMS actúan como cliente en una configuración cliente/servidor donde el origen de datos actúa como servidor. En la mayoría de los casos, el cliente (controlador) y el servidor (origen de datos) residen en equipos diferentes, aunque ambos podrían residir en el mismo equipo que ejecuta un sistema operativo multitarea. Una tercera posibilidad es una puerta de *enlace,* que se encuentra entre el controlador y el origen de datos. Una puerta de enlace es una pieza de software que hace que un DBMS se parezca a otro. Por ejemplo, las aplicaciones escritas para usar SQL Server también pueden acceder a datos de DB2 a través de Micro Decisionware DB2 Gateway; este producto hace que DB2 se parezca a SQL Server.  
  
 En la ilustración siguiente se muestran tres configuraciones diferentes de controladores basados en DBMS. En la primera configuración, el controlador y el origen de datos residen en el mismo equipo. En el segundo, el controlador y el origen de datos residen en equipos diferentes. En el tercero, el controlador y el origen de datos residen en diferentes equipos y una puerta de enlace se encuentra entre ellos, que residen en otra máquina.  
  
 ![Tres configuraciones para controladores basados en&#45;DBMS](../../odbc/reference/media/pr07.gif "pr07")
