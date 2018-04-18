---
title: Tareas de controlador | Documentos de Microsoft
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
ms.topic: article
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0ded25d00f66e3acb11e2e4d529684ed9551faa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="driver-tasks"></a>Tareas de controlador
Tareas específicas realizadas por los controladores incluyen:  
  
-   Conectarse y desconectarse del origen de datos.  
  
-   Comprueba si hay errores de función no activados por el Administrador de controladores.  
  
-   Iniciar transacciones; Este proceso es transparente para la aplicación.  
  
-   Enviando instrucciones SQL al origen de datos para su ejecución. El controlador debe modificar SQL de ODBC para DBMS específicos SQL; Esto a menudo se limita a reemplazar cláusulas de escape que se definen en ODBC con SQL específicos de DBMS.  
  
-   Enviar datos y recuperar datos del origen de datos, incluyendo la conversión de tipos de datos de acuerdo con lo especificado por la aplicación.  
  
-   Asignación de errores específicos de DBMS para SQLSTATE de ODBC.
