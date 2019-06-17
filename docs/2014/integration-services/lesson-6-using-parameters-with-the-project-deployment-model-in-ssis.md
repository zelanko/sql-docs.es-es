---
title: 'Lección 6: Usar parámetros con el modelo de implementación del proyecto | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d559defe1dd08f26077738cdd0aea219e8f7554b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62890550"
---
# <a name="lesson-6-using-parameters-with-the-project-deployment-model"></a>Lección 6: Uso de parámetros con el modelo de implementación de proyectos
  SQL Server 2012 presenta un nuevo modelo de implementación en el que puede implementar sus proyectos en el servidor de Integration Services. El servidor de Integration Services permite administrar y ejecutar paquetes, así como configurar valores en tiempo de ejecución para los paquetes.  
  
 En esta lección, modificará el paquete que creó en [lección 5: Agregar configuraciones de paquetes para el modelo de implementación de paquetes](lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md) para utilizar el modelo de implementación del proyecto. Reemplazará el valor de configuración con un parámetro para especificar la ubicación de los datos de ejemplo. También puede copiar el paquete de la lección 5 completada que se incluye con el tutorial.  
  
 Con el Asistente para la conversión de proyectos de Integration Services, convertirá el proyecto al modelo de implementación de proyectos y usará un parámetro en lugar de un valor de configuración para establecer la propiedad Directory. Esta lección abarca parcialmente los pasos que se seguiría para convertir paquetes SSIS existentes al nuevo modelo de implementación de proyectos.  
  
 Cuando ejecute el paquete de nuevo, el servicio Integration Services usará el parámetro para rellenar el valor de la variable y la variable actualizará a su vez la propiedad Directory. Como resultado, el paquete iterará por los archivos de la nueva carpeta de datos especificada por el valor del parámetro, en lugar de iterar por la carpeta que se estableció en el archivo de configuración del paquete.  
  
> [!IMPORTANT]  
>  Para este tutorial, se necesita la base de datos de ejemplo **AdventureWorksDW2012** . Para obtener más información sobre cómo instalar e implementar **AdventureWorksDW2012**, consulte [Considerations for Installing SQL Server Samples and Sample Databases](https://technet.microsoft.com/library/ms161556%28v=sql.105%29) (Consideraciones para instalar ejemplos y bases de datos de ejemplo de SQL Server).  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 Esta lección contiene las siguientes tareas:  
  
1.  [Paso 1: Copiar el paquete de la lección 5](lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [Paso 2: Convertir el proyecto al modelo de implementación de proyectos](lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [Paso 3: Probar el paquete de la lección 6](lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [Paso 4: Implementar el paquete de la lección 6](lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
 [Paso 1: Copiar el paquete de la lección 5](lesson-6-1-copying-the-lesson-5-package.md)  
  
  
