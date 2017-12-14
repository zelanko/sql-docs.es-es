---
title: "Implementar un proyecto de SSIS desde el símbolo del sistema | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6c3e7f7e3fa870c7aa5b30a5a4a324f0cef7f6ba
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>Implementar un proyecto de SSIS desde el símbolo del sistema con ISDeploymentWizard.exe
En este tutorial de inicio rápido se muestra cómo implementar un proyecto de SSIS desde el símbolo del sistema mediante la ejecución del asistente para la implementación de Integration Services, `ISDeploymentWizard.exe`.

Para obtener más información sobre el asistente para la implementación de Integration Services, consulte [Integration Services Deployment Wizard (Asistente para la implementación de Integration Services)](packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard).

## <a name="start-the-integration-services-deployment-wizard"></a>Iniciar el asistente para la implementación de Integration Services
1. Abra una ventana de símbolo del sistema.

2. Ejecute `ISDeploymentWizard.exe`. Se abre entonces el asistente para la implementación de Integration Services.

    Si la carpeta que contiene `ISDeploymentWizard.exe` no está en la variable de entorno `path`, es posible que deba usar el comando `cd` para cambiar al directorio de la misma. En SQL Server 2017, esta carpeta está normalmente en `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

## <a name="deploy-a-project-with-the-wizard"></a>Implementar un proyecto con el asistente
1. En la página **Introducción** del asistente, lea la introducción. Haga clic en **Siguiente** para abrir la página **Seleccionar origen**.

2. En la página **Seleccionar origen**, seleccione el proyecto SSIS existente que hay que implementar.
    -   Para implementar un archivo de implementación de proyectos que haya creado, seleccione **Archivo de implementación de proyecto** y especifique la ruta de acceso del archivo .ispac.
    -   Para implementar un proyecto que resida en un catálogo de SSIS, seleccione **Catálogo de Integration Services** y especifique el nombre del servidor y la ruta de acceso al proyecto en el catálogo.
    Haga clic en **Siguiente** para ver la página **Seleccionar destino** .
  
3.  En la página **Seleccionar destino**, seleccione el destino del proyecto.
    -   Escriba el nombre completo del servidor. Si el servidor de destino es un servidor de Azure SQL Database, el nombre tendrá este formato: `<server_name>.database.windows.net`.
    -   A continuación, haga clic en **Examinar** para seleccionar la carpeta de destino en SSISDB.
    Haga clic en **Siguiente** para abrir la página **Revisión**.  
  
4.  En la página **Revisión**, revise la configuración seleccionada.
    -   Puede cambiar las selecciones si hace clic en **Anterior**o si hace clic en cualquiera de los pasos del panel izquierdo.
    -   Haga clic en **Implementar** para iniciar el proceso de implementación.
  
5.  Una vez completado el proceso de implementación, se abrirá la página **Resultados**. Esta página muestra si cada acción si se completó correctamente o no.
    -   Si se produce un error en la acción, haga clic en **Error** en la columna **Resultado** para que aparezca una explicación del error.
    -   De forma opcional, puede hacer clic en **Guardar informe...** para guardar los resultados en un archivo XML.
    -   Haga clic en **Cerrar** para salir del asistente.

## <a name="next-steps"></a>Pasos siguientes
- Tenga en cuenta otras formas de implementar un paquete.
    - [Deploy an SSIS package with SSMS (Implementar un paquete SSIS con SSMS)](./ssis-quickstart-deploy-ssms.md)
    - [Deploy an SSIS package with Transact-SQL (SSMS) (Implementar un paquete SSIS con Transact-SQL [SSMS])](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Deploy an SSIS package with Transact-SQL (VS Code) (Implementar un paquete SSIS con Transact-SQL [VS Code])](ssis-quickstart-deploy-tsql-vscode.md)
    - [Deploy an SSIS package with PowerShell (Implementar un paquete SSIS con PowerShell)](ssis-quickstart-deploy-powershell.md)
    - [Deploy an SSIS package with C# (Implementar un paquete SSIS con C#)](./ssis-quickstart-deploy-dotnet.md) 
- Ejecute un paquete implementado. Para ejecutar un paquete, puede elegir entre varias herramientas y lenguajes. Para obtener más información, vea los artículos siguientes:
    - [Run an SSIS package with SSMS (Ejecutar un paquete SSIS con SSMS)](./ssis-quickstart-run-ssms.md)
    - [Run an SSIS package with Transact-SQL (SSMS) (Ejecutar un paquete SSIS con Transact-SQL [SSMS])](./ssis-quickstart-run-tsql-ssms.md)
    - [Run an SSIS package with Transact-SQL (VS Code) (Ejecutar un paquete SSIS con Transact-SQL [VS Code])](ssis-quickstart-run-tsql-vscode.md)
    - [Run an SSIS package from the command prompt (Ejecutar un paquete SSIS desde el símbolo del sistema)](./ssis-quickstart-run-cmdline.md)
    - [Run an SSIS package with PowerShell (Ejecutar un paquete SSIS con PowerShell)](ssis-quickstart-run-powershell.md)
    - [Run an SSIS package with C# (Ejecutar un paquete SSIS con C#)](./ssis-quickstart-run-dotnet.md) 
