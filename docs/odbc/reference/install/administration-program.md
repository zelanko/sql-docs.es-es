---
title: Programa de administración | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9cb78dae32bb17598ee0e86c26e621be1b6362c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068551"
---
# <a name="administration-program"></a>Programa de administración
> [!NOTE]  
>  Desde Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. ODBC explícitamente sólo debe instalar en versiones anteriores de Windows.  
  
 Un programa de administración, el Administrador ODBC, se incluye con el SDK de MDAC/SDK de Windows. Este programa y puede distribuirse por los usuarios del SDK. Además, los desarrolladores pueden escribir sus propios programas de administración. Por lo general, los desarrolladores escribir sus propios programas de administración solo si desean conservar el control completo sobre la configuración de orígenes de datos, o si están configurando los orígenes de datos directamente desde una aplicación que actúa como un programa de administración. Por ejemplo, un programa de hoja de cálculo podría permitir a los usuarios agregar y, a continuación, utilizar orígenes de datos en tiempo de ejecución.  
  
 El programa de administración carga por primera vez el archivo DLL de instalador. A continuación, llama a funciones en el instalador de DLL para realizar las tareas siguientes:  
  
-   **Agregar, modificar o eliminar orígenes de datos de forma interactiva.** El programa de administración puede llamar a **SQLManageDataSources**, **SQLCreateDataSource**, o **SQLConfigDataSource**.  
  
     **SQLManageDataSources** muestra un cuadro de diálogo con el que el usuario puede agregar, modificar, o eliminar orígenes de datos y especifique las opciones de seguimiento; esta función se invoca cuando se invoca el archivo DLL de instalador directamente desde el Panel de Control. **SQLCreateDataSource** muestra un cuadro de diálogo con el que el usuario solo puede agregar orígenes de datos. **SQLConfigDataSource** pasa la llamada directamente a la DLL de instalación de controlador.  
  
     En todos los casos, llama la DLL de instalador **ConfigDSN** en el programa de instalación de controlador DLL para agregar, modificar o eliminar el origen de datos. La configuración del controlador de archivo DLL podría preguntar al usuario para obtener más información.  
  
-   **Agregar, modificar o eliminar orígenes de datos en modo silencioso.** Las llamadas del programa de administración **SQLConfigDataSource** en el archivo DLL de instalador y pasadas que una ventana nula controlar, el nombre de un origen de datos para agregar, modificar o eliminar y una lista de valores para el registro. Las llamadas DLL de instalador **ConfigDSN** en el programa de instalación de controlador DLL para agregar, modificar o eliminar el origen de datos.  
  
-   **Agregar, modificar o eliminar un origen de datos de forma predeterminada.** El origen de datos predeterminada es igual que cualquier otro origen de datos, excepto en que su nombre es el valor predeterminado. Está agregado, modificado o eliminado en la misma manera que cualquier otro origen de datos.
