---
title: DLL de seguimiento ( Trace DLL) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e1f9dc57415ad9865ca1b2ad02487b62a93f18f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298075"
---
# <a name="trace-dll"></a>DLL de traza
El archivo DLL que realiza el seguimiento es uno de los componentes principales de ODBC. El archivo DLL de seguimiento se proporciona actualmente como un archivo DLL de ejemplo en el componente ODBC del Windows SDK y anteriormente se incluía el SDK de microsoft Data Access Components (MDAC). Por lo tanto, la entrada del Registro, la interfaz y el código de ejemplo para el archivo DLL de seguimiento están disponibles. Este archivo DLL se puede reemplazar por un archivo DLL de seguimiento generado por un usuario ODBC o un proveedor de terceros. Un archivo DLL de seguimiento personalizado debe tener un nombre diferente al archivo DLL de seguimiento de ejemplo original. Los archivos DLL de seguimiento deben estar instalados en el directorio del sistema o no se cargarán. El Administrador de controladores no pasará las cadenas de conexión al archivo DLL de seguimiento.  
  
 El archivo DLL de seguimiento realiza un seguimiento de los argumentos de entrada, los argumentos de salida, los argumentos diferidos, los códigos de retorno y los SQLSTATEs. Cuando se habilita el seguimiento, el Administrador de controladores llama al archivo DLL de seguimiento en dos puntos: una vez en la entrada de la función (antes de la validación del argumento) y de nuevo justo antes de que se devuelva la función.  
  
 Cuando una aplicación llama a una función, el Administrador de controladores llama a una función de seguimiento en el archivo DLL de seguimiento antes de llamar a la función en el controlador o procesar la propia llamada. Cada función ODBC tiene una función de seguimiento correspondiente (prefijada con *Trace*) que es idéntica a la función ODBC con la excepción del nombre. Cuando se llama a la función de seguimiento, el archivo DLL de seguimiento captura los argumentos de entrada y devuelve un código de retorno. Dado que se llama al archivo DLL de seguimiento antes de que el Administrador de controladores valide argumentos, se realiza un seguimiento de las llamadas a funciones no válidas, por lo que se registran los errores de transición de estado y los argumentos no válidos.  
  
 Después de llamar a la función de seguimiento en el archivo DLL de seguimiento, el Administrador de controladores llama a la función ODBC en el controlador. A continuación, llama a **TraceReturn** en el archivo DLL de seguimiento. Esta función toma dos argumentos: el valor devuelto por el archivo DLL de seguimiento para la función de seguimiento y el código de retorno devuelto por el controlador al Administrador de controladores para la función ODBC (o el valor devuelto por el propio Administrador de controladores si procesó la función). La función utiliza el valor devuelto para la función de seguimiento para manipular los valores de argumento de entrada capturados. Escribe el código devuelto para la función ODBC en el archivo de registro (o lo muestra dinámicamente, si está habilitado). Desreferencia los punteros del argumento de salida y registra los valores del argumento de salida.
