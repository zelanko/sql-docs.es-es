---
title: 'Lección 5: Agregar configuraciones de paquete de SSIS para el modelo de implementación de paquetes | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d3b3ccea56d367e7870826b39830e415e26bb2ac
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295908"
---
# <a name="lesson-5-add-ssis-package-configurations-for-the-package-deployment-model"></a>Lección 5: Agregar configuraciones de paquete de SSIS para el modelo de implementación de paquetes

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Las configuraciones de paquetes permiten definir propiedades y variables de tiempo de ejecución desde el exterior del entorno de desarrollo. Las configuraciones permiten desarrollar paquetes que son flexibles y fáciles de implementar y distribuir. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ofrece los tipos de configuración siguientes:  
  
-   Archivo de configuración XML  
  
-   Variable de entorno  
  
-   Entrada del Registro  
  
-   Variable de paquete primario  
  
-   Tabla [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
En esta lección se modifica el paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] de ejemplo creado en [Lección 4: Agregar redireccionamiento de flujo de errores con SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md) para usar el modelo de implementación de paquetes y aprovechar las configuraciones de paquetes. También puede copiar el paquete de la lección 4 completado incluido con este tutorial. 

Con el Asistente para configuración de paquetes, se crea una configuración XML que actualiza la propiedad **Directory** del contenedor de bucles Foreach. Se usa una variable de nivel de paquete asignada a la propiedad **Directory**. Después de crear el archivo de configuración, se modifica el valor de la variable desde el exterior del entorno de desarrollo con una nueva ruta de acceso de carpeta de datos de ejemplo. Cuando ejecute el paquete de nuevo, el archivo de configuración rellenará el valor de la variable y la variable actualizará a su vez la propiedad **Directory** . Luego, el paquete se itera a través de los archivos de la nueva carpeta de datos, en lugar de hacerlo en la carpeta original codificada de forma rígida.  
  
> [!NOTE]
> Si todavía no lo ha hecho, consulte los [requisitos previos de la lección 1](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).
  
## <a name="lesson-tasks"></a>Tareas de la lección  
Esta lección contiene las siguientes tareas:  
  
-   [Paso 1: Copiar el paquete de la lección 4](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [Paso 2: Habilitar y configurar configuraciones de paquetes](../integration-services/lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [Paso 3: Modificar el valor de configuración de la propiedad Directory](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [Paso 4: Probar el paquete de la lección 5](../integration-services/lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
  
-   [Paso 1: Copiar el paquete de la lección 4](../integration-services/lesson-5-1-copying-the-lesson-4-package.md)  
  
  
  
