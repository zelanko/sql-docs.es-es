---
title: Arquitectura de controladores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], architecture
ms.assetid: c5003413-0cc1-4f41-b877-a64e2f5ab118
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd9bbb74d77a0b56b6b1f1aa5d8f1a6b5e97f5aa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915475"
---
# <a name="driver-architecture"></a>Arquitectura de controladores
Arquitectura de controladores se divide en dos categorías, dependiendo de qué instrucciones SQL de procesos de software:  
  
-   **Controladores basados en archivos** el controlador tiene acceso directo a los datos físicos. En este caso, el controlador actúa como controlador y el origen de datos; es decir, lo procesa las llamadas ODBC e instrucciones SQL. Por ejemplo, dBASE controladores son basados en archivos porque dBASE no proporciona que un motor de base de datos independiente del controlador se puede usar. Es importante tener en cuenta que los desarrolladores de controladores basados en archivo deben escribir sus propios motores de base de datos.  
  
-   **Controladores basados en DBMS** el controlador tiene acceso a los datos físicos a través de un motor de base de datos independiente. En este caso, el controlador procesa solo las llamadas ODBC; instrucciones SQL pasa al motor de base de datos para procesar. Por ejemplo, los controladores de Oracle son controladores basados en DBMS porque Oracle tiene un motor de base de datos independiente que utiliza el controlador. En el que reside el motor de base de datos es irrelevante. Puede residir en el mismo equipo que el controlador o un equipo diferente en la red. incluso puede obtenerse a través de una puerta de enlace.  
  
 Arquitectura de controladores es interesante por lo general solo a los escritores de controladores; es decir, arquitectura de controladores por lo general no hay ninguna diferencia a la aplicación. Sin embargo, la arquitectura puede determinar si una aplicación puede usar SQL específicos para DBMS. Por ejemplo, Microsoft Access proporciona un motor de base de datos independiente. Si un controlador de Microsoft Access es basados en DBMS, tiene acceso a los datos a través de este motor - la aplicación puede pasar las instrucciones SQL de Microsoft Access para el motor para su procesamiento.  
  
 Sin embargo, si el controlador está basado en archivos, es decir, contiene un motor de propiedad que tiene acceso el archivo .mdb de Microsoft® Access directamente - cualquier intento de pasar las instrucciones SQL específicas de Microsoft Access para el motor suelen dar lugar a errores de sintaxis. El motivo es que el motor de propietario es probable que implementar sólo ODBC SQL.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Controladores basados en archivos](../../odbc/reference/file-based-drivers.md)  
  
-   [Controladores basados en DBMS](../../odbc/reference/dbms-based-drivers.md)  
  
-   [Ejemplo de red](../../odbc/reference/network-example.md)  
  
-   [Otras arquitecturas de controlador](../../odbc/reference/other-driver-architectures.md)
