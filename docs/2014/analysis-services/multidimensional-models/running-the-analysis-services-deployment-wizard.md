---
title: Ejecutar el Asistente para la implementación de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services Deployment Wizard, running
ms.assetid: 3a38d489-4625-4878-bd18-c6f903be33df
author: minewiskan
ms.author: owend
ms.openlocfilehash: 03e142f00192e04d5b17bc2041563cea06199c8b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545727"
---
# <a name="running-the-analysis-services-deployment-wizard"></a>Ejecutar el Asistente para la implementación de Analysis Services
  Al utilizar el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente para la implementación de para implementar un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto de, puede ejecutar el Asistente de las siguientes maneras:  
  
-   **Interactivamente** Cuando se ejecuta interactivamente, el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera un script XML basado en los archivos de entrada tal y como han sido modificados interactivamente mediante la entrada del usuario. El asistente solo aplica las modificaciones del usuario al script de implementación. El asistente no modifica los archivos de entrada. Para obtener más información acerca de los archivos de entrada, vea [Understanding the Input Files Used to Create the Deployment Script](deployment-script-files-input-used-to-create-deployment-script.md).  
  
-   **Desde el símbolo del sistema** Cuando se ejecuta en el símbolo del sistema, el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente para la implementación genera un script de implementación de XML for Analysis (XMLA) basado en los modificadores que se usan para ejecutar el asistente. El asistente puede realizar cualquier de las siguientes tareas: solicitar la entrada de usuario y, en función de esa entrada, modificar los archivos de entrada, ejecutar una implementación desatendida en modo silencioso utilizando los archivos de entrada sin cambios o crear un script de implementación para utilizarlo posteriormente.  
  
## <a name="running-the-analysis-services-deployment-wizard-interactively"></a>Ejecutar interactivamente el Asistente para la implementación de Analysis Services  
 Cuando se ejecuta interactivamente, el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lee los valores de los archivos de entrada y le muestra dicha información. Puede modificar estos valores de entrada, como el destino de la implementación, la configuración, las opciones de implementación y las contraseñas de las cadenas de conexión, o bien dejarlas tal cual. Si cambia alguno de los valores de entrada, el asistente utiliza estos cambios cuando genera el script de implementación XMLA. Sin embargo, el asistente no realiza ningún cambio en los valores del archivo de entrada.  
  
> [!NOTE]  
>  Si desea que el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] modifique los valores de entrada, ejecute el asistente en el símbolo del sistema y configúrelo para que se ejecute en modo de archivo de respuesta.  
  
 Después de revisar los valores de entrada y efectuar los cambios oportunos, el asistente genera un script de implementación XMLA. Este script de implementación puede ejecutarse de inmediato en el servidor de destino o guardarse para utilizarlo en otra ocasión.  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-interactively"></a>Para ejecutar interactivamente el Asistente para la implementación de Analysis Services  
  
-   En el menú **Inicio**, elija **Todos los programas**, **Microsoft SQL Server**, **Analysis Services**y, a continuación, haga clic en **Asistente para la implementación**.  
  
     o bien  
  
-   En la carpeta **proyectos** del [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto, haga doble clic en el *\<project name>* archivo. asdatabase.  
  
    > [!NOTE]  
    >  Si no puede encontrar el *\<project name>* archivo. asdatabase, pruebe a usar buscar y especifique *. asdatabase.  
  
## <a name="running-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>Ejecutar el Asistente para la implementación de Analysis Services desde el símbolo del sistema  
 El Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también puede ejecutarse desde el símbolo del sistema. Cuando se ejecuta desde el símbolo del sistema, se especifica la ruta completa al archivo .asdatabase y se ejecuta en alguno de los siguientes modos:  
  
 **Modo de archivo de respuesta**  
 En este modo, el asistente le permite modificar interactivamente los archivos de entrada creados originariamente cuando el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fue creado en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. El asistente guarda estos archivos de entrada modificados antes de generar el script de implementación XMLA. Los archivos de entrada modificados se convierten en el nuevo punto de partida la próxima vez que se ejecuta el asistente.  
  
 Para ejecutar el asistente en modo de archivo de respuesta, use el modificador **/a** .  
  
 **Modo silencioso**  
 En este modo, el asistente ejecuta una implementación silenciosa desatendida basada en la información que reside en los archivos de entrada.  
  
 Para ejecutar el asistente en modo silencioso, utilice el modificador **/s** . Al ejecutar el asistente en modo silencioso, los mensajes se muestran en la consola o en un archivo de registro si se proporciona uno.  
  
 **Modo de salida**  
 En este modo, el asistente genera un script de implementación XMLA basado en los archivos de entrada para su ejecución posterior.  
  
 Para ejecutar el asistente en modo de salida, use el modificador **/o** y proporcione un nombre de archivo de salida.  
  
 Para obtener más información acerca de estos modificadores de línea de comandos, consulte [Implementar soluciones de modelos con la utilidad de implementación](deploy-model-solutions-with-the-deployment-utility.md).  
  
 El siguiente procedimiento describe cómo ejecutar el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] desde el símbolo del sistema.  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>Para ejecutar el Asistente para la implementación de Analysis Services desde el símbolo del sistema  
  
1.  Abra el símbolo del sistema y navegue a la carpeta C:\Archivos de programa\Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE.  
  
2.  Escriba **Microsoft.AnalysisServices.Deployment.exe** seguido de los modificadores correspondientes al modo en que desee ejecutar el asistente.  
  
## <a name="see-also"></a>Consulte también  
 [Descripción del script de implementación de Analysis Services](understanding-the-analysis-services-deployment-script.md)   
 [Implementar soluciones con el Asistente para la implementación](deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
