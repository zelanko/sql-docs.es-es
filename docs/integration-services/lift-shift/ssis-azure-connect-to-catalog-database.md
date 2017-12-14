---
title: "Conectarse a la base de datos del catálogo de SSISDB en Azure | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: lift-shift
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10be16cbc85cccce51fafbcd733045c653b7be0a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-the-ssisdb-catalog-database-on-azure"></a>Conectarse a la base de datos del catálogo de SSISDB en Azure

Obtenga la información de conexión necesaria para conectarse a la base de datos del catálogo de SSISDB hospedada en un servidor de Azure SQL Database. Necesita los siguientes elementos para poder conectarse:
- Un nombre completo de servidor
- El nombre de la base de datos
- La información de inicio de sesión 

## <a name="prerequisites"></a>Requisitos previos
Antes de comenzar, asegúrese de que tiene instalada la versión 17.2 (o posterior) de SQL Server Management Studio. Para descargar la versión más reciente de SSMS, consulte [Download SQL Server Management Studio (SSMS) (Descargar SQL Server Management Studio [SSMS])](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="get-the-connection-info-from-the-azure-portal"></a>Obtener la información de conexión desde Azure Portal
1. Inicie sesión en el [Portal de Azure](https://portal.azure.com/).
2. En Azure Portal, seleccione **Bases de datos SQL** desde el menú izquierdo y, a continuación, seleccione la base de datos `SSISDB` en la página **Bases de datos SQL**. 
3. En la página **Introducción** de la base de datos `SSISDB`, compruebe el nombre completo del servidor tal como se muestra en la siguiente imagen. Mantenga el puntero sobre el nombre del servidor para que aparezca la opción **Haga clic para copiar**.

    ![Información de conexión del servidor](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. Si ha olvidado la información de inicio de sesión del servidor de SQL Database, vaya a la página del servidor de SQL Database. En ella podrá ver el nombre de administrador del servidor y, si fuera necesario, podrá restablecer la contraseña.

## <a name="connect-with-ssms"></a>Conectarse con SSMS
1. Abra SQL Server Management Studio.

2. **Conéctese al servidor**. Escriba la información siguiente en el cuadro de diálogo **Conectarse al servidor**:

   | Configuración       | Valor sugerido | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Motor de base de datos | Este valor es necesario. |
   | **Nombre del servidor** | Nombre completo del servidor | El nombre debe tener este formato: **mysqldbserver.database.windows.net**. |
   | **Autenticación** | Autenticación de SQL Server | Esta guía de inicio rápido usa la autenticación SQL. |
   | **Inicio de sesión** | Cuenta de administrador del servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña** | Contraseña de la cuenta de administrador del servidor | Se trata de la contraseña que especificó cuando creó el servidor. |

3. **Conéctese a la base de datos de SSISDB**. Seleccione **Opciones** para expandir el cuadro de diálogo **Conectar con el servidor**. En el cuadro de diálogo **Conectar con el servidor** expandido, seleccione la pestaña **Propiedades de conexión**. En el campo **Conectar con la base de datos**, seleccione o especifique `SSISDB`.

    > [!IMPORTANT]
    > Si no selecciona `SSISDB` cuando se conecte, es posible que no vea el catálogo de SSIS en el Explorador de objetos.

4. Seleccione **Conectar**.

5. En el Explorador de objetos, expanda la opción **Catálogos de Integration Services** y, a continuación, expanda **SSISDB** para ver los objetos de la base de datos del catálogo de SSIS.

## <a name="next-steps"></a>Pasos siguientes
- Implementar un paquete. Para obtener más información, consulte [Deploy an SSIS project with SQL Server Management Studio (SSMS) (Implementar un proyecto de SSIS con SQL Server Management Studio [SSMS])](../ssis-quickstart-deploy-ssms.md).
- Ejecutar un paquete. Para obtener más información, consulte [Run an SSIS package with SQL Server Management Studio (SSMS) (Ejecutar un paquete de SSIS con SQL Server Management Studio [SSMS])](../ssis-quickstart-run-ssms.md).
- Programar un paquete. Para obtener más información, consulte [Schedule SSIS package execution on Azure (Programar la ejecución de paquetes de SSIS en Azure)](ssis-azure-schedule-packages.md).
