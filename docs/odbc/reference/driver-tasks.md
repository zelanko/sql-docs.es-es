---
title: Tareas del conductor ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1b30df63a3c955d2ed074ab13649ea55c21a6da7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294205"
---
# <a name="driver-tasks"></a>Tareas de controlador
Las tareas específicas realizadas por los conductores incluyen:  
  
-   Conexión y desconexión del origen de datos.  
  
-   Comprobación de errores de función no comprobados por el Administrador de controladores.  
  
-   Iniciar transacciones; esto es transparente para la aplicación.  
  
-   Envío de instrucciones SQL al origen de datos para su ejecución. El controlador debe modificar ODBC SQL a SQL específico de DBMS; esto se limita a suponer cláusulas de escape definidas por ODBC por SQL específico de DBMS.  
  
-   Enviar datos y recuperar datos del origen de datos, incluida la conversión de tipos de datos según lo especificado por la aplicación.  
  
-   Asignación de errores específicos de DBMS a SQLSTATEs ODBC.
