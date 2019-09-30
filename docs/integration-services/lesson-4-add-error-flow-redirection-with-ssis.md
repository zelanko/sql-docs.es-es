---
title: 'Lección 4: Adición de redireccionamiento de flujo de errores con SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c0117f867363a9536887ff1b67e1960170317d8d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295936"
---
# <a name="lesson-4-add-error-flow-redirection-with-ssis"></a>Lección 4: Adición de redireccionamiento de flujo de errores con SSIS

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Para controlar los errores que puedan aparecer en el proceso de transformación, [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] permite decidir en función de cada componente y cada columna cómo administrar los datos que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no puede transformar. Puede optar por omitir un error en determinadas columnas, redireccionar toda la fila que ha generado el error o rechazar el componente debido a un error. De forma predeterminada, los componentes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] están configurados para ser rechazados si se produce un error. Por su parte, el componente rechazado por un error hace que el paquete también genere un error y que se detenga el procesamiento.  
  
En lugar de dejar que los errores detengan la ejecución de los paquetes, se pueden configurar y controlar los posibles errores de procesamiento cuando se produzcan. Una opción consiste en omitir los errores por completo para que el paquete siempre se ejecute correctamente. También se puede redirigir la fila con error a otra ruta de procesamiento, donde los datos y el error se pueden conservar, examinar o volver a procesar.  
  
En esta lección, creará una copia del paquete que ha desarrollado en [Lección 3: Adición de registro con SSIS](../integration-services/lesson-3-add-logging-with-ssis.md). Con este paquete nuevo, se crea una versión dañada de uno de los archivos de datos de ejemplo. El archivo dañado fuerza la aparición de un error de procesamiento al ejecutar el paquete.  
  
Para controlar los datos de error, se agrega y configura un destino de archivo plano que escribe las filas con errores en un archivo de error. 
  
Antes de que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] escriba los datos de error en el archivo, se incluye un componente de Script que obtiene las descripciones de error. Después, se vuelve a configurar la transformación Lookup Currency Key para redireccionar los datos que no se hayan podido procesar en la transformación Script.  
  
## <a name="prerequisites"></a>Prerequisites

> [!NOTE]
> Si todavía no lo ha hecho, vea los [requisitos previos de la lección 1](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).
 
## <a name="lesson-task"></a>Tarea de la lección
Esta lección contiene las siguientes tareas:  
  
-   [Paso 1: Copia del paquete de la lección 3](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [Paso 2: Creación de un archivo dañado](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
-   [Paso 3: Adición de redireccionamiento de flujo de errores](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
-   [Paso 4: Adición de un destino de archivo plano](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [Paso 5: Prueba del paquete del tutorial de la lección 4](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
[Paso 1: Copia del paquete de la lección 3](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
  
  
