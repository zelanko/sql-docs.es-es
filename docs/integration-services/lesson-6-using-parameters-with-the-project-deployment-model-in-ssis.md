---
title: 'Lección 6: Uso de parámetros con el modelo de implementación de proyectos | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: chugugrace
ms.author: chugu
ms.openlocfilehash: afc1e7ceb6dca21bd562745fe7250500cc9c2033
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "77903879"
---
# <a name="lesson-6-use-parameters-with-the-project-deployment-model-in-ssis"></a>Lección 6: Uso de parámetros con el modelo de implementación de proyectos en SSIS

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



SQL Server 2012 ha incorporado un nuevo modelo de implementación que permite implementar los proyectos en el servidor de Integration Services. El servidor de Integration Services permite administrar y ejecutar paquetes, así como configurar valores en tiempo de ejecución para los paquetes.  
  
En esta lección se modifica el paquete creado en [Lección 5: Agregar configuraciones de paquete de SSIS para el modelo de implementación de paquetes](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md) para usar el modelo de implementación de paquetes. Reemplazará el valor de configuración con un parámetro para especificar la ubicación de los datos de ejemplo. También puede copiar el paquete de la lección 5 completada que se incluye con el tutorial.  
  
Con el Asistente para configuración de proyectos de Integration Services se convierte el proyecto al modelo de implementación de proyectos. Este modelo usa un parámetro en lugar de un valor de configuración para establecer la propiedad Directory. Esta lección abarca parcialmente los pasos que se seguiría para convertir paquetes SSIS existentes al nuevo modelo de implementación de proyectos.  
  
Al ejecutar el paquete de nuevo, el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa el parámetro para rellenar el valor de la variable. La variable a su vez actualiza la propiedad Directory. El paquete se itera a través de los archivos de la carpeta de datos especificada por el nuevo parámetro.  
  
> [!NOTE]
> Si todavía no lo ha hecho, consulte los [requisitos previos de la lección 1](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).
    
## <a name="lesson-tasks"></a>Tareas de la lección  
Esta lección contiene las siguientes tareas:  
  
1.  [Paso 1: Copiar el paquete de la lección 5](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [Paso 2: Convertir el proyecto al modelo de implementación de proyectos](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [Paso 3: Probar el paquete de la lección 6](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [Paso 4: Implementar el paquete de la lección 6](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
[Paso 1: Copiar el paquete de la lección 5](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
