---
title: Tareas del controlador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e2ed50ac3f9e914953abdd64907199a5f978af2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915458"
---
# <a name="driver-tasks"></a>Tareas de controlador
Entre las tareas específicas realizadas por los controladores se incluyen las siguientes:  
  
-   Conectarse y desconectarse del origen de datos.  
  
-   Comprobando si hay errores de función no comprobados por el administrador de controladores.  
  
-   Iniciar transacciones; Esto es transparente para la aplicación.  
  
-   Enviar instrucciones SQL al origen de datos para su ejecución. El controlador debe modificar SQL ODBC a SQL específico de DBMS; a menudo, esto se limita al reemplazo de cláusulas de escape definidas por ODBC con SQL específico del DBMS.  
  
-   Enviar y recuperar datos del origen de datos, incluida la conversión de los tipos de datos especificados por la aplicación.  
  
-   Asignación de errores específicos de DBMS a SQLSTATEs de ODBC.
