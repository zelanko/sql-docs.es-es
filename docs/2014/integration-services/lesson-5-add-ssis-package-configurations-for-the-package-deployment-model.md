---
title: 'Lección 5: Agregar configuraciones de paquetes para el modelo de implementación de paquetes | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1c10dd54-67cb-4b63-9e4d-aa6ff0452ecb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 25922725e202bc7b38e2c6141a097df1af119ed2
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378840"
---
# <a name="lesson-5-adding-package-configurations-for-the-package-deployment-model"></a>Lección 5: Agregar configuraciones de paquetes para el modelo de implementación de paquetes
  Las configuraciones de paquetes permiten definir propiedades y variables de tiempo de ejecución desde el exterior del entorno de desarrollo. Las configuraciones permiten desarrollar paquetes que son flexibles y fáciles de implementar y distribuir. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ofrece los tipos de configuración siguientes:  
  
-   Archivo de configuración XML  
  
-   Variable de entorno  
  
-   Entrada del Registro  
  
-   Variable de paquete primario  
  
-   Tabla [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
 En esta lección, modificará el sencillo [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] paquete que creó en [lección 4: Agregar Error Flow Redirection](lesson-4-add-error-flow-redirection-with-ssis.md) para usar el modelo de implementación de paquetes y aprovechar las configuraciones de paquetes. También puede copiar el paquete de la lección 4 completada que se incluye con el tutorial. Mediante el Asistente para la configuración de paquetes, creará un archivo de configuración XML que actualiza la propiedad `Directory` del contenedor de bucles Foreach utilizando una variable de nivel de paquete asignada a la propiedad Directory. Una vez que haya creado el archivo de configuración, modificará el valor de la variable desde el exterior del entorno de desarrollo y hará que la propiedad haga referencia a una nueva carpeta de datos de ejemplo. Cuando ejecute el paquete de nuevo, el archivo de configuración rellenará el valor de la variable y la variable actualizará a su vez la `Directory` propiedad. Como consecuencia de ello, el paquete se iterará en los archivos de la nueva carpeta de datos, en lugar de iterarse en los archivos de la carpeta original del paquete codificada de forma rígida.  
  
> [!IMPORTANT]  
>  Para este tutorial, se necesita la base de datos de ejemplo **AdventureWorksDW2012** . Para obtener más información sobre cómo instalar e implementar **AdventureWorksDW2012**, consulte [Ejemplos de productos de Reporting Services en CodePlex](https://go.microsoft.com/fwlink/?LinkID=526910).  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 Esta lección contiene las siguientes tareas:  
  
-   [Paso 1: Copiar el paquete de la lección 4](lesson-5-1-copying-the-lesson-4-package.md)  
  
-   [Paso 2: Habilitar y configurar las configuraciones de paquetes](lesson-5-2-enabling-and-configuring-package-configurations.md)  
  
-   [Paso 3: Modificar el valor de configuración de propiedad de directorio](lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
-   [Paso 4: Probar el paquete del Tutorial lección 5](lesson-5-4-testing-the-lesson-5-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
  
-   [Paso 1: Copiar el paquete de la lección 4](lesson-5-1-copying-the-lesson-4-package.md)  
  
  
