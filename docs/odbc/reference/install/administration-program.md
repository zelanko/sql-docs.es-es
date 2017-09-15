---
title: "Programa de administración | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 476c4710a4265214235bdd7b80a330fad5b37f34
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="administration-program"></a>Programa de administración
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo de Windows. Solo explícitamente debe instalar ODBC en versiones anteriores de Windows.  
  
 Un programa de administración, el Administrador de ODBC, se incluye con el SDK de MDAC/SDK de Windows. Este programa y puede distribuirse por los usuarios SDK de. Además, los programadores pueden escribir sus propios programas de administración. Por lo general, los desarrolladores escribir sus propios programas de administración solo si desean conservar un control completo sobre la configuración del origen de datos, o si va a configurar orígenes de datos directamente desde una aplicación que actúa como un programa de administración. Por ejemplo, un programa de hoja de cálculo puede permitir a los usuarios agregar y, a continuación, utilizar orígenes de datos en tiempo de ejecución.  
  
 El programa de administración carga por primera vez el archivo DLL del instalador. A continuación, llama a funciones en el instalador de DLL para realizar las tareas siguientes:  
  
-   **Agregar, modificar o eliminar orígenes de datos de forma interactiva.** El programa de administración puede llamar a **SQLManageDataSources**, **SQLCreateDataSource**, o **SQLConfigDataSource**.  
  
     **SQLManageDataSources** muestra un cuadro de diálogo con el que el usuario puede agregar, modificar, o eliminar orígenes de datos y especificar opciones de seguimiento; esta función se invoca cuando se invoca el archivo DLL del programa de instalación directamente desde el Panel de Control. **SQLCreateDataSource** muestra un cuadro de diálogo con el que el usuario solo puede agregar orígenes de datos. **SQLConfigDataSource** pasa la llamada directamente a la DLL de la instalación de controladores.  
  
     En todos los casos, el programa de instalación DLL llama **ConfigDSN** en el programa de instalación de controlador DLL para agregar, modificar o eliminar el origen de datos. El programa de instalación de controlador DLL podría solicitar al usuario para obtener información adicional.  
  
-   **Agregar, modificar o eliminar orígenes de datos en modo silencioso.** El programa de administración llame **SQLConfigDataSource** en la DLL del instalador y pasa que una ventana null controlar, el nombre de un origen de datos para agregar, modificar o eliminar y una lista de valores para el registro. Las llamadas DLL de instalador **ConfigDSN** en el programa de instalación de controlador DLL para agregar, modificar o eliminar el origen de datos.  
  
-   **Agregar, modificar o eliminar un origen de datos predeterminado.** El origen de datos predeterminado es igual que cualquier otro origen de datos, salvo que su nombre es el valor predeterminado. Se agrega, modifica o elimina de la misma forma que cualquier otro origen de datos.
