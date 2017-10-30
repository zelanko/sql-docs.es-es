---
title: Implementar un proyecto de SSIS con SSMS | Documentos de Microsoft
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: b9729343ab14563ee6264795d6f098f3c22e91bf
ms.contentlocale: es-es
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-with-sql-server-management-studio-ssms"></a>Implementar un proyecto de SSIS con SQL Server Management Studio (SSMS)
Este inicio rápido muestra cómo usar SQL Server Management Studio (SSMS) para conectarse a la base de datos de catálogo de SSIS y, a continuación, ejecute el Asistente para la implementación de Integration Services para implementar un proyecto de SSIS en el catálogo de SSIS. 

SQL Server Management Studio es un entorno integrado para administrar cualquier infraestructura de SQL de SQL Server a la base de datos SQL. Para obtener más información acerca de SSMS, vea [SQL Server Management Studio (SSMS)](../ssms/sql-server-management-studio-ssms.md).

## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, asegúrese de que tiene la última versión de SQL Server Management Studio. Para descargar SSMS, vea [descargar SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="connect-to-the-ssisdb-database"></a>Conectarse a la base de datos SSISDB

Usar SQL Server Management Studio para establecer una conexión con el catálogo de SSIS. 

> [!NOTE]
> Un servidor de base de datos de SQL Azure escucha en el puerto 1433. Si está intentando conectarse a un servidor de base de datos de SQL Azure desde dentro de un firewall corporativo, este puerto debe estar abierto en el firewall corporativo para poder conectarse correctamente.

1. Abra SQL Server Management Studio.

2. En el **conectar al servidor** diálogo cuadro, escriba la siguiente información:

   | Configuración       | Valor recomendado | Más información | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Motor de base de datos | Este valor es necesario. |
   | **Nombre del servidor** | El nombre completo del servidor | Si se está conectando a un servidor de base de datos de SQL Azure, el nombre está en este formato: `<server_name>.database.windows.net`. |
   | **Autenticación** | Autenticación de SQL Server | Este tutorial rápido usa la autenticación de SQL. |
   | **Inicio de sesión** | La cuenta de administrador de servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña** | La contraseña de la cuenta de administrador del servidor | Esta es la contraseña que especificó cuando creó el servidor. |

3. Haga clic en **Conectar**. Se abre la ventana de explorador de objetos en SSMS. 

4. En el Explorador de objetos, expanda **catálogos de Integration Services** y, a continuación, expanda **SSISDB** para ver los objetos en la base de datos de catálogo de SSIS.

## <a name="start-the-integration-services-deployment-wizard"></a>Iniciar al Asistente para la implementación de Integration Services
1. En el Explorador de objetos, con el **catálogos de Integration Services** nodo y **SSISDB** expandido, expanda una carpeta de proyecto.

2.  Seleccione el **proyectos** nodo.

3.  Haga doble clic en el **proyectos** nodo y seleccione **implementar proyecto**. Se abre el Asistente para la implementación de Integration Services. Puede implementar un proyecto desde el catálogo actual o desde el sistema de archivos.

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
    - [Implementar un paquete SSIS con Transact-SQL (SSMS)](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Implementar un paquete SSIS con Transact-SQL (frente a código)](ssis-quickstart-deploy-tsql-vscode.md)
    - [Implementar un paquete SSIS desde el símbolo del sistema](./ssis-quickstart-deploy-cmdline.md)
    - [Implementar un paquete SSIS con PowerShell](ssis-quickstart-deploy-powershell.md)
    - [Implementar un paquete SSIS con C#](./ssis-quickstart-deploy-dotnet.md) 
- Ejecutar un paquete implementado. Para ejecutar un paquete, puede elegir entre varias herramientas y lenguajes. Para obtener más información, vea los siguientes artículos:
    - [Ejecutar un paquete SSIS con SSMS](./ssis-quickstart-run-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (SSMS)](./ssis-quickstart-run-tsql-ssms.md)
    - [Ejecutar un paquete SSIS con Transact-SQL (frente a código)](ssis-quickstart-run-tsql-vscode.md)
    - [Ejecutar un paquete SSIS desde la línea de comandos](./ssis-quickstart-run-cmdline.md)
    - [Ejecutar un paquete SSIS con PowerShell](ssis-quickstart-run-powershell.md)
    - [Ejecutar un paquete SSIS con C#](./ssis-quickstart-run-dotnet.md) 

