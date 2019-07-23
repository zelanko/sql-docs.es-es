---
title: 'Tutorial: Creación y uso de índices en columnas basadas en enclave mediante el cifrado aleatorio | Microsoft Docs'
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 9865be1d006e10271295ae4dda731eb33331dbda
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126796"
---
# <a name="tutorial-creating-and-using-indexes-on-enclave-enabled-columns-using-randomized-encryption"></a>Tutorial: Creación y uso de índices en columnas basadas en enclave mediante cifrado aleatorio
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este tutorial le enseña a crear y usar índices en columnas habilitadas para enclave que usan el cifrado aleatorio admitido en [Always Encrypted con enclaves seguros](encryption/always-encrypted-enclaves.md). En él encontrará:

- Cómo crear un índice cuando tiene acceso a las claves (la clave maestra de columna y la clave de cifrado de columna) que protegen la columna.
- Cómo crear un índice cuando no tiene acceso a las claves que protegen la columna.

## <a name="prerequisites"></a>Prerequisites

Este tutorial es la continuación del [Tutorial: Introducción a Always Encrypted con enclaves seguros con SSMS](./tutorial-getting-started-with-always-encrypted-enclaves.md). Asegúrese de haberlo completado antes de seguir los pasos siguientes.

## <a name="step-1-enable-accelerated-database-recovery-adr-in-your-database"></a>Paso 1: Habilitación de la recuperación de base de datos acelerada (ADR) en la base de datos

Microsoft recomienda encarecidamente habilitar ADR en la base de datos antes de crear el primer índice en una columna habilitada para enclave que usa cifrado aleatorio. Consulte la sección [Recuperación de la base de datos](./encryption/always-encrypted-enclaves.md##database-recovery) del tutorial [Always Encrypted con enclaves seguros](./encryption/always-encrypted-enclaves.md).

1. Cierre todas las instancias SSMS que usó en el tutorial anterior. Las conexiones abiertas de base de datos se cerrarán, lo que es necesario para habilitar ADR.
1. Abra una nueva instancia de SSMS y conéctese a la instancia de SQL Server como sysadmin **sin** Always Encrypted habilitado para la conexión de base de datos.
    1. Inicie SSMS.
    1. En el cuadro de diálogo **Conectar a servidor**, especifique el nombre del servidor, seleccione un método de autenticación e indique sus credenciales.
    1. Haga clic en **Opciones >>** y seleccione la pestaña **Always Encrypted**.
    1. Asegúrese de que la casilla **Habilitar Always Encrypted (cifrado de columna)** **no** esté activada.
    1. Seleccione **Conectar**.
1. Abra una nueva ventana de consulta y ejecute la siguiente instrucción para habilitar ADR.

   ```sql
   ALTER DATABASE ContosoHR SET ACCELERATED_DATABASE_RECOVERY = ON;
   ```

## <a name="step-2-create-and-test-an-index-without-role-separation"></a>Paso 2: Creación y prueba de un índice sin separación de roles

En este paso, creará y probará un índice en una columna cifrada. Actuará como un usuario que asume los roles de un administrador de base de datos, que administra la base de datos, y de un propietario de datos, que tiene acceso a las claves que protegen los datos.

1. Abra una nueva instancia de SSMS y conéctese a la instancia de SQL Server **con** Always Encrypted habilitado para la conexión de base de datos.
   1. Inicie una nueva instancia de SSMS.
   1. En el cuadro de diálogo **Conectar a servidor**, especifique el nombre del servidor, seleccione un método de autenticación e indique sus credenciales.
   1. Haga clic en **Opciones >>** y seleccione la pestaña **Always Encrypted**.
   1. Active la casilla **Habilitar Always Encrypted (cifrado de columna)** y especifique la dirección URL de atestación de enclave (por ejemplo, ht<span>tp://<   span>hgs.bastion.local/Attestation).
   1. Seleccione **Conectar**.
   1. Si se le pide habilitar la parametrización para las consultas de Always Encrypted, haga clic en **Habilitar**.
1. Si no se le solicita que habilite la parametrización de Always Encrypted, compruebe que está habilitada.
   1. Seleccione **Herramientas** en el menú principal de SSMS.
   2. Seleccione **Opciones...** .
   3. Vaya a **Ejecución de consulta** > **SQL Server** > **Avanzadas**.
   4. Asegúrese de que la opción **Habilitar parametrización para Always Encrypted** esté activada.
   5. Seleccione **Aceptar**.
1. Abra una ventana de consulta y ejecute las siguientes instrucciones para cifrar la columna **LastName** en la tabla **Empleados**. En pasos posteriores, deberá crear y utilizar un índice en esa columna.

   ```sql
   USE [ContosoHR];
   GO   
   ALTER TABLE [dbo].[Employees]
   ALTER COLUMN [LastName] [nvarchar](50) COLLATE Latin1_General_BIN2 
   ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL;
   GO   
   ALTER DATABASE SCOPED CONFIGURATION CLEAR PROCEDURE_CACHE;
   GO
   ```

1. Cree un índice en la columna **LastName**. Puesto que está conectado a la base de datos con Always Encrypted habilitado, el controlador cliente dentro de SSMS proporciona de modo transparente **CEK1** (la clave de cifrado de columna que protege la columna **LastName**) al enclave, que es necesario para crear el índice.

   ```sql
   USE [ContosoHR];
   GO

   CREATE INDEX IX_LastName ON [Employees] ([LastName])
   INCLUDE ([EmployeeID], [FirstName], [SSN], [Salary]);
   GO
   ```

1. Ejecute una consulta completa en la columna **LastName** y compruebe que SQL Server usa el índice al ejecutar la consulta.
   1. En la misma ventana de consulta o en otra nueva, asegúrese de que el botón **Incluir estadísticas de consultas dinámicas** de la barra de herramientas esté activado.
   1. Ejecute la siguiente consulta.

       ```sql
       USE [ContosoHR];
       GO

       DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
       SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
       GO
      ```

   1. En la pestaña **Estadísticas de consultas dinámicas** (en la parte inferior de la ventana de consulta), observe que la consulta utiliza el índice.

## <a name="step-3-create-an-index-with-role-separation"></a>Paso 3: Creación de un índice con separación de roles

En este paso, creará un índice en una columna cifrada, que simula ser dos usuarios distintos. Un usuario es un administrador de base de datos que necesita crear un índice, pero que no tiene acceso a las claves. El otro usuario es un propietario de datos, que tiene acceso a las claves.

1. Con la instancia de SSMS **sin** Always Encrypted habilitado, ejecute la siguiente instrucción para quitar el índice de la columna **LastName**.

   ```sql
   USE [ContosoHR];
   GO

   DROP INDEX IX_LastName ON [Employees]; 
   GO
   ```

1. Actúe como propietario de datos (o una aplicación que tenga acceso a las claves) y llene la caché dentro del enclave con **CEK1**.

   > [!NOTE]
   > A menos que haya reiniciado la instancia de SQL Server después del **Paso 2: Creación y prueba de un índice sin separación de roles**, este paso es redundante ya que **CEK1** ya está presente en la caché. Lo hemos agregado para demostrar cómo un propietario de datos puede proporcionar una clave al enclave, si aún no está presente en él.

   1. En la instancia de SSMS **con** Always Encrypted habilitado, ejecute las siguientes instrucciones en una ventana de consulta. La instrucción envía todas las claves de cifrado de columna habilitadas para enclave al enclave. Consulte [sp_enclave_send_keys](../system-stored-procedures/sp-enclave-send-keys-sql.md) para obtener más información.

        ```sql
        USE [ContosoHR];
        GO

        EXEC sp_enclave_send_keys;
        GO
        ```

   1. Como alternativa a ejecutar el procedimiento almacenado anterior, puede ejecutar una consulta DML que usa el enclave en la columna **LastName**. Esta acción rellenará el enclave solo con **CEK1**.

        ```sql
        USE [ContosoHR];
        GO

        DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
        SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
        GO
        ```

1. Actúe como un administrador de base de datos y cree el índice.
    1. En la instancia de SSMS **sin** Always Encrypted habilitado, ejecute las siguientes instrucciones en una ventana de consulta.

        ```sql
        USE [ContosoHR];
        GO

        CREATE INDEX IX_LastName ON [Employees] ([LastName])
        INCLUDE ([EmployeeID], [FirstName], [SSN], [Salary]);
        GO
        ```

1. Como propietario de datos, ejecute una consulta completa en la columna **LastName** y compruebe que SQL Server usa el índice al ejecutarla.
   1. En la instancia de SSMS **con** Always Encrypted habilitado, seleccione una ventana de consulta existente o abra una nueva ventana de consulta y asegúrese de que el botón **Incluir estadísticas de consultas dinámicas** de la barra de herramientas esté activado.
   1. Ejecute la siguiente consulta. 

        ```sql
        USE [ContosoHR];
        GO

        DECLARE @LastNamePrefix NVARCHAR(50) = 'Aber%';
        SELECT * FROM [dbo].[Employees] WHERE [LastName] LIKE @LastNamePrefix;
        GO
        ```

   1. En **Estadísticas de consultas dinámicas** (en la parte inferior de la ventana de consulta), observe que la consulta utiliza el índice.

## <a name="next-steps"></a>Pasos siguientes

- Consulte [Configuración de Always Encrypted con enclaves seguros](encryption/configure-always-encrypted-enclaves.md) para más información sobre otros casos de uso de Always Encrypted con enclaves seguros.
