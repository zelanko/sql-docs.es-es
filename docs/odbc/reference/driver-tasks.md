---
title: Tareas de controlador | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915458"
---
# <a name="driver-tasks"></a>Tareas de controlador
Tareas específicas realizadas por los controladores incluyen:  
  
-   La conexión y desconexión del origen de datos.  
  
-   Comprueba si hay errores de función no comprueba por el Administrador de controladores.  
  
-   Iniciar las transacciones. Esto es transparente para la aplicación.  
  
-   Enviar instrucciones SQL para el origen de datos para su ejecución. El controlador debe modificar SQL de ODBC para DBMS específicos SQL; Esto suele limitarse a reemplazando las cláusulas de escape que se definen en ODBC con SQL específicos para DBMS.  
  
-   Enviar y recuperar datos de origen de datos, incluyendo la conversión de tipos de datos según lo especificado por la aplicación.  
  
-   Asignación de errores específicos de DBMS para SQLSTATE de ODBC.
