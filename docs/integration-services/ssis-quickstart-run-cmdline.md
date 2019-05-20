---
title: Ejecutar un paquete SSIS desde el símbolo del sistema | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d1a3a27bfce0a62aa70d047e221f54ccc33c0c6b
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65717549"
---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>Ejecutar un paquete SSIS desde el símbolo del sistema con DTExec.exe

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


En este inicio rápido se muestra cómo ejecutar un paquete SSIS desde el símbolo del sistema mediante la ejecución de `DTExec.exe` con los parámetros adecuados.

> [!NOTE]
> El método descrito en este artículo no se ha probado con los paquetes que se implementan en un servidor de Azure SQL Database.

Para obtener más información sobre `DTExec.exe`, consulte [dtexec Utility](https://docs.microsoft.com/sql/integration-services/packages/dtexec-utility).

## <a name="supported-platforms"></a>Plataformas compatibles

Puede usar la información que aparece en este inicio rápido para ejecutar un paquete de SSIS en las siguientes plataformas:

-   SQL Server en Windows.

El método descrito en este artículo no se ha probado con los paquetes que se implementan en un servidor de Azure SQL Database. Para más información sobre cómo implementar y ejecutar paquetes en Azure, vea [Migrar cargas de trabajo de SQL Server Integration Services a la nube mediante lift-and-shift](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md).

No puede usar la información que aparece en este inicio rápido para ejecutar un paquete de SSIS en Linux. Para más información sobre cómo ejecutar paquetes en Linux, vea [Extract, transform, and load data on Linux with SSIS](../linux/sql-server-linux-migrate-ssis.md) (Extraer, transformar y cargar datos en Linux con SSIS).

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
