---
description: Arquitectura de controladores
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 530940cef233b8a6b6a3f5c0575dd154998126cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494618"
---
# <a name="driver-architecture"></a>Arquitectura de controladores
La arquitectura de los controladores se divide en dos categorías, dependiendo del software que procese las instrucciones SQL:  
  
-   **Controladores basados en archivos** El controlador accede directamente a los datos físicos. En este caso, el controlador actúa como el controlador y el origen de datos; es decir, procesa las llamadas ODBC y las instrucciones SQL. Por ejemplo, los controladores dBASE son controladores basados en archivos porque dBASE no proporciona un motor de base de datos independiente que pueda usar el controlador. Es importante tener en cuenta que los desarrolladores de controladores basados en archivos deben escribir sus propios motores de base de datos.  
  
-   **Controladores basados en DBMS** El controlador obtiene acceso a los datos físicos a través de un motor de base de datos independiente. En este caso, el controlador solo procesa las llamadas ODBC; pasa instrucciones SQL al motor de base de datos para su procesamiento. Por ejemplo, los controladores de Oracle son controladores basados en DBMS porque Oracle tiene un motor de base de datos independiente que utiliza el controlador. El lugar en el que reside el motor de base de datos es irrelevante. Puede residir en el mismo equipo que el controlador o en otro equipo de la red. incluso se puede tener acceso a ella a través de una puerta de enlace.  
  
 La arquitectura de controladores es generalmente interesante solo para escritores de controladores; es decir, la arquitectura de controladores generalmente no hace ninguna diferencia en la aplicación. Sin embargo, la arquitectura puede afectar a si una aplicación puede usar SQL específico del DBMS. Por ejemplo, Microsoft Access proporciona un motor de base de datos independiente. Si un controlador de Microsoft Access está basado en DBMS, tiene acceso a los datos a través de este motor; la aplicación puede pasar instrucciones SQL de Microsoft Access-SQL al motor para su procesamiento.  
  
 Sin embargo, si el controlador está basado en archivos, es decir, contiene un motor propietario que accede directamente al archivo. mdb de Microsoft® Access, cualquier intento de pasar instrucciones SQL específicas de Microsoft Access al motor es probable que se produzcan errores de sintaxis. La razón es que el motor propietario es probable que implemente solo ODBC SQL.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Controladores basados en archivos](../../odbc/reference/file-based-drivers.md)  
  
-   [Controladores basados en DBMS](../../odbc/reference/dbms-based-drivers.md)  
  
-   [Ejemplo de red](../../odbc/reference/network-example.md)  
  
-   [Otras arquitecturas de controlador](../../odbc/reference/other-driver-architectures.md)
