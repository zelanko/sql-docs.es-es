---
title: (Controlador ODBC de Visual FoxPro) de compatibilidad con subprocesos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 72672cfc20b5d363229fd1ba49278d11e6d6793d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912416"
---
# <a name="thread-support-visual-foxpro-odbc-driver"></a>Compatibilidad con subprocesos (el controlador ODBC de Visual FoxPro)
El controlador ODBC de Visual FoxPro es segura para subprocesos. Acceso a los identificadores de entorno (*hen*), identificadores de conexión (*hdbc*) y los identificadores de instrucciones (*hstmt*) se ajusta en semáforos adecuados para evitar que otros procesos obtengan acceso y posiblemente modificar estructuras de datos internas del controlador.  
  
 En una aplicación multiproceso, puede cancelar una función que se está ejecutando de forma sincrónica en un *hstmt* mediante una llamada a [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md) en un subproceso independiente.  
  
 El controlador utiliza un subproceso independiente para capturar los datos cuando se usa capturando progresiva. Para utilizar la obtención de progresiva para un origen de datos, seleccione el **capturar los datos en segundo plano** casilla de verificación en la [cuadro de diálogo del programa de instalación de Visual FoxPro ODBC](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md) o usar la palabra clave de atributo BackgroundFetch en la conexión cadena. Evite el uso de captura en segundo plano cuando se llama el controlador de aplicaciones multiproceso. Para obtener información sobre palabras clave de atributo de cadena de conexión, vea [utilizando las cadenas de conexión](../../odbc/microsoft/using-connection-strings.md).  
  
 Para obtener más información sobre los subprocesos y **SQLCancel**, consulte [SQLCancel](../../odbc/reference/syntax/sqlcancel-function.md) en el *referencia del programador de ODBC*.
