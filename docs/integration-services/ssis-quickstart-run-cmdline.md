---
title: "Ejecutar un paquete SSIS desde la línea de comandos | Documentos de Microsoft"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: a33b8518ec3284f5de73d38c87209057dc1c7487
ms.contentlocale: es-es
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>Ejecutar un paquete SSIS desde el símbolo del sistema con DTExec.exe
Este tutorial de inicio rápido muestra cómo ejecutar un paquete SSIS desde el símbolo del sistema mediante la ejecución de `DTExec.exe` con los parámetros adecuados.

> [!NOTE]
> El método descrito en este artículo no se ha probado con los paquetes que se implementen en un servidor de base de datos de SQL Azure.

Para obtener más información acerca de `DTExec.exe`, consulte [dtexec (utilidad)](https://docs.microsoft.com/en-us/sql/integration-services/packages/dtexec-utility).

## <a name="run-a-package-with-dtexec"></a>Ejecutar un paquete con dtexec

Si la carpeta que contiene `DTExec.exe` no está en su `path` variable de entorno, es podrán que deba utilizar la `cd` comando para cambiar a su directorio. En SQL Server 2017, esta carpeta es normalmente `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`.

Con los valores de parámetro utilizados en el ejemplo siguiente, el programa ejecuta el paquete en la ruta de acceso de la carpeta especificada en el servidor SSIS: es decir, el servidor que hospeda la base de datos de catálogo de SSIS (SSISDB). El `/Server` parámetro proporciona el nombre del servidor. El programa se conecta como el usuario actual con la autenticación integrada de Windows. Para utilizar autenticación de SQL, especifique la `/User` y `Password` parámetros con valores adecuados.

1. Abra una ventana de símbolo del sistema.

2. Ejecutar `DTExec.exe` y proporcione valores al menos para la `ISServer` y `Server` parámetros, como se muestra en el ejemplo siguiente:

    ```cmd
    dtexec /ISServer "\SSISDB\Project1Folder\Integration Services Project1\Package.dtsx" /Server "localhost"
    ```

## <a name="next-steps"></a>Pasos siguientes
- Tenga en cuenta otras formas para ejecutar un paquete.
    - [Ejecutar un paquete SSIS con SSMS](./ssis-quickstart-run-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (frente a código)](ssis-quickstart-run-tsql-vscode.md)
    - [Ejecutar un paquete SSIS con PowerShell](ssis-quickstart-run-powershell.md)
    - [Ejecutar un paquete SSIS con C#](./ssis-quickstart-run-dotnet.md) 

