---
title: Ejecutar un paquete SSIS desde el símbolo del sistema | Microsoft Docs
ms.date: 09/25/2017
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: quick-start
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0dec4f11b797cc138f11f20a521e1c304efa0463
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>Ejecutar un paquete SSIS desde el símbolo del sistema con DTExec.exe
Este tutorial de inicio rápido muestra cómo ejecutar un paquete SSIS desde el símbolo del sistema mediante la ejecución de `DTExec.exe` con los parámetros adecuados.

> [!NOTE]
> El método descrito en este artículo no se ha probado con los paquetes que se implementan en un servidor de Azure SQL Database.

Para obtener más información sobre `DTExec.exe`, consulte [dtexec Utility](https://docs.microsoft.com/sql/integration-services/packages/dtexec-utility).

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
    - [Run an SSIS package with Transact-SQL (SSMS) (Ejecutar un paquete SSIS con Transact-SQL [SSMS])](./ssis-quickstart-run-tsql-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (VS Code)](ssis-quickstart-run-tsql-vscode.md)
    - [Run an SSIS package with PowerShell](ssis-quickstart-run-powershell.md) (Ejecutar un paquete de SSIS con PowerShell)
    - [Ejecutar un paquete SSIS con C#](./ssis-quickstart-run-dotnet.md) 
