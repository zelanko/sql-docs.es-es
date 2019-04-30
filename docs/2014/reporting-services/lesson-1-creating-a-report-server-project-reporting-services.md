---
title: 'Lección 1: Crear un proyecto de servidor de informes (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 675671ca-e6c9-48a2-82e9-386778f3a49f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 52050b9513de2638cacc394309f7e87d6ba77709
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63143284"
---
# <a name="lesson-1-creating-a-report-server-project-reporting-services"></a>Lección 1: Crear un proyecto de servidor de informes (Reporting Services)
  Para crear un informe en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], primero debe crear un proyecto de servidor de informes donde guardará el archivo de definición de informe (.rdl) y cualquier otro archivo de recursos que necesite para el informe. Luego creará el archivo de definición de informe real, definirá un origen de datos para el informe, definirá un conjunto de datos y establecerá el diseño del informe. Cuando ejecuta el informe, los datos reales se recuperan y combinan con el diseño y luego se representan en pantalla, desde donde se pueden exportar, imprimir o guardar.  
  
 En esta lección aprenderá a crear un proyecto de servidor de informes en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Los proyectos de servidor de informes sirven para crear informes que se ejecutan en servidores de informes.  
  
### <a name="to-create-a-report-server-project"></a>Para crear un proyecto de servidor de informes  
  
1.  Haga clic en **iniciar**, apunte a **todos los programas**, apunte a [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]y, a continuación, haga clic en **SQL Server Data Tools**. Si esta es la primera vez haya abierto [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en **configuración de Business Intelligence** para la configuración del entorno predeterminado.  
  
2.  En el menú **Archivo** , seleccione **Nuevo**y haga clic en **Proyecto**.  
  
3.  En la lista **Plantillas instaladas** , haga clic en **Business Intelligence**.  
  
4.  Haga clic en **Report Server Project**.  
  
5.  En **Nombre**, escriba **tutorial**.  
  
6.  Haga clic en **Aceptar** para crear el proyecto.  
  
     El proyecto Tutorial se muestra en el Explorador de soluciones.  
  
### <a name="to-create-a-new-report-definition-file"></a>Para crear un nuevo archivo de definición de informe  
  
1.  En el Explorador de soluciones, haga clic en **informes**, apunte a **agregar**y haga clic en **nuevo elemento**.  
  
    > [!NOTE]  
    >  Si la ventana **Explorador de soluciones** no está visible, en el menú **Ver** , haga clic en **Explorador de soluciones**.  
  
2.  En el **Agregar nuevo elemento** cuadro de diálogo **plantillas**, haga clic en **informe**.  
  
3.  En **Nombre**, escriba **Sales Orders.rdl** y, después, haga clic en **Agregar**.  
  
     Se abrirá el Diseñador de informes y se mostrará el nuevo archivo .rdl en la vista Diseño.  
  
 El Diseñador de informes es un componente de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que se ejecuta en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Tiene dos vistas: **Diseño** y **Vista previa**. Haga clic en cada pestaña para cambiar las vistas.  
  
 Los datos se definen en el panel **Datos de informe** . El diseño del informe se define en la vista **Diseño** . Puede ejecutar el informe y ver su aspecto en la vista **Vista previa** .  
  
## <a name="next-task"></a>Tarea siguiente  
 Ha creado un proyecto de informe denominado "Tutorial" y ha agregado un archivo de definición de informe (.rdl) al proyecto del informe correctamente. A continuación, debe especificar un origen de datos para utilizarlo con el informe. Consulte [Lección 2: Especificación de información de conexión &#40;Reporting Services&#41;](lesson-2-specifying-connection-information-reporting-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
