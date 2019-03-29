---
title: 'Paso 1: Generar la utilidad de implementación | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1ff4dcff-89b3-4b99-a725-5f7963e98abf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6655e4fcf33b66e4bef4025f69c91ec3c13bc79e
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58280899"
---
# <a name="lesson-2-1---building-the-deployment-utility"></a>Lección 2-1: Generar la utilidad de implementación
En esta tarea, configurará y generará una utilidad de implementación para el proyecto Deployment Tutorial.  
  
Antes de generar la utilidad de implementación, debe modificar las propiedades del proyecto Deployment Tutorial. Usará el cuadro de diálogo **Deployment Tutorial Property Pages** (Páginas de propiedades de Deployment Tutorial) para configurar estas propiedades. En este cuadro de diálogo, debe habilitar la capacidad de actualizar configuraciones durante la implementación y especificar que el proceso de creación crea una utilidad de implementación. Después de establecer las propiedades, generará el proyecto.  
  
[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] proporciona un conjunto de ventanas que puede usar para depurar paquetes. Puede ver mensajes de errores, advertencias e información, realizar el seguimiento del estado de paquetes en tiempo de ejecución o ver el progreso y los resultados de los procesos de generación. En esta lección, usará la ventana de resultados para ver el progreso y el resultado de la generación de la utilidad de implementación.  
  
### <a name="to-set-the-deployment-utility-properties"></a>Para establecer las propiedades de la utilidad de implementación  
  
1.  Si [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] no está abierto todavía, haga clic en **Inicio**, seleccione **Todos los programas**, **Microsoft SQL Server**y, después, haga clic en **Business Intelligence Development Studio**.  
  
2.  En el menú **Archivo** , haga clic en **Abrir**y, en **Proyecto o solución**, haga clic en la carpeta **Deployment Tutorial** a continuación, haga clic en **Abrir**y, después, haga doble clic en **Deployment Tutorial.sln**.  
  
3.  En el Explorador de soluciones, haga clic con el botón derecho en Deployment Tutorial y haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **Deployment Tutorial Property Pages** (Páginas de propiedades de Deployment Tutorial), expanda Propiedades de configuración y haga clic en Utilidad de implementación.  
  
5.  En el panel derecho del cuadro de diálogo **Deployment Tutorial Property Pages** (Páginas de propiedades de Deployment Tutorial), compruebe que **AllowConfigurationChanges** se establece en **True**, establezca **CreateDeploymentUtility** en **True**y, de manera opcional, actualice el valor predeterminado de **DeploymentOutputPath**.  
  
6.  Haga clic en **Aceptar**.  
  
### <a name="to-build-the-deployment-utility"></a>Para generar las propiedades de la utilidad de implementación  
  
1.  En el Explorador de soluciones, haga clic en **Deployment Tutorial**.  
  
2.  En el menú **Ver** , haga clic en **Salida**. De forma predeterminada, la ventana de resultados se encuentra en la esquina inferior izquierda de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
3.  En el menú **Generar** , haga clic en **Build Deployment Tutorial**(Generar Deployment Tutorial).  
  
4.  En la ventana de resultados, compruebe la siguiente información:  
  
    Compilación iniciada: Proyecto de SQL Integration Services: Incremental ...  
  
    Creando la utilidad de implementación...  
  
    Utilidad de implementación creada.  
  
    Generación completa -- 0 errores, 0 advertencias  
  
    ========== Build: 0 correcto, 0 errores, 1 actualizados, 0 omitidos ==========  
  
5.  En el menú **Archivo** , haga clic en **Salir**. Si se le pregunta si quiere guardar los cambios en los elementos de Deployment Tutorial, haga clic en **Sí**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Paso 2: Comprobación del paquete de implementación](../integration-services/lesson-2-2-verifying-the-deployment-bundle.md)  
  
## <a name="see-also"></a>Consulte también  
[Crear una utilidad de implementación](../integration-services/packages/create-a-deployment-utility.md)  
  
  
  
