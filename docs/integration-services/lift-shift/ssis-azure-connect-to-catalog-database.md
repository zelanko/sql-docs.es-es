---
title: "Conectarse a la base de datos de catálogo de SSISDB en Azure | Documentos de Microsoft"
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
ms.sourcegitcommit: 560965a241b24a09f50a23faf63ce74d0049d5a7
ms.openlocfilehash: ac121e600c3c616006d79892c50f796ca7cd6b3f
ms.contentlocale: es-es
ms.lasthandoff: 10/13/2017

---
# <a name="connect-to-the-ssisdb-catalog-database-on-azure"></a>Conectarse a la base de datos de catálogo de SSISDB en Azure

Obtener la información de conexión necesaria para conectarse a la base de datos de catálogo de SSISDB hospedada en un servidor de base de datos de SQL Azure. Necesita los siguientes elementos para conectarse:
- nombre completo del servidor
- Nombre de base de datos
- información de inicio de sesión 

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar, asegúrese de que tiene versión 17.2 u otra posterior de SQL Server Management Studio. Para descargar la versión más reciente de SSMS, vea [descargar SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

## <a name="get-the-connection-info-from-the-azure-portal"></a>Obtener la información de conexión desde el portal de Azure
1. Inicie sesión en el [Portal de Azure](https://portal.azure.com/).
2. En el portal de Azure, seleccione **bases de datos SQL** desde el menú izquierdo y, a continuación, seleccione la `SSISDB` en la base de datos la **bases de datos SQL** página. 
3. En el **Introducción** página para el `SSISDB` la base de datos, revise el nombre completo del servidor tal como se muestra en la siguiente imagen. Mantenga el mouse sobre el nombre del servidor para que aparezca el **haga clic aquí para copiar** opción.

    ![Información de conexión de servidor](media/ssis-azure-connect-to-catalog-database/server-name.png) 

4. Si ha olvidado la información de inicio de sesión para el servidor de base de datos SQL, vaya a la página de base de datos de SQL server. Podrá ver el administrador del servidor el nombre y, si es necesario, restablezca la contraseña.

## <a name="connect-with-ssms"></a>Conectar con SSMS
1. Abra SQL Server Management Studio.

2. **Conectarse al servidor**. En el **conectar al servidor** diálogo cuadro, escriba la siguiente información:

   | Configuración       | Valor recomendado | Description | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Tipo de servidor** | Motor de base de datos | Este valor es necesario. |
   | **Nombre del servidor** | El nombre completo del servidor | El nombre debe tener este formato: **mysqldbserver.database.windows.net**. |
   | **Autenticación** | Autenticación de SQL Server | Este tutorial rápido usa la autenticación de SQL. |
   | **Inicio de sesión** | La cuenta de administrador de servidor | Se trata de la cuenta que especificó cuando creó el servidor. |
   | **Contraseña** | La contraseña de la cuenta de administrador del servidor | Esta es la contraseña que especificó cuando creó el servidor. |

3. **Conectarse a la base de datos SSISDB**. Seleccione **opciones** para expandir el **conectar al servidor** cuadro de diálogo. En el esquema **conectar al servidor** cuadro de diálogo, seleccione la **propiedades de conexión** ficha. En el **conectar con base de datos** campo, seleccione o especifique `SSISDB`.

    > [!IMPORTANT]
    > Si no selecciona `SSISDB` cuando se conecte, quizás no vea el catálogo de SSIS en el Explorador de objetos.

4. A continuación, seleccione **conectar**.

5. En el Explorador de objetos, expanda **catálogos de Integration Services** y, a continuación, expanda **SSISDB** para ver los objetos en la base de datos de catálogo de SSIS.

## <a name="next-steps"></a>Pasos siguientes
- Implementar un paquete. Para obtener más información, consulte [implementar un proyecto de SSIS con SQL Server Management Studio (SSMS)](../ssis-quickstart-deploy-ssms.md).
- Ejecutar un paquete. Para obtener más información, consulte [ejecutar un paquete SSIS con SQL Server Management Studio (SSMS)](../ssis-quickstart-run-ssms.md).
- Programar un paquete. Para obtener más información, consulte [paquetes de SSIS de programación de ejecución en Azure](ssis-azure-schedule-packages.md)

