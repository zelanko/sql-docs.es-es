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
ms.openlocfilehash: fcd2221d9a0bb9cba42745901e5f00a6f8c8415e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68111248"
---
# <a name="dbms-based-drivers"></a>Controladores basados en DBMS
Los controladores basados en DBMS se utilizan con orígenes de datos como Oracle o SQL Server que proporcionan un motor de base de datos independiente para que lo use el controlador. Estos controladores acceden a los datos físicos a través del motor independiente; es decir, envían instrucciones SQL a y recuperan los resultados del motor de.  
  
 Dado que los controladores basados en DBMS usan un motor de base de datos existente, suelen ser más fáciles de escribir que los controladores basados en archivos. Aunque un controlador basado en DBMS se puede implementar fácilmente mediante la traducción de llamadas ODBC a llamadas API nativas, el resultado es un controlador más lento. Una manera mejor de implementar un controlador basado en DBMS es usar el protocolo de secuencia de datos subyacente, que normalmente es lo que hace la API nativa. Por ejemplo, un controlador de SQL Server debe usar TDS (el protocolo de flujo de datos para SQL Server) en lugar de la biblioteca de base de datos (la API nativa para SQL Server). Una excepción a esta regla es cuando ODBC es la API nativa. Por ejemplo, Watcom SQL es un motor independiente que reside en el mismo equipo que la aplicación y que se carga directamente como el controlador.  
  
 Los controladores basados en DBMS actúan como el cliente en una configuración de cliente/servidor en la que el origen de datos actúa como servidor. En la mayoría de los casos, el cliente (controlador) y el servidor (origen de datos) residen en equipos diferentes, aunque ambos podrían residir en el mismo equipo que ejecuta un sistema operativo multitarea. Una tercera posibilidad es una *puerta de enlace,* que se encuentra entre el controlador y el origen de datos. Una puerta de enlace es un elemento de software que hace que un DBMS tenga el mismo aspecto que otro. Por ejemplo, las aplicaciones escritas para usar SQL Server también pueden acceder a los datos de DB2 a través de la puerta de enlace DB2 de micro decisionware; Este producto hace que DB2 tenga el siguiente aspecto SQL Server.  
  
 En la siguiente ilustración se muestran tres configuraciones diferentes de controladores basados en DBMS. En la primera configuración, el controlador y el origen de datos residen en el mismo equipo. En el segundo, el controlador y el origen de datos residen en equipos diferentes. En el tercero, el controlador y el origen de datos residen en equipos diferentes y una puerta de enlace se encuentra entre ellos y reside en otra máquina.  
  
 ![Tres configuraciones para los controladores basados en&#45;de DBMS](../../odbc/reference/media/pr07.gif "pr07")
