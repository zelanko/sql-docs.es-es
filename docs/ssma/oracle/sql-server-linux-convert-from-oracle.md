---
title: Migrar el esquema de recursos humanos de Oracle a SQL Server en Linux | Documentos de Microsoft
description: Convertir el esquema de ejemplo Oracle a SQL Server en Linux
author: edmacauley
ms.author: edmacauley
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: f4ab25f440db693c0fd81093f6191fc0c3390ebb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>Migración de un esquema de Oracle a SQL Server 2017 en Linux con SQL Server Migration Assistant

Este tutorial usa SQL Server Migration Assistant (SSMA) para Oracle en Windows para convertir el ejemplo Oracle **HR** esquema a [2017 de SQL Server en Linux](../../linux/sql-server-linux-overview.md).

> [!div class="checklist"]
> * Descargue e instale SSMA en Windows
> * Crear un proyecto SSMA para administrar la migración
> * Conectar con Oracle
> * Ejecutar un informe de migración
> * Convertir el esquema de recursos humanos de ejemplo
> * migrar los datos

## <a name="prerequisites"></a>Prerequisites

- Una instancia de Oracle 12C (12.2.0.1.0) con el **HR** esquema instalado
- Una instancia de trabajo de SQL Server en Linux

> [!NOTE]
> Los mismos pasos que pueden usarse para dirigidas a SQL Server en Windows, pero debe activar Windows en el **Migrate To** configuración del proyecto.

## <a name="download-and-install-ssma-for-oracle"></a>Descargue e instale SSMA para Oracle

Hay varias ediciones de SQL Server Migration Assistant disponibles, dependiendo de la base de datos de origen.  Descargar la versión actual de [SQL Server Migration Assistant para Oracle](http://aka.ms/ssmafororacle) e instalarlo mediante las instrucciones que encontrará en la página de descarga.

> [!NOTE]
> En este momento, el **SSMA para paquete de extensión de Oracle** no se admite en Linux, pero no es necesario para este tutorial.

## <a name="create-and-set-up-project"></a>Crear y proyecto de instalación

Utilice los pasos siguientes para crear un nuevo proyecto SSMA:

1. Abra SSMA para Oracle y elija **nuevo proyecto** desde el **archivo** menú.

1. Asigne un nombre al proyecto.

1. Elija "2017 (Linux) - vista previa SQL Server" en la **Migrate To** campo.

SSMA para Oracle no usa los esquemas de ejemplo de Oracle de forma predeterminada. Para habilitar el esquema de recursos humanos, siga estos pasos:

1. En SSMA, seleccione la **herramientas** menú.

1. Seleccione **la configuración predeterminada del proyecto**y, a continuación, elija **cargar objetos del sistema**.

1. Asegúrese de que **HR** está activada y elija **Aceptar**.

## <a name="connect-to-oracle"></a>Conectar con Oracle

A continuación conectar SSMA para Oracle.

1. En la barra de herramientas, haga clic en **conectar con Oracle**.

1. Escriba el nombre del servidor, la puerto, el SID de Oracle, los nombre de usuario y la contraseña.

   ![Conectar con Oracle](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. Después, haga clic en **Conectar**. En unos instantes, SSMA para Oracle se conecta a la base de datos y lee sus metadatos.

## <a name="create-a-report"></a>Crear un informe

Siga estos pasos para generar un informe de migración.

1. En el **Explorador de metadatos de Oracle**, expanda el nodo de su servidor.

1. Expanda **esquemas**, haga clic en **HR**y seleccione **crear informe**.

   ![Explorador de metadatos de Oracle crear informe](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. Se abre una nueva ventana del explorador con un informe que enumere todas las advertencias y errores asociados con la conversión.

   > [!NOTE]
   > No es necesario hacer nada con esa lista para este tutorial. Si realiza estos pasos para su propia base de datos de Oracle, debe revisar el informe para solucionar los problemas de conversión importante para la base de datos.

   ![Informe de migración de ejemplo](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>Conectar a SQL Server

A continuación elija **conectar con SQL Server** y escriba la información de conexión adecuada.  Si utiliza un nombre de base de datos que aún no existe, SSMA para Oracle crea para usted.

![Conectar a SQL Server](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>Convertir esquema

Haga doble clic en **HR** en **Explorador de metadatos de Oracle**y elija convertir esquema.

![Convertir esquema](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>Sincronizar la base de datos

A continuación, sincronizar la base de datos.

1. Una vez finalizada la conversión, utilice la **Explorador de metadatos de SQL Server** para ir a la base de datos que creó en el paso anterior.

1. Haga doble clic en la base de datos, seleccione **sincronizar con la base de datos**y, a continuación, haga clic en Aceptar.

   ![Sincronizar con la base de datos](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>Migrar datos

El último paso es migrar los datos.

1. En el **Explorador de metadatos de Oracle**, haga doble clic en **HR**y seleccione **migrar datos**.

1. El paso de migración de datos requiere que vuelva a escribir las credenciales de Oracle y SQL Server.

1. Cuando termine, revise el informe de migración de datos, que debe ser similar a la captura de pantalla siguiente:

   ![Informe de migración de datos](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>Pasos siguientes

Para un esquema de Orcale más complejo, el proceso de conversión implicaría más tiempo, las pruebas y posibles cambios en las aplicaciones cliente. El propósito de este tutorial es mostrar cómo puede usar SSMA para Oracle como parte del proceso de migración general.

En este tutorial, ha aprendido cómo:
> [!div class="checklist"]
> * Instalar SSMA en Windows
> * Cree un nuevo proyecto SSMA
> * Evaluar y ejecutar una migración de Oracle

A continuación, explore otras formas de usar SSMA:

> [!div class="nextstepaction"]
>[Documentación de SQL Server Migration Assistant](../sql-server-migration-assistant.md)
