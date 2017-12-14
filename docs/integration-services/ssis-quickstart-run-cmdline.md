---
title: "Ejecutar un paquete SSIS desde el símbolo del sistema | Microsoft Docs"
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
ms.openlocfilehash: 2c2b83605714e01961c50d71e83ba57691bc3833
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>Ejecutar un paquete SSIS desde el símbolo del sistema con DTExec.exe
Este tutorial de inicio rápido muestra cómo ejecutar un paquete SSIS desde el símbolo del sistema mediante la ejecución de `DTExec.exe` con los parámetros adecuados.

> [!NOTE]
> El método descrito en este artículo no se ha probado con los paquetes que se implementan en un servidor de Azure SQL Database.

Para obtener más información sobre `DTExec.exe`, consulte [dtexec Utility](https://docs.microsoft.com/en-us/sql/integration-services/packages/dtexec-utility).

## <a name="run-a-package-with-dtexec"></a>Ejecutar un paquete con dtexec

Si la carpeta que contiene `DTExec.exe` no está en la variable de entorno `path`, es posible que deba usar el comando `cd` para cambiar al directorio de esta. En SQL Server 2017, esta carpeta está normalmente en `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

Con los valores de parámetro utilizados en el ejemplo siguiente, el programa ejecuta el paquete en la ruta de acceso de la carpeta especificada en el servidor SSIS; es decir, el servidor que hospeda la base de datos del catálogo de SSIS (SSISDB). El parámetro `/Server` proporciona el nombre del servidor. El programa se conecta como el usuario actual con la autenticación integrada de Windows. Para utilizar la autenticación de SQL, especifique los parámetros `/User` y `Password` con valores adecuados.

1. Abra una ventana de símbolo del sistema.

2. Ejecute `DTExec.exe` y proporcione valores al menos para los parámetros `ISServer` y `Server`, como se muestra en el ejemplo siguiente:

    ```cmd
    dtexec /ISServer "\SSISDB\Project1Folder\Integration Services Project1\Package.dtsx" /Server "localhost"
    ```

## <a name="next-steps"></a>Pasos siguientes
- Tenga en cuenta otras formas de ejecutar un paquete.
    - [Ejecutar un paquete SSIS con SSMS](./ssis-quickstart-run-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Ejecutar un paquete SSIS con PowerShell](ssis-quickstart-run-powershell.md)
    - [Ejecutar un paquete SSIS con C#](./ssis-quickstart-run-dotnet.md) 
