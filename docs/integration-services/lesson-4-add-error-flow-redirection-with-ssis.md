---
title: "Lección 4: Agregar redirección de flujo de errores con SSIS | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 48ed42543041f88519f106d8d9e3dcf50392799b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="lesson-4-add-error-flow-redirection-with-ssis"></a>Lección 4: Agregar redirección de flujo de errores con SSIS
Para administrar los errores que puedan aparecer en el proceso de transformación, [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ofrece la posibilidad de decidir para cada componente y cada columna cómo administrar los datos que no pueden transformarse. Puede optar por omitir un error en determinadas columnas, redireccionar toda la fila que ha generado el error o simplemente rechazar el componente debido a un error. De forma predeterminada, todos los componentes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] están configurados para ser rechazados si se produce un error. Rechazar el componente debido a un error, causa, a su vez, que el paquete también genere un error y que todos los procesos subsiguientes se detengan.  
  
En lugar de dejar que los errores detengan la ejecución de los paquetes, es recomendable configurar y administrar los posibles errores de procesamiento como si se produjeran en la transformación. Si bien puede optar por omitir los errores a fin de garantizar que el paquete se ejecute correctamente, generalmente es mejor redireccionar la fila que genera el error a otra ruta de proceso en la que los datos y el error puedan persistir, puedan examinarse y puedan procesarse de nuevo más adelante.  
  
En esta lección, creará una copia del paquete que ha desarrollado en la [Lección 3: Agregar registro con SSIS](../integration-services/lesson-3-add-logging-with-ssis.md). Trabajando con este paquete nuevo, creará una versión dañada de los archivos de datos de ejemplo. El archivo dañado forzará la aparición de un error de proceso al ejecutar el paquete.  
  
Para administrar los datos del error, agregará y configurará un destino de archivo plano que escribirá en un archivo las filas que no puedan encontrar un valor de búsqueda en la transformación Lookup Currency Key.  
  
Antes de escribir los datos del error en el archivo, incluirá un componente de script que utiliza un script para obtener descripciones de error. A continuación, volverá a configurar la transformación Lookup Currency Key para redireccionar los datos que no hayan podido procesarse en la transformación Script.  
  
> [!IMPORTANT]  
> Para este tutorial, se necesita la base de datos de ejemplo **AdventureWorksDW2012** . Para obtener más información sobre cómo instalar e implementar **AdventureWorksDW2012**, [ejemplos de producto de Reporting Services en CodePlex](http://go.microsoft.com/fwlink/p/?LinkID=526910).  
  
## <a name="tasks-in-lesson"></a>Tareas de la lección  
Esta lección contiene las siguientes tareas:  
  
-   [Paso 1: copiar el paquete de la lección 3](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [Paso 2: Crear un archivo dañado](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
-   [Paso 3: Agregar redirección de flujo de errores](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
-   [Paso 4: Agregar un destino de archivo plano](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [Paso 5: Probar el paquete del tutorial de la lección 4](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
[Paso 1: copiar el paquete de la lección 3](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
  
  
