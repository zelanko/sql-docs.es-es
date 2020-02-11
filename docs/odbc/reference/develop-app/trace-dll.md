---
title: DLL de seguimiento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- trace DLLs [ODBC]
- tracing options [ODBC], trace DLLs
ms.assetid: 5ab99bd3-cdc3-4e2c-8827-932d1fcb6e00
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6fe910c93beac676e5fb0f663b740c03a826c326
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67985223"
---
# <a name="trace-dll"></a>DLL de traza
El archivo DLL que realiza el seguimiento es uno de los componentes principales de ODBC. El archivo DLL de seguimiento se proporciona actualmente como un archivo DLL de ejemplo en el componente ODBC del Windows SDK y anteriormente se incluía el SDK de Microsoft Data Access Components (MDAC). Por lo tanto, están disponibles la entrada del registro, la interfaz y el código de ejemplo para el archivo DLL de seguimiento. Este archivo DLL se puede reemplazar por un archivo DLL de seguimiento generado por un usuario ODBC o un proveedor de terceros. Un archivo DLL de seguimiento personalizado debe tener un nombre distinto al del archivo DLL de seguimiento de ejemplo original. Los archivos dll de seguimiento deben estar instalados en el directorio del sistema o no se cargarán. El administrador de controladores no pasará las cadenas de conexión al archivo DLL de seguimiento.  
  
 El archivo DLL de seguimiento realiza un seguimiento de los argumentos de entrada, los argumentos de salida, los argumentos diferidos, los códigos de retorno y SQLSTATEs. Cuando el seguimiento está habilitado, el administrador de controladores llama a la DLL de seguimiento en dos puntos: una vez en la entrada de la función (antes de la validación de argumentos) y de nuevo justo antes de que la función devuelva un valor.  
  
 Cuando una aplicación llama a una función, el administrador de controladores llama a una función de seguimiento en el archivo DLL de seguimiento antes de llamar a la función en el controlador o procesar la propia llamada. Cada función ODBC tiene una función de seguimiento correspondiente (con el prefijo *Trace*) que es idéntica a la función ODBC con la excepción del nombre. Cuando se llama a la función trace, el archivo DLL de seguimiento captura los argumentos de entrada y devuelve un código de retorno. Dado que se llama a la DLL de seguimiento antes de que el administrador de controladores valide los argumentos, se realiza un seguimiento de las llamadas de función no válidas, por lo que los errores de transición de estado y los argumentos no válidos  
  
 Después de llamar a la función trace en el archivo DLL de seguimiento, el administrador de controladores llama a la función ODBC en el controlador. A continuación, llama a **TraceReturn** en el archivo dll de seguimiento. Esta función toma dos argumentos: el valor devuelto por la DLL de seguimiento para la función trace y el código de retorno devuelto por el controlador al administrador de controladores para la función ODBC (o el valor devuelto por el propio administrador de controladores si ha procesado la función). La función utiliza el valor devuelto por la función trace para manipular los valores de los argumentos de entrada capturados. Escribe el código devuelto para la función ODBC en el archivo de registro (o lo muestra dinámicamente, si está habilitado). Desreferencia los punteros de argumento de salida y registra los valores de los argumentos de salida.
