---
title: Compatibilidad con subprocesos (controlador ODBC de Visual FoxPro) Microsoft Docs
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
ms.openlocfilehash: 2aa19eb233525b5a65ef67fe9903814fc1163177
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303086"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>Compatibilidad con subprocesos (el controlador ODBC de Visual FoxPro)
El controlador ODBC de Visual FoxPro es seguro para subprocesos. El acceso a los identificadores de entorno (*hen*), los identificadores de conexión (*hdbc*) y los identificadores de instrucción (*hstmt*) se ajusta en los semáforos adecuados para evitar que otros procesos accedan y puedan alterar las estructuras de datos internas del controlador.  
  
 En una aplicación multiproceso, puede cancelar una función que se ejecuta sincrónicamente en un *hstmt* llamando a [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) en un subproceso independiente.  
  
 El controlador utiliza un subproceso independiente para capturar datos cuando se usa la obtención progresiva. Para usar la obtención progresiva para un origen de datos, active la casilla **Obtener datos en segundo plano** en el cuadro de diálogo Configuración de ODBC Visual [FoxPro](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) o use la palabra clave de atributo BackgroundFetch en la cadena de conexión. Evite usar la captura en segundo plano cuando llame al controlador desde aplicaciones multiproceso. Para obtener información acerca de las palabras clave de atributo de cadena de conexión, consulte Uso de [cadenas](../../odbc/microsoft/using-connection-strings.md)de conexión .  
  
 Para obtener más información acerca de los subprocesos y **SQLCancel**, vea [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) en la *referencia del programador ODBC*.
