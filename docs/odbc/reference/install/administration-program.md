---
title: Programa de Administración (Administración) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d8a2a8363371d6f6c3644c2b7b49aa77644d496e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306646"
---
# <a name="administration-program"></a>Programa de administración
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar ODBC explícitamente en versiones anteriores de Windows.  
  
 Un programa de administración, el Administrador ODBC, se incluye con el SDK de Windows SDK/MDAC. Este programa puede ser redistribuido por los usuarios del SDK. Además, los desarrolladores pueden escribir sus propios programas de administración. Por lo general, los desarrolladores escriben sus propios programas de administración solo si desean conservar el control total sobre la configuración del origen de datos o si configuran orígenes de datos directamente desde una aplicación que actúa como un programa de administración. Por ejemplo, un programa de hoja de cálculo puede permitir a los usuarios agregar y, a continuación, usar orígenes de datos en tiempo de ejecución.  
  
 El programa de administración carga primero el archivo DLL del instalador. A continuación, llama a funciones en el archivo DLL del instalador para realizar las siguientes tareas:  
  
-   **Agregue, modifique o elimine orígenes de datos de forma interactiva.** El programa de administración puede llamar a **SQLManageDataSources**, **SQLCreateDataSource**o **SQLConfigDataSource**.  
  
     **SQLManageDataSources** muestra un cuadro de diálogo con el que el usuario puede agregar, modificar o eliminar orígenes de datos y especificar opciones de seguimiento; Se llama a esta función cuando se invoca el archivo DLL del instalador directamente desde el Panel de control. **SQLCreateDataSource** muestra un cuadro de diálogo con el que el usuario solo puede agregar orígenes de datos. **SQLConfigDataSource** pasa la llamada directamente al archivo DLL de instalación del controlador.  
  
     En todos los casos, el archivo DLL del instalador llama a **ConfigDSN** en el archivo DLL de instalación del controlador para agregar, modificar o eliminar realmente el origen de datos. El archivo DLL de instalación del controlador puede solicitar al usuario información adicional.  
  
-   **Agregue, modifique o elimine orígenes de datos de forma silenciosa.** El programa de administración llama a **SQLConfigDataSource** en el archivo DLL del instalador y le pasa un identificador de ventana nulo, el nombre de un origen de datos para agregar, modificar o eliminar y una lista de valores para el registro. El archivo DLL del instalador llama a **ConfigDSN** en el archivo DLL de instalación del controlador para agregar, modificar o eliminar realmente el origen de datos.  
  
-   **Agregar, modificar o eliminar un origen de datos predeterminado.** El origen de datos predeterminado es el mismo que cualquier otro origen de datos, excepto que su nombre es Default. Se agrega, modifica o elimina de la misma manera que cualquier otro origen de datos.
