---
description: Secuencia de registros de estado
title: Secuencia de registros de estado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], diagnostic records
- status records [ODBC]
- diagnostic records [ODBC]
ms.assetid: 0e0436cc-230f-44b0-b373-04a57e83ee76
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b2cb519cab987a1abd924f1b779a7f07c3201475
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476457"
---
# <a name="sequence-of-status-records"></a>Secuencia de registros de estado
Si se devuelven dos o más registros de estado, el administrador de controladores y el controlador los clasifican según las reglas siguientes. El registro con el rango más alto es el primer registro. El origen de un registro (Administrador de controladores, controlador, puerta de enlace, etc.) no se tiene en cuenta al clasificar registros.  
  
-   **Errores** de Los registros de estado que describen los errores tienen el rango más alto. Entre los registros de errores, los registros que indican un error en la transacción o un posible error de transacción se sobreclasifican todos los demás registros. Si dos o más registros describen la misma condición de error, SQLSTATEs definida por la especificación Open Group CLI (clases de 03 a HZ) de la jerarquía definida por ODBC y la SQLSTATEs definida por el controlador.  
  
-   **No hay valores de datos definidos por la implementación** Los registros de estado que describen valores no de datos definidos por el controlador (clase 02) tienen el segundo rango más alto.  
  
-   **Advertencias** Los registros de estado que describen las advertencias (clase 01) tienen el rango más bajo. Si dos o más registros describen la misma condición de advertencia, se SQLSTATEs la advertencia definida por la especificación de la CLI Open Group y el SQLSTATEs definido por el controlador.  
  
 Si hay dos o más registros con el rango más alto, no está definido qué registro es el primer registro. El orden de todos los demás registros es indefinido. En concreto, dado que las advertencias pueden aparecer antes que los errores, las aplicaciones deben comprobar todos los registros de estado cuando una función devuelve un valor distinto de SQL_SUCCESS.
