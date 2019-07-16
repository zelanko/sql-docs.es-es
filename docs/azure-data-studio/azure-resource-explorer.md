---
title: Explore los recursos de SQL Azure con Azure Resource Explorer
titleSuffix: Azure Data Studio
description: Obtenga información sobre cómo explorar y administrar la instancia administrada de SQL Azure a través de Azure Resource Explorer, Azure SQL Database y Azure SQL Server.
ms.custom: seodec18
author: yanancai
ms.author: yanacai
ms.date: 09/24/2018
ms.topic: quickstart
ms.prod: sql
ms.technology: azure-data-studio
ms.openlocfilehash: 87a0364555b9da22c89470965c281b3d939b6f4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959714"
---
# <a name="explore-and-manage-azure-sql-resources-with-azure-resource-explorer"></a>Explorar y administrar recursos de SQL Azure con Azure Resource Explorer

En este documento, obtendrá información sobre cómo puede explorar y administrar Azure SQL Server, base de datos SQL de Azure y los recursos de la instancia administrada de SQL Azure a través de Azure Resource Explorer en [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)].

>[!NOTE]
>El Explorador de recursos de Azure se admitirá en versión preliminar de SQL Server 2019 en octubre. Después de eso, puede instalar la extensión de la versión preliminar a través de [Administrador de extensiones](extensions.md) o a través **archivo** > **Instalar paquete de paquete VSIX**.


## <a name="connect-to-azure"></a>Conectarse a Azure

Después de instalar el complemento de la versión preliminar SQL, aparece un icono de Azure en la barra de menú de la izquierda. Haga clic en el icono para abrir el Explorador de recursos de Azure. Si no ve el icono de Azure, a la derecha, haga clic en la barra de menú de la izquierda y seleccione **Azure Resource Explorer**.

### <a name="add-an-azure-account"></a>Agregar una cuenta de Azure

Para ver los recursos SQL asociados con una cuenta de Azure, primero debe agregar la cuenta a [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)].

1. Abra **cuentas vinculadas** diálogo a través del icono de administración de la cuenta en la parte inferior izquierda o a través de **iniciar sesión en Azure...**  vínculo en el Explorador de recursos de Azure.

    ![Inicie sesión en Azure](media/azure-resource-explorer/sign-in-to-azure.png)

2. En el **cuentas vinculadas** cuadro de diálogo, haga clic en **agregar una cuenta**.

    ![Agregar una cuenta de Azure](media/azure-resource-explorer/add-an-azure-account.png)

3. Haga clic en **copiar y abrir** para abrir el explorador para la autenticación.

    ![Página de autenticación abierta en el explorador](media/azure-resource-explorer/open-authentication-in-browser.png)

4. Pegar la **código de usuario** en la página web y haga clic en **continuar** para autenticar.

    ![Realizar la autenticación en el explorador](media/azure-resource-explorer/authenticate-in-browser.png)

5. En [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)] ahora debe buscar el inicio de sesión en la cuenta de Azure en **cuentas vinculadas** cuadro de diálogo.

    ![Cuenta de Azure con sesión iniciada](media/azure-resource-explorer/signed-in-azure-account.png)

### <a name="add-more-azure-accounts"></a>Agregar cuentas de Azure más

Varias cuentas de Azure se admiten en [!INCLUDE [Azure Data Studio](../includes/name-sos-short.md)]. Para agregar cuentas de Azure más, haga clic en el botón en la parte superior derecha de **cuentas vinculadas** cuadro de diálogo y siga los mismos pasos con agregan una sección de la cuenta de Azure para agregar cuentas de Azure más.

![Agregar cuenta de Azure más](media/azure-resource-explorer/add-more-azure-account.png)

### <a name="remove-an-azure-account"></a>Quitar una cuenta de Azure

Para quitar una cuenta de Azure conectada existente:

1. Abra **cuentas vinculadas** diálogo a través del icono de administración de la cuenta en la parte inferior izquierda.
2. Haga clic en el **X** situado a la derecha de la cuenta de Azure para quitarlo.

    ![Quitar cuenta de Azure](media/azure-resource-explorer/remove-azure-account.png)

## <a name="filter-subscription"></a>Filtrar suscripciones

Una vez que inicia sesión en una cuenta de Azure, todas las suscripciones asociadas con esa cuenta de Azure de presentación en el Explorador de recursos de Azure. Puede filtrar las suscripciones para cada cuenta de Azure.

1. Haga clic en el **Select Subscription** situado a la derecha de la cuenta de Azure.

   ![Filtrar suscripciones](media/azure-resource-explorer/filter-subscription.png)

2. Seleccione las casillas de las suscripciones que desea examinar y, a continuación, haga clic en la cuenta **Aceptar**.

   ![Selección de la suscripción](media/azure-resource-explorer/select-subscription.png)

## <a name="explore-azure-sql-resources"></a>Explore los recursos de SQL Azure

Para navegar por un recurso de SQL Azure en Azure Resource Explorer, expanda las cuentas de Azure y el grupo de tipos de recursos.

Explorador de recursos de Azure es compatible con Azure SQL Server, Azure SQL Database y Azure SQL Managed Instance actualmente.

## <a name="connect-to-azure-sql-resources"></a>Conectarse a los recursos de SQL Azure

Explorador de recursos de Azure proporcionan acceso rápido que le permite conectarse a servidores SQL Server y bases de datos para la administración y consulta. 

1. Explore el recurso de SQL que le gustaría conectar desde la vista de árbol.
2. Haga clic en el recurso y seleccione **Connect**, también puede encontrar el botón Conectar a la derecha del recurso.

   ![Conectarse a recursos de SQL Azure](media/azure-resource-explorer/connect-to-azure-sql-resource.png)

3. En el modo abierto **conexión** cuadro de diálogo, escriba la contraseña y haga clic en **Connect**.

   ![Cuadro de diálogo de conexión de SQL](media/azure-resource-explorer/sql-connection-dialog.png)
4. El **servidores** ventana se abre automáticamente con el nuevo SQL server/base de datos conectada una vez finalizada correctamente la conexión.

## <a name="next-steps"></a>Pasos siguientes

- [Use [!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] para conectarse y consultar la base de datos SQL de Azure](quickstart-sql-database.md)
- [Use [!INCLUDE[Azure Data Studio](../includes/name-sos-short.md)] para conectarse y consultar datos en Azure SQL Data Warehouse](quickstart-sql-dw.md)