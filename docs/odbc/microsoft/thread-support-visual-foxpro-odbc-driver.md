---
description: Compatibilidad con subprocesos (el controlador ODBC de Visual FoxPro)
title: Compatibilidad con subprocesos (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- thread support [ODBC]
- Visual FoxPro ODBC driver [ODBC], thread support
- FoxPro ODBC driver [ODBC], thread support
- multithreaded applications [ODBC]
ms.assetid: 0c6abbbc-012b-41aa-bded-5e7e362d015b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 013ccd1f5d202794ba6b7a44c10339dd14c08d17
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449077"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>Compatibilidad con subprocesos (el controlador ODBC de Visual FoxPro)
El controlador ODBC de Visual FoxPro es seguro para subprocesos. El acceso a los identificadores de entorno (*gallina*), los identificadores de conexión (*hdbc*) y los identificadores de instrucción (*hstmt*) se encapsula en los semáforos adecuados para evitar que otros procesos obtengan acceso a las estructuras de datos internas del controlador y puedan alterarlas.  
  
 En una aplicación multiproceso, puede cancelar una función que se ejecuta de forma sincrónica en un *hstmt* llamando a [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) en un subproceso independiente.  
  
 El controlador usa un subproceso independiente para capturar datos cuando se usa la captura progresiva. Para usar la captura progresiva para un origen de datos, active la casilla **capturar datos en segundo plano** en el [cuadro de diálogo Configuración de ODBC Visual FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) o use la palabra clave del atributo BackgroundFetch en la cadena de conexión. Evite el uso de la captura en segundo plano cuando llame al controlador desde aplicaciones multiproceso. Para obtener información sobre las palabras clave de atributo de cadena de conexión, vea [usar cadenas de conexión](../../odbc/microsoft/using-connection-strings.md).  
  
 Para obtener más información sobre los subprocesos y **SQLCancel**, vea [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) en la *Referencia del programador de ODBC*.
