---
title: Migrar el esquema HR de Oracle a SQL Server en Linux | Microsoft Docs
description: Convertir el ejemplo de esquema de Oracle a SQL Server en Linux
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.suite: sql
ms.custom: ''
ms.technology: ssma
ms.openlocfilehash: c80a67028d1bb0d46596287b4ff168ce994af2a0
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2018
ms.locfileid: "36927116"
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>Migración de un esquema de Oracle a SQL Server 2017 en Linux con SQL Server Migration Assistant

Este tutorial usa SQL Server Migration Assistant (SSMA) para Oracle en Windows para convertir el ejemplo Oracle **HR** esquema [SQL Server 2017 en Linux](../../linux/sql-server-linux-overview.md).

> [!div class="checklist"]
> * Descarga e instalación de SSMA en Windows
> * Crear un proyecto SSMA para administrar la migración
> * Conectar con Oracle
> * Ejecutar un informe de migración
> * Convierta el esquema de ejemplo HR
> * Migrar los datos

## <a name="prerequisites"></a>Requisitos previos

- Una instancia de Oracle 12C (12.2.0.1.0) con el **HR** esquema instalado
- Una instancia de trabajo de SQL Server en Linux

> [!NOTE]
> Se pueden usar los mismos pasos para SQL Server en Windows de destino, pero debe seleccionar Windows en el **Migrate To** configuración del proyecto.

## <a name="download-and-install-ssma-for-oracle"></a>Descarga e instalación de SSMA para Oracle

Existen varias ediciones de SQL Server Migration Assistant, dependiendo de la base de datos de origen.  Descargue la versión actual de [SQL Server Migration Assistant para Oracle](http://aka.ms/ssmafororacle) e instalarlo mediante las instrucciones que encontrará en la página de descarga.

> [!NOTE]
> En este momento, el **SSMA para Oracle: paquete de extensión** no es compatible con Linux, pero no es necesario para este tutorial.

## <a name="create-and-set-up-project"></a>Crear y configurar proyecto

Use los pasos siguientes para crear un nuevo proyecto SSMA:

1. Abra SSMA para Oracle y elija **nuevo proyecto** desde el **archivo** menú.

1. Asigne al proyecto un nombre.

1. Elija "SQL Server 2017 (Linux): versión preliminar" en el **Migrate To** campo.

SSMA para Oracle no usa los esquemas de ejemplo de Oracle de forma predeterminada. Para habilitar el esquema de recursos humanos, siga estos pasos:

1. En SSMA, seleccione el **herramientas** menú.

1. Seleccione **la configuración predeterminada del proyecto**y, a continuación, elija **cargar objetos del sistema**.

1. Asegúrese de que **HR** está activada y elija **Aceptar**.

## <a name="connect-to-oracle"></a>Conectar con Oracle

A continuación, conéctese SSMA para Oracle.

1. En la barra de herramientas, haga clic en **conectar con Oracle**.

1. Escriba el nombre del servidor, puerto, el SID de Oracle, nombre de usuario y contraseña.

   ![Conectar con Oracle](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. Después, haga clic en **Conectar**. En unos instantes, SSMA para Oracle se conecta a la base de datos y lee sus metadatos.

## <a name="create-a-report"></a>Crear un informe

Siga estos pasos para generar un informe de migración.

1. En el **Explorador de metadatos de Oracle**, expanda el nodo del servidor.

1. Expanda **esquemas**, haga clic en **HR**y seleccione **crear informe**.

   ![Explorador de metadatos de Oracle crear informe](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. Se abre una nueva ventana del explorador con un informe que enumere todas las advertencias y errores asociados con la conversión.

   > [!NOTE]
   > No es necesario hacer nada con esa lista para este tutorial. Si realiza estos pasos para su propia base de datos de Oracle, debe revisar el informe para solucionar los problemas de conversión importante para la base de datos.

   ![Informe de migración de ejemplo](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>Conectar a SQL Server

A continuación, elija **conectar con SQL Server** y escriba la información de conexión adecuada.  Si usa un nombre de base de datos que aún no existe, SSMA para Oracle crea para usted.

![Conectar a SQL Server](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>Convertir esquema

Haga doble clic en **HR** en **Explorador de metadatos de Oracle**y elija convertir esquemas.

![Convertir esquema](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>Sincronizar la base de datos

A continuación, sincronizar la base de datos.

1. Una vez finalizada la conversión, utilice el **Explorador de metadatos de SQL Server** para ir a la base de datos que creó en el paso anterior.

1. Haga doble clic en la base de datos, seleccione **sincronizar con base de datos**y, a continuación, haga clic en Aceptar.

   ![Sincronizar con base de datos](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>Migración de datos

El último paso es migrar los datos.

1. En el **Explorador de metadatos de Oracle**, haga doble clic en **HR**y seleccione **migrar datos**.

1. El paso de migración de datos requiere que vuelva a escribir sus credenciales de Oracle y SQL Server.

1. Cuando termine, revise el informe de migración de datos, que debe ser similar a la captura de pantalla siguiente:

   ![Informe de migración de datos](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>Pasos siguientes

Para un esquema Orcale más complejo, el proceso de conversión implicaría más tiempo, las pruebas y los posibles cambios en las aplicaciones cliente. El propósito de este tutorial es mostrar cómo puede usar SSMA para Oracle como parte de su proceso de migración general.

En este tutorial, ha aprendido cómo:
> [!div class="checklist"]
> * Instalación de SSMA en Windows
> * Cree un nuevo proyecto SSMA
> * Evaluar y ejecutar una migración desde Oracle

A continuación, explorar otras formas de usar SSMA:

> [!div class="nextstepaction"]
>[Documentación de SQL Server Migration Assistant](../sql-server-migration-assistant.md)
