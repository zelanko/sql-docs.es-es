---
title: DLL de seguimiento | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- trace DLLs [ODBC]
- tracing options [ODBC], trace DLLs
ms.assetid: 5ab99bd3-cdc3-4e2c-8827-932d1fcb6e00
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b58f344839a0f8e74fa46c5e788b7835d3eadc2
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="trace-dll"></a>DLL de traza
El archivo DLL que realiza el seguimiento es uno de los componentes principales ODBC. El seguimiento de la DLL se proporciona actualmente como una DLL de ejemplo en el componente ODBC del SDK de Windows y era anteriormente incluida Microsoft Data Access Components (MDAC) SDK. Por lo tanto, la entrada del registro, la interfaz y el código de ejemplo para el archivo DLL de seguimiento están disponibles. Este archivo DLL puede reemplazarse por un seguimiento de la DLL generada por un usuario ODBC o un proveedor de terceros. Una DLL de traza personalizada debe tener un nombre diferente de la DLL de traza de ejemplo original. Archivos DLL de seguimiento deben estar instaladas en el directorio del sistema o se producirá un error al cargar. Las cadenas de conexión no se pasará a la DLL de seguimiento mediante el Administrador de controladores.  
  
 El archivo DLL de seguimiento realiza el seguimiento de argumentos de entrada, argumentos de salida, argumentos aplazados, códigos de retorno y SQLState. Cuando se habilita el seguimiento, el Administrador de controladores llama a la DLL de traza en dos puntos: una vez en la entrada de la función (antes de la validación de argumento) y nuevo justo antes de que la función devuelve.  
  
 Cuando una aplicación llama a una función, el Administrador de controladores llama a una función de seguimiento en el seguimiento DLL antes de llamar a la función en el controlador o el procesamiento de la llamada en Sí. Cada función ODBC tiene una función de seguimiento correspondiente (con el prefijo *seguimiento*) que es idéntica a la función ODBC con el nombre de la excepción. Cuando se llama a la función de seguimiento, el archivo DLL de seguimiento captura los argumentos de entrada y devuelve un código de retorno. Dado que el archivo DLL de seguimiento se llama antes de que el Administrador de controladores valida los argumentos, se realiza un seguimiento en llamadas de función no válida, por lo que se registran los errores de transición de estado y argumentos no válidos.  
  
 Después de llamar a la función de seguimiento en el archivo DLL de seguimiento, el Administrador de controladores llama a la función ODBC en el controlador. A continuación, se llama **TraceReturn** en el archivo DLL de seguimiento. Esta función toma dos argumentos: el valor devuelto por el archivo DLL de seguimiento para la función de seguimiento y el código de retorno devueltos por el controlador para el Administrador de controladores para la función ODBC (o el valor devuelto por el Administrador de controladores Sí si ha procesado la función). La función utiliza el valor devuelto para la función de seguimiento para manipular los valores de argumento de entrada capturada. Escribe el código devuelto para la función ODBC para el archivo de registro (o muestra dinámicamente, si la está habilitada). Desreferencia los punteros de argumento de salida y registra los valores de argumento de salida.
