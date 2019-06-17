---
title: Importar un proyecto de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3301c328-b0f5-4517-915c-93713413e453
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ac28a67051299b0dbdfc7010d9abe20d0d2d2493
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058171"
---
# <a name="import-an-integration-services-project"></a>Importar un proyecto de Integration Services
  Use el **Asistente para importar proyectos** de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para crear un proyecto a partir de un archivo de implementación (.ispac) existente o de un proyecto implementado en el catálogo de Integration Services. Esta característica resulta especialmente útil si no tiene la copia original del proyecto, pero desea crear uno a partir de un archivo .ispac o un catálogo de SSISDB.  
  
### <a name="to-import-a-project"></a>Para importar un proyecto  
  
1.  En [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], haga clic en **Nuevo** > **Proyecto** en el menú **Archivo** .  
  
2.  En el área **Plantillas instaladas** de la ventana **Nuevo proyecto** , expanda **Business Intelligence**y haga clic en **Integration Services**.  
  
3.  Seleccione **Asistente para importar proyectos de Integration Services** de la lista de tipos de proyecto.  
  
4.  Escriba un nombre para el proyecto que va a crear en el cuadro de texto **Nombre** .  
  
5.  Escriba la ruta de acceso o la ubicación del proyecto en el cuadro de texto **Ubicación** o haga clic en **Examinar** para seleccionar uno.  
  
6.  Escriba un nombre para la solución en el cuadro de texto **Nombre de solución** .  
  
7.  Haga clic en **Aceptar** para iniciar el cuadro de diálogo **Asistente para importar proyectos de Integration Services** .  
  
8.  Haga clic en **Siguiente** para cambiar a la página **Seleccionar origen** .  
  
9. Si va a importar desde un archivo **.ispac** , escriba la ruta de acceso con el nombre de archivo incluido en el cuadro de texto **Ruta de acceso** . Haga clic en **Examinar** para navegar hasta la carpeta donde desea almacenar la solución, escriba el nombre del archivo en el cuadro de texto **Nombre de archivo** y haga clic en **Abrir**.  
  
     Si está efectuando una importación desde un **Catálogo de Integration Services**, escriba el nombre de la instancia de base de datos en el cuadro de texto **Nombre del servidor** o haga clic en **Examinar** y seleccione la instancia de base de datos que contiene el catálogo.  
  
     Haga clic en **Examinar** junto al cuadro de texto **Ruta de acceso** , expanda la carpeta del catálogo, seleccione el proyecto que desea importar y haga clic en **Aceptar**.  
  
     Haga clic en **Siguiente** para pasar a la página **Revisión** .  
  
10. Revise la información y haga clic en **Importar** para crear un proyecto basado en el proyecto existente que ha seleccionado.  
  
11. Opcional: haga clic en **Guardar informe** para guardar los resultados en un archivo  
  
12. Haga clic en **Cerrar** para cerrar el cuadro de diálogo **Asistente para importar proyectos de Integration Services** .  
  
  
