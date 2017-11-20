---
title: Ejecutar un paquete SSIS con SSMS | Documentos de Microsoft
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
ms.openlocfilehash: bbc17907311785ef98560493cb453b7b9b6d1556
ms.contentlocale: es-es
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-with-sql-server-management-studio-ssms"></a>Ejecutar un paquete SSIS con SQL Server Management Studio (SSMS)
Este inicio rápido muestra cómo usar SQL Server Management Studio (SSMS) para conectarse a la base de datos de catálogo de SSIS y, a continuación, ejecutar un paquete SSIS que se almacenan en el catálogo de SSIS del explorador de objetos en SSMS.

SQL Server Management Studio es un entorno integrado para administrar cualquier infraestructura de SQL de SQL Server a la base de datos SQL. Para obtener más información acerca de SSMS, vea [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, asegúrese de que tiene la versión más reciente de SQL Server Management Studio (SSMS). Para descargar SSMS, vea [descargar SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssisdb-database"></a>Conectarse a la base de datos SSISDB

Usar SQL Server Management Studio para establecer una conexión con el catálogo de SSIS. 

> [!NOTE]
> Un servidor de base de datos de SQL Azure escucha en el puerto 1433. Si está intentando conectarse a un servidor de base de datos de SQL Azure desde dentro de un firewall corporativo, este puerto debe estar abierto en el firewall corporativo para poder conectarse correctamente.

1. Abra SQL Server Management Studio.

2. En el **conectar al servidor** diálogo cuadro, escriba la siguiente información:

   | Configuración       | Valor recomendado | Más información | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Motor de base de datos | Este valor es necesario. |
   | **Nombre del servidor** | El nombre completo del servidor | Si se está conectando a un servidor de base de datos de SQL Azure, el nombre está en este formato: `<server_name>.database.windows.net`. |
   | **Autenticación** | Autenticación de SQL Server | Este tutorial rápido usa la autenticación de SQL. |
   | **Inicio de sesión** | La cuenta de administrador de servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña** | La contraseña de la cuenta de administrador del servidor | Esta es la contraseña que especificó cuando creó el servidor. |

3. Haga clic en **Conectar**. Se abre la ventana de explorador de objetos en SSMS. 

4. En el Explorador de objetos, expanda **catálogos de Integration Services** y, a continuación, expanda **SSISDB** para ver los objetos en la base de datos de catálogo de SSIS.

## <a name="run-a-package"></a>Ejecutar un paquete

1. En el Explorador de objetos, seleccione el paquete que se va a ejecutar.

2. Haga clic en y seleccione **Execute**. El **Ejecutar paquete** abre el cuadro de diálogo.

3.  Configurar la ejecución del paquete mediante la configuración en el **parámetros**, **administradores de conexión**, y **avanzadas** fichas en el cuadro de diálogo Ejecutar paquete.

4.  Haga clic en Aceptar para ejecutar el paquete.

## <a name="next-steps"></a>Pasos siguientes
- Tenga en cuenta otras formas para ejecutar un paquete.
    - [Ejecutar un paquete SSIS con Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (frente a código)](ssis-quickstart-run-tsql-vscode.md)
    - [Ejecutar un paquete SSIS desde la línea de comandos](./ssis-quickstart-run-cmdline.md)
    - [Ejecutar un paquete SSIS con PowerShell](ssis-quickstart-run-powershell.md)
    - [Ejecutar un paquete SSIS con C#](./ssis-quickstart-run-dotnet.md) 

