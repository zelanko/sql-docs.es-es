---
title: Conectarse a la base de datos del catálogo de SSIS (SSISDB) en Azure | Microsoft Docs
ms.date: 09/25/2017
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.component: lift-shift
ms.suite: sql
ms.custom: ''
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 639f02809a003bc5418ecb5ec33930f89205701f
ms.sourcegitcommit: 0cc2cb281e467a13a76174e0d9afbdcf4ccddc29
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2018
---
# <a name="connect-to-the-ssis-catalog-database-ssisdb-in-azure"></a>Conectarse a la base de datos del catálogo de SSIS (SSISDB) en Azure

Obtenga la información de conexión necesaria para conectarse a la base de datos del catálogo de SSISDB hospedada en un servidor de Azure SQL Database. Necesita los siguientes elementos para poder conectarse:
- Un nombre completo de servidor
- El nombre de la base de datos
- La información de inicio de sesión 

> [!IMPORTANT]
> En la versión 2 de Azure Data Factory, en estos momentos no se puede crear la base de datos del catálogo SSISDB en Azure SQL Database, independientemente de la creación del entorno de ejecución de integración de Azure-SSIS. El entorno de ejecución de Azure-SSIS es el que ejecuta los paquetes SSIS en Azure. Para obtener más información, vea [Implementación de paquetes SSIS en Azure](https://docs.microsoft.com/azure/data-factory/tutorial-create-azure-ssis-runtime-portal). 

## <a name="prerequisites"></a>Prerequisites
Antes de comenzar, asegúrese de que tiene instalada la versión 17.2 (o posterior) de SQL Server Management Studio (SSMS). Si la base de datos del catálogo de SSISDB se hospeda en Instancia administrada de SQL Database (versión preliminar), asegúrese de tener la versión 17.6 o una versión posterior de SSMS. Para descargar la versión más reciente de SSMS, consulte [Download SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) [Descargar SQL Server Management Studio (SSMS)].

## <a name="get-the-connection-info-from-the-azure-portal"></a>Obtener la información de conexión desde Azure Portal
1. Inicie sesión en el [Portal de Azure](https://portal.azure.com/).
2. En Azure Portal, seleccione **Bases de datos SQL** desde el menú izquierdo y, a continuación, seleccione la base de datos `SSISDB` en la página **Bases de datos SQL**. 
3. En la página **Introducción** de la base de datos `SSISDB`, compruebe el nombre completo del servidor tal como se muestra en la siguiente imagen. Mantenga el puntero sobre el nombre del servidor para que aparezca la opción **Haga clic para copiar**.

    ![Información de conexión del servidor](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. Si ha olvidado la información de inicio de sesión del servidor de SQL Database, vaya a la página del servidor de SQL Database. En ella podrá ver el nombre de administrador del servidor y, si fuera necesario, podrá restablecer la contraseña.

## <a name="connect-with-ssms"></a>Conectarse con SSMS
1. Abra SQL Server Management Studio.

2. **Conéctese al servidor**. En el cuadro de diálogo **Conectar con el servidor**, escriba la información siguiente:

   | Configuración       | Valor sugerido | Descripción | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Motor de base de datos | Este valor es necesario. |
   | **Nombre del servidor** | Nombre completo del servidor | El nombre debe tener este formato: **mysqldbserver.database.windows.net**. |
   | **Autenticación** | Autenticación de SQL Server | Esta guía de inicio rápido usa la autenticación SQL. |
   | **Inicio de sesión** | Cuenta de administrador del servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña** | Contraseña de la cuenta de administrador del servidor | Se trata de la contraseña que especificó cuando creó el servidor. |

    ![Conexión al servidor con SSMS](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-1.png)

3. **Conéctese a la base de datos de SSISDB**. Seleccione **Opciones** para expandir el cuadro de diálogo **Conectar con el servidor**. En el cuadro de diálogo **Conectar con el servidor** expandido, seleccione la pestaña **Propiedades de conexión**. En el campo **Conectar con la base de datos**, seleccione o especifique `SSISDB`.

    > [!IMPORTANT]
    > Si no selecciona `SSISDB` cuando se conecte, es posible que no vea el catálogo de SSIS en el Explorador de objetos.

    ![Selección de la base de datos SSISDB para la conexión](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-2.png)

4. A continuación, seleccione **Conectar**.

5. En el Explorador de objetos, expanda la opción **Catálogos de Integration Services** y, a continuación, expanda **SSISDB** para ver los objetos de la base de datos del catálogo de SSIS.

    ![Búsqueda de la base de datos SSISDB en el Explorador de objetos de SSMS](media/ssis-azure-connect-to-catalog-database/ssisdb-connect-3.png)

## <a name="next-steps"></a>Pasos siguientes
- Implementar un paquete. Para obtener más información, consulte [Deploy an SSIS project with SQL Server Management Studio (SSMS) (Implementar un proyecto de SSIS con SQL Server Management Studio [SSMS])](../ssis-quickstart-deploy-ssms.md).
- Ejecutar un paquete. Para obtener más información, consulte [Run an SSIS package with SQL Server Management Studio (SSMS) (Ejecutar un paquete de SSIS con SQL Server Management Studio [SSMS])](../ssis-quickstart-run-ssms.md).
- Programar un paquete. Para obtener más información, consulte [Schedule SSIS package execution on Azure (Programar la ejecución de paquetes de SSIS en Azure)](ssis-azure-schedule-packages.md).
