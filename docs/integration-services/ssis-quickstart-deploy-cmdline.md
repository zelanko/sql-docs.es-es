---
title: "Implementar un proyecto de SSIS desde el símbolo del sistema | Documentos de Microsoft"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 0f1c7733f0ce6b132c209961a1fd12da80cbd282
ms.contentlocale: es-es
ms.lasthandoff: 10/06/2017

---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>Implementar un proyecto de SSIS desde el símbolo del sistema con ISDeploymentWizard.exe
Este tutorial de inicio rápido muestra cómo implementar un proyecto de SSIS desde el símbolo del sistema ejecutando el Asistente para la implementación de Integration Services, `ISDeploymentWizard.exe`.

Para obtener más información sobre el Asistente para la implementación de servicios de integración, vea [Integration Services Deployment Wizard](packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard).

## <a name="start-the-integration-services-deployment-wizard"></a>Iniciar al Asistente para la implementación de Integration Services
1. Abra una ventana de símbolo del sistema.

2. Ejecute `ISDeploymentWizard.exe`. Se abre el Asistente para la implementación de Integration Services.

    Si la carpeta que contiene `ISDeploymentWizard.exe` no está en su `path` variable de entorno, es podrán que deba utilizar la `cd` comando para cambiar a su directorio. En SQL Server 2017, esta carpeta es normalmente `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

## <a name="deploy-a-project-with-the-wizard"></a>Implementar un proyecto con el Asistente
1. En el **Introducción** página del asistente, revise la introducción. Haga clic en **siguiente** para abrir el **Seleccionar origen** página.

2. En el **Seleccionar origen** página, seleccione el proyecto SSIS existente para implementar.
    -   Para implementar un archivo de implementación de proyectos que haya creado, seleccione **Archivo de implementación de proyecto** y especifique la ruta de acceso del archivo .ispac.
    -   Para implementar un proyecto que resida en un catálogo de SSIS, seleccione **catálogo de Integration Services**y, a continuación, escriba el nombre del servidor y la ruta de acceso al proyecto en el catálogo.
    Haga clic en **Siguiente** para ver la página **Seleccionar destino** .
  
3.  En el **Seleccionar destino** página, seleccione el destino para el proyecto.
    -   Escriba el nombre completo del servidor. Si el servidor de destino es un servidor de base de datos de SQL Azure, el nombre está en este formato: `<server_name>.database.windows.net`.
    -   A continuación, haga clic en **examinar** para seleccionar la carpeta de destino de SSISDB.
    Haga clic en **siguiente** para abrir el **revisión** página.  
  
4.  En el **revisar** página, revise la configuración seleccionada.
    -   Puede cambiar las selecciones si hace clic en **Anterior**o si hace clic en cualquiera de los pasos del panel izquierdo.
    -   Haga clic en **Implementar** para iniciar el proceso de implementación.
  
5.  Una vez completado, el proceso de implementación del **resultados** se abre la página. Esta página muestra si cada acción si se completó correctamente o no.
    -   Si se produjo un error, haga clic en **error** en el **resultado** columna para que aparezca una explicación del error.
    -   Si lo desea, haga clic en **Guardar informe...**  para guardar los resultados en un archivo XML.
    -   Haga clic en **cerrar** para salir del asistente.

## <a name="next-steps"></a>Pasos siguientes
- Tenga en cuenta otras formas de implementar un paquete.
    - [Implementar un paquete SSIS con SSMS](./ssis-quickstart-deploy-ssms.md)
    - [Implementar un paquete SSIS con Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Implementar un paquete SSIS con Transact-SQL (frente a código)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Implementar un paquete SSIS con PowerShell](ssis-quickstart-deploy-powershell.md)
    - [Implementar un paquete SSIS con C#](./ssis-quickstart-deploy-dotnet.md) 
- Ejecutar un paquete implementado. Para ejecutar un paquete, puede elegir entre varias herramientas y lenguajes. Para obtener más información, vea los siguientes artículos:
    - [Ejecutar un paquete SSIS con SSMS](./ssis-quickstart-run-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (frente a código)](ssis-quickstart-run-tsql-vscode.md)
    - [Ejecutar un paquete SSIS desde la línea de comandos](./ssis-quickstart-run-cmdline.md)
    - [Ejecutar un paquete SSIS con PowerShell](ssis-quickstart-run-powershell.md)
    - [Ejecutar un paquete SSIS con C#](./ssis-quickstart-run-dotnet.md) 

