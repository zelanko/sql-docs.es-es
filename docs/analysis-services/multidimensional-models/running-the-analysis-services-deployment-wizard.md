---
title: Ejecutar el análisis de Asistente para la implementación de servicios | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f7362e216213bc27efab0fd49f3ded2f15c37bdb
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="running-the-analysis-services-deployment-wizard"></a>Ejecutar el Asistente para la implementación de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  El [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente para la implementación se puede ejecutar lo siguiente:  
  
-   **Interactivamente** cuando se ejecuta interactivamente, el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente de implementación genera un script de implementación basado en los archivos de entrada, tal y como han sido modificados interactivamente mediante la entrada del usuario. El asistente solo aplica las modificaciones del usuario al script de implementación. El asistente no modifica los archivos de entrada. Para obtener más información acerca de los archivos de entrada, vea [Understanding the Input Files Used to Create the Deployment Script](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md).  
  
-   **Desde el símbolo del sistema** cuando se ejecuta en el símbolo del sistema, la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente de implementación genera un script de implementación basado en los modificadores que utilizan para ejecutar el asistente. El asistente puede realizar cualquier de las siguientes tareas: solicitar la entrada de usuario y, en función de esa entrada, modificar los archivos de entrada, ejecutar una implementación desatendida en modo silencioso utilizando los archivos de entrada sin cambios o crear un script de implementación para utilizarlo posteriormente.  
  
## <a name="running-the-analysis-services-deployment-wizard-interactively"></a>Ejecutar interactivamente el Asistente para la implementación de Analysis Services  
 Cuando se ejecuta interactivamente, el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lee los valores de los archivos de entrada y le muestra dicha información. Puede modificar estos valores de entrada, como el destino de la implementación, la configuración, las opciones de implementación y las contraseñas de la cadena de conexión, o bien no cambiar nada. Si cambia los valores de entrada, el asistente utiliza estos cambios al generar el script de implementación. Sin embargo, el asistente no realiza ningún cambio en los valores del archivo de entrada.  
  
> [!NOTE]  
>  Si desea que el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] modifique los valores de entrada, ejecute el asistente en el símbolo del sistema y configúrelo para que se ejecute en modo de archivo de respuesta.  
  
 Después de revisar los valores de entrada y efectuar los cambios oportunos, el asistente genera el script de implementación. Este script de implementación puede ejecutarse de inmediato en el servidor de destino o guardarse para utilizarlo en otra ocasión.  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-interactively"></a>Para ejecutar interactivamente el Asistente para la implementación de Analysis Services  
  
-   Haga clic en **iniciar** > **de Microsoft SQL Server** > **Asistente para la implementación**.  
  
     O bien  
  
-   En el **proyectos** carpeta de la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto de equipo y haga doble clic en el \<nombre del proyecto >. asdatabase.
    > [!NOTE]  
    >  Si no consigue encontrar el archivo.asdatabase, pruebe a utilizar Buscar especificando *.asdatabase. O bien, puede que necesite crear el proyecto de SSDT.  
  
## <a name="running-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>Ejecutar el Asistente para la implementación de Analysis Services desde el símbolo del sistema  
 El Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también puede ejecutarse desde el símbolo del sistema. Cuando se ejecuta desde el símbolo del sistema, se especifica la ruta completa al archivo .asdatabase y se ejecuta en alguno de los siguientes modos:  
  
 **Modo de archivo de respuesta**  
 En este modo, el asistente le permite modificar interactivamente los archivos de entrada creados originariamente cuando el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fue creado en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. El asistente guarda estos archivos de entrada modificados antes de generar el script de implementación. Los archivos de entrada modificados se convierten en el nuevo punto de partida la próxima vez que se ejecuta el asistente.  
  
 Para ejecutar el Asistente en modo de archivo de respuesta, use la **/a** cambiar.  
  
 **Modo silencioso**  
 En este modo, el asistente ejecuta una implementación silenciosa desatendida basada en la información que reside en los archivos de entrada.  
  
 Para ejecutar el Asistente en modo silencioso, utilice la **/s** cambiar. Al ejecutar el asistente en modo silencioso, los mensajes se muestran en la consola o en un archivo de registro si se proporciona uno.  
  
 **Modo de salida**  
 En este modo, el asistente genera un script de implementación para ejecutarlas posteriormente en función de los archivos de entrada.  
  
 Para ejecutar el Asistente en modo de salida, utilice la **/o** cambiar y especifique un nombre de archivo de salida.  
  
 Para obtener más información acerca de estos modificadores de línea de comandos, consulte [Implementar soluciones de modelos con la utilidad de implementación](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md).  
  
 El siguiente procedimiento describe cómo ejecutar el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] desde el símbolo del sistema.  
  
#### <a name="to-run-the-analysis-services-deployment-wizard-at-the-command-prompt"></a>Para ejecutar el Asistente para la implementación de Analysis Services desde el símbolo del sistema  
  
1.  Abra un símbolo del sistema y desplácese a la \Microsoft SQL Server\140\Tools\Binn\ManagementStudio C:\Program Files (x86)  
  
2.  Escriba **Microsoft.AnalysisServices.Deployment.exe** seguido de los modificadores correspondientes al modo en que desee ejecutar el asistente.  
  
## <a name="see-also"></a>Vea también  
 [Descripción del script de implementación de Analysis Services](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)   
 [Implementar soluciones con el Asistente para implementación](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
  
