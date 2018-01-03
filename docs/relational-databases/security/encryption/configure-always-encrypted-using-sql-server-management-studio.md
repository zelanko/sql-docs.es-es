---
title: Configurar Always Encrypted con SQL Server Management Studio | Microsoft Docs
ms.custom: 
ms.date: 11/30/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: security
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.SWB.COLUMNMASTERKEY.PAGE.F1
- SQL13.SWB.COLUMNENCRYPTIONKEY.PAGE.F1
- SQL13.SWB.COLUMNMASTERKEY.ROTATION.F1
helpviewer_keywords: Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
caps.latest.revision: "15"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7a6e6764d71d632cb4f232eecd34e16f38bede57
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="configure-always-encrypted-using-sql-server-management-studio"></a>Configure Always Encrypted using SQL Server Management Studio (Configurar Always Encrypted con SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

En este artículo se describen las tareas para configurar Always Encrypted y administrar las bases de datos que usan Always Encrypted con [SQL Server Management Studio (SSMS)](../../../ssms/download-sql-server-management-studio-ssms.md).

Cuando se usa SSMS para configurar Always Encrypted, SSMS controla las claves y la información confidencial de Always Encrypted, por lo que dichas claves e información aparecen como texto no cifrado en el proceso de SSMS. Por esta razón, es importante que ejecute SSMS en un equipo seguro. Si la base de datos está hospedada en SQL Server, asegúrese de que SSMS se ejecuta en un equipo diferente del que hospeda la instancia de SQL Server. Dado que el objetivo principal de Always Encrypted es garantizar la seguridad de la información confidencial cifrada, incluso si el sistema de base de datos está en peligro, la ejecución de un script de PowerShell que procese las claves o la información confidencial en el equipo de SQL Server puede reducir o anular las ventajas de la característica. Para obtener más recomendaciones, vea [Security Considerations for Key Management](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#SecurityForKeyManagement)(Consideraciones de seguridad para la administración de claves).

SSMS no admite la separación de roles entre los administradores de la base de datos (DBA) y los administradores de secretos criptográficos que tienen acceso a datos de texto no cifrado (administradores de seguridad o administradores de la aplicación). Si la organización exige la separación de roles, debe usar PowerShell para configurar Always Encrypted. Para obtener más información, vea [Overview of Key Management for Always Encrypted (Información general de administración de claves de Always Encrypted)](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) y [Configure Always Encrypted using PowerShell (Configurar Always Encrypted con PowerShell)](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md).

## <a name="configuring-always-encrypted-using-the-always-encrypted-wizard"></a>Configurar Always Encrypted con el Asistente para Always Encrypted

El [Asistente para Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-wizard.md) es una herramienta eficaz que permite establecer la configuración de cifrado elegida para las columnas de la base de datos seleccionadas. Según la configuración actual de Always Encrypted y la configuración de destino elegida, el asistente puede cifrar una columna, descifrarla (quitar el cifrado) o volver a cifrarla (por ejemplo, con una nueva clave de cifrado de columnas o con un tipo de cifrado diferente del actual configurado para la columna). Es posible configurar varias columnas en una misma ejecución del asistente.

Si no ha aprovisionado claves para Always Encrypted, el asistente las generará automáticamente. Basta con que seleccione un almacén de claves para la clave maestra de columna: el Almacén de certificados de Windows o el Almacén de claves de Azure. El asistente generará automáticamente los nombres de las claves y sus objetos de metadatos en la base de datos. Si necesita más control sobre la manera en que se aprovisionan las claves (y más opciones para un almacén de claves que contenga una clave maestra de columna), puede usar los cuadros de diálogo **Nueva clave maestra de columna** y **Nueva clave de cifrado de columnas** (descritos a continuación) para aprovisionar claves antes de iniciar el asistente. Después puede elegir la clave de cifrado de columnas existente en el Asistente para Always Encrypted.

Para obtener más información sobre cómo usar el asistente, vea  [Asistente para Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-wizard.md).

## <a name="querying-encrypted-columns"></a>Consultar columnas cifradas

Esta sección describe cómo:   
-   Recuperar los valores de texto cifrado almacenados en columnas cifradas.   
-   Recuperar los valores de texto no cifrado almacenados en columnas cifradas.   
-   Enviar valores de texto no cifrado con columnas cifradas como destino (por ejemplo, en instrucciones `INSERT` o `UPDATE` y como parámetros de búsqueda de las cláusulas `WHERE` en las instrucciones `SELECT` ).   

### <a name="retrieving-ciphertext-values-stored-in-encrypted-columns"></a>Recuperación de los valores de texto cifrado almacenados en columnas cifradas    

Para recuperar valores desde una columna cifrada como texto cifrado (sin descifrar los valores):
1.  Asegúrese de que Always Encrypted esté deshabilitado para la conexión de base de datos de la ventana del Editor de consultas, desde donde ejecuta la consulta `SELECT` . Consulte [Habilitación y deshabilitación de Always Encrypted para una conexión de base de datos](#en-dis) que aparece más adelante.      
2.  Ejecute una consulta `SELECT` . Todos los datos que se recuperen de las columnas cifradas se devolverán como valores binarios (cifrados).   

*Ejemplo*   
Suponiendo que `SSN` es una columna cifrada de la tabla `Patients` , la consulta que aparece a continuación recuperará los valores binarios de texto cifrado, si Always Encrypted está deshabilitado para la conexión de base de datos.   

![always-encrypted-ciphertext](../../../relational-databases/security/encryption/media/always-encrypted-ciphertext.png)
 
### <a name="retrieving-plaintext-values-stored-in-encrypted-columns"></a>Recuperación de los valores de texto no cifrado almacenados en columnas cifradas    

Para recuperar valores desde una columna cifrada como texto no cifrado (para descifrar los valores):   
1.  Asegúrese de que Always Encrypted esté habilitado para la conexión de base de datos de la ventana del Editor de consultas, desde donde ejecuta la consulta `SELECT` . Esto indicará al proveedor de datos .NET Framework para SQL Server (que SSMS usa) que descifre los datos recuperados de las columnas cifradas. Consulte [Habilitación y deshabilitación de Always Encrypted para una conexión de base de datos](#en-dis) que aparece más adelante.
2.  Asegúrese de que puede tener acceso a todas las claves maestras de columna configuradas para las columnas cifradas. Por ejemplo, si la clave maestra de columna es un certificado, debe asegurarse de que este esté implementado en la máquina en la que se ejecuta SSMS. O bien, si la clave maestra de columna es una clave almacenada en Azure Key Vault, debe asegurarse de tener los permisos para obtener acceso a la clave (además, es posible que se le pida iniciar sesión en Azure).
3.  Ejecute una consulta `SELECT` . Los datos que se recuperen de las columnas cifradas se devolverán como texto no cifrado como valores de los tipos de datos originales.   

*Ejemplo*   
Suponiendo que SSN es una columna `char(11)` cifrada de la tabla `Patients` , la columna que se muestra a continuación devolverá valores de texto no cifrado si Always Encrypted está habilitado para la conexión de base de datos y si tiene acceso a la clave maestra de columna configurada para la columna `SSN` .   

![always-encrypted-plaintext](../../../relational-databases/security/encryption/media/always-encrypted-plaintext.png)
 
### <a name="sending-plaintext-values-targeting-encrypted-columns"></a>Envío de valores de texto no cifrado con columnas cifradas como destino       

Para ejecutar una consulta que envía un valor con una columna cifrada como destino, por ejemplo, una consulta que inserta o actualiza un valor almacenado, o filtra según él, en una columna cifrada, haga lo siguiente:   
1.  Asegúrese de que Always Encrypted esté habilitado para la conexión de base de datos de la ventana del Editor de consultas, desde donde ejecuta la consulta `SELECT` . Esto indicará al proveedor de datos .NET Framework para SQL Server (que SSMS usa) que cifre las variables Transact-SQL parametrizadas (ver a continuación) con columnas cifradas como destino. Consulte [Habilitación y deshabilitación de Always Encrypted para una conexión de base de datos](#en-dis) que aparece más adelante.   
2.  Asegúrese de que puede tener acceso a todas las claves maestras de columna configuradas para las columnas cifradas. Por ejemplo, si la clave maestra de columna es un certificado, debe asegurarse de que este esté implementado en la máquina en la que se ejecuta SSMS. O bien, si la clave maestra de columna es una clave almacenada en Azure Key Vault, debe asegurarse de tener los permisos para obtener acceso a la clave (además, es posible que se le pida iniciar sesión en Azure).   
3.  Asegúrese de que la parametrización de Always Encrypted esté habilitada para la ventana del Editor de consultas. (Requiere al menos la versión 17.0 de SSMS) Declare una variable Transact-SQL e inicialícela con un valor que desea enviar (insertar, actualizar o según el cual filtrar) a la base de datos. Consulte [Parametrización de Always Encrypted](#param) que aparece más adelante para detalles.   
    >   [!NOTE]
    >   Como Always Encrypted admite un subconjunto limitado de conversiones de tipo, en muchos casos se requiere que ese tipo de datos de una variable Transact-SQL sea el mismo tipo de la columna de base de datos de destino.   
4.  Ejecute la consulta; para ello, envíe el valor de la variable Transact-SQL a la base de datos. SSMS convertirá la variable en un parámetro de consulta y cifrará su valor antes de enviarlo a la base de datos.   

*Ejemplo*   
Suponiendo que `SSN` es una columna `char(11)` cifrada de la tabla `Patients` , el script a continuación intentará encontrar una fila que contenga `'795-73-9838'` en la columna SSN y devolverá el valor de la columna `LastName` , siempre que Always Encrypted esté habilitado para la conexión de base de datos, que Parametrización para Always Encrypted esté habilitado para la ventana del Editor de consultas y que usted tenga acceso a la clave maestra de columna configurada para la columna `SSN` .   

![always-encrypted-patients](../../../relational-databases/security/encryption/media/always-encrypted-patients.png)
 
### <a name="en-dis"></a> Habilitación y deshabilitación de Always Encrypted para una conexión de base de datos   

Habilitar Always Encrypted para una conexión de base de datos indica al proveedor de datos .NET Framework para SQL Server, que SQL Server Management Studio usa, que intente realizar lo siguiente de manera transparente:   
-   Descifrar los valores que se recuperan de las columnas cifradas y se devuelven en los resultados de la consulta.   
-   Cifrar los valores de las variables Transact-SQL parametrizadas que tienen como destino las columnas de base de datos cifradas.   
Para habilitar Always Encrypted para una conexión de base de datos, especifique `Column Encryption Setting=Enabled` en la pestaña **Propiedades adicionales** del cuadro de diálogo **Conectar con el servidor** .    
Para deshabilitar Always Encrypted para una conexión de base de datos, especifique `Column Encryption Setting=Disabled` o simplemente quite el valor en **Valor de cifrado de columnas** en la pestaña **Propiedades adicionales** del cuadro de diálogo **Conectar con el servidor** (su valor predeterminado es **Deshabilitado**).   

>  [!TIP] 
>  Para alternar entre Always Encrypted habilitado y deshabilitado para una ventana existente del Editor de consultas, haga lo siguiente:   
>  1.   Haga clic con el botón derecho en cualquier parte de la ventana del Editor de consultas.
>  2.   Seleccione **Conexión** > **Cambiar conexión...** 
>  3.   Haga clic en **Opciones** >>
>  4.   Seleccione la pestaña **Propiedades adicionales** y escriba `Column Encryption Setting=Enabled` (para habilitar el comportamiento de Always Encrypted) o quite el valor (para deshabilitar el comportamiento de Always Encrypted).   
>  5.   Haga clic en **Conectar**.   
   
### <a name="param"></a>Parametrización de Always Encrypted   
 
Parametrización de Always Encrypted es una característica de SQL Server Management Studio que convierte automáticamente las variables Transact-SQL en parámetros de consulta (instancias de [SqlParameter Class](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx)). (Requiere al menos la versión 17.0 de SSMS) Esto permite que el proveedor de datos .NET Framework para SQL Server subyacente detecte datos con columnas cifradas como destino y cifre dichos datos antes de enviarlos a la base de datos. 
  
Sin la parametrización, el proveedor de datos .NET Framework pasa cada instrucción que usted crea en el Editor de consultas como una consulta no parametrizada. Si la consulta contiene literales o variables Transact-SQL con columnas cifradas como destino, el proveedor de datos .NET Framework para SQL Server no podrá detectarlas ni cifrarlas antes de enviar la consulta a la base de datos. Como resultado, la consulta presentará un error debido a un error de coincidencia de tipos (entre la variable Transact-SQL literal de texto no cifrado y la columna cifrada). Por ejemplo, la consulta siguiente presentará un error sin parametrización, suponiendo que la columna `SSN` está cifrada.   

```sql
DECLARE @SSN NCHAR(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN
```

#### <a name="enablingdisabling-parameterization-for-always-encrypted"></a>Habilitación/deshabilitación de parametrización de Always Encrypted   


Parametrización de Always Encrypted está deshabilitada de manera predeterminada.    

Para habilitar/deshabilitar parametrización de Always Encrypted para la ventana actual del Editor de consultas, haga lo siguiente:   
1.  Seleccione **Consulta** en el menú principal.   
2.  Seleccione **Opciones de consulta…**.   
3.  Vaya a **Ejecución** > **Avanzadas**.   
4.  Seleccione o anule la selección de **Habilitar parametrización de Always Encrypted**.   
5.  Haga clic en **Aceptar**.   

Para habilitar/deshabilitar parametrización de Always Encrypted para ventanas futuras del Editor de consultas, haga lo siguiente:   
1.  Seleccione **Herramientas** en el menú principal.   
2.  Seleccione **Opciones…**.   
3.  Vaya a **Ejecución de consulta** > **SQL Server** > **Avanzadas**.   
4.  Seleccione o anule la selección de **Habilitar parametrización de Always Encrypted**.   
5.  Haga clic en **Aceptar**.   

Si ejecuta una consulta en una ventana del Editor de consultas que usa una conexión de base de datos con Always Encrypted habilitado, pero la parametrización no está habilitada para la ventana del Editor de consultas, se le pedirá que la habilite.   
>   [!NOTE]   
>   Parametrización de Always Encrypted funcione solo en ventanas del Editor de consultas que usan conexiones de base de datos con Always Encrypted habilitadas (consulte [Habilitación y deshabilitación de Always Encrypted para una conexión de base de datos](#en-dis)). Ninguna variable Transact-SQL será parametrizada si la ventana del Editor de consultas usa una conexión de base de datos sin tener habilitado Always Encrypted.   

#### <a name="how-parameterization-for-always-encrypted-works"></a>Funcionamiento de parametrización de Always Encrypted   

Si la parametrización para Always Encrypted y el comportamiento de Always Encrypted en la conexión de base de datos están habilitados para una ventana del Editor de consultas, SQL Server Management Studio intentará parametrizar las variables Transact-SQL que cumplen con las condiciones de requisitos previos siguientes:    
- Se declaran e inicializan en la misma instrucción (inicialización alineada). Las variables declaradas que usan instrucciones `SET` independientes no se parametrizarán.   
- Se inicializan con un solo literal. Las variables que se inicializan con expresiones que incluyen cualquier operador o función no se parametrizarán.      

A continuación, aparecen ejemplos de variables que SQL Server Management Studio parametrizará.   
```sql
DECLARE @SSN char(11) = '795-73-9838';
   
DECLARE @BirthDate date = '19990104';
DECLARE @Salary money = $30000;
```

Y, a continuación, algunos ejemplos de variables que SQL Server Management Studio no intentará parametrizar:   
```sql
DECLARE @Name nvarchar(50); --Initialization seperate from declaration
SET @Name = 'Abel';
   
DECLARE @StartDate date = GETDATE(); -- a function used instead of a literal
   
DECLARE @NewSalary money = @Salary * 1.1; -- an expression used instead of a literal
```
 
Para que un intento de parametrización se realice correctamente:   
- El tipo de literal que se use para la inicialización de la variable que se parametrizará debe coincidir con el tipo de la declaración de variable.   
- Si el tipo declarado de la variable es un tipo de fecha o un tipo de hora, la variable se debe inicializar con una cadena usando uno de los siguientes formatos compatibles con ISO 8601.   

Estos son ejemplos de declaraciones de variable Transact-SQL que generarán errores de parametrización:   
```sql
DECLARE @BirthDate date = '01/04/1999' -- unsupported date format   
   
DECLARE @Number int = 1.1 -- the type of the literal does not match the type of the variable   
```
SQL Server Management Studio usa IntelliSense para informarle las variables que se pueden parametrizar correctamente y cuáles son los intentos de parametrización que presentan error (y por qué).   

Una declaración de una variable que se puede parametrizar correctamente está marcada con un carácter de subrayado de advertencia en el Editor de consultas. Si mantiene el puntero sobre una instrucción de declaración que se marcó con un carácter de subrayado de advertencia, verá los resultados del proceso de parametrización, incluidos los valores de las propiedades clave del objeto [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) resultante (al que se asigna la variable): [SqlDbType](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqldbtype.aspx), [Size](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.size.aspx), [Precision](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.precision.aspx), [Scale](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.scale.aspx), [SqlValue](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.sqlvalue.aspx). También puede ver la lista completa de todas las variables que se parametrizaron correctamente en la pestaña **Advertencia** de la vista **Lista de errores** . Para abrir la vista **Lista de errores** , seleccione **Vista** en el menú principal y, luego, seleccione **Lista de errores**.    

Si SQL Server Management Studio intentó parametrizar una variable, pero la parametrización presentó un error, la declaración de la variable se marcará con un carácter de subrayado de error. Si mantiene el puntero sobre una instrucción de declaración que se marcó con un carácter de subrayado de error, recibirá los resultados del error. También podrá ver la lista completa de errores de parametrización de todas las variables en la pestaña **Error** de la vista **Lista de errores** . Para abrir la vista **Lista de errores** , seleccione **Vista** en el menú principal y, luego, seleccione **Lista de errores**.   

La captura de pantalla siguiente muestra un ejemplo de 6 declaraciones de variable. SQL Server Management Studio parametrizó correctamente las 3 primeras variables. Las últimas 3 variables no cumplieron con las condiciones requeridas para la parametrización y, por tanto, SQL Server Management Studio no intentó parametrizarlas (sus declaraciones no están marcadas de ninguna manera).   

![always-encrypted-parameter-warnings](../../../relational-databases/security/encryption/media/always-encrypted-parameter-warnings.png)
 
Otro ejemplo que aparece a continuación muestra 2 variables que cumplen con las condiciones requeridas para la parametrización, pero el intento de parametrización presenta un error porque las variables se inicializaron de manera incorrecta.    
 
![always-encrypted-error](../../../relational-databases/security/encryption/media/always-encrypted-error.png)
 
>   [!NOTE]
>   Como Always Encrypted admite un subconjunto limitado de conversiones de tipo, en muchos casos se requiere que ese tipo de datos de una variable Transact-SQL sea el mismo tipo de la columna de base de datos de destino. Por ejemplo, suponiendo que el tipo de la columna `SSN` de la tabla `Patients` sea `char(11)`, la consulta siguiente presentará un error, debido a que el tipo de la variable `@SSN` , que es `nchar(11)`, no coincide con el tipo de la columna.   

```sql
DECLARE @SSN nchar(11) = '795-73-9838'
SELECT * FROM [dbo].[Patients]
WHERE [SSN] = @SSN;
```

    Msg 402, Level 16, State 2, Line 5   
    The data types char(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') collation_name = 'Latin1_General_BIN2' 
    and nchar(11) encrypted with (encryption_type = 'DETERMINISTIC', 
    encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', 
    column_encryption_key_database_name = 'Clinic') are incompatible in the equal to operator.

>   [!NOTE]
>   Sin parametrización, la columna completa, incluidas las conversiones de tipo, se procesan dentro de SQL Server/Azure SQL Database. Con la parametrización habilitada, .NET Framework ejecuta algunas conversiones de tipo dentro de SQL Server Management Studio. Debido a las diferencias entre el sistema de tipo de .NET Framework y el sistema de tipo de SQL Server (por ejemplo, una precisión distinta de algunos tipos, como float), una consulta que se ejecuta con parametrización habilitada puede generar resultados distintos a los de la consulta ejecutada sin la parametrización habilitada. 

#### <a name="permissions"></a>Permisos      

Para ejecutar cualquier consulta contra las columnas cifradas, incluidas las consultas que recuperan datos en texto cifrado, necesita los permisos `VIEW ANY COLUMN MASTER KEY DEFINITION` y `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` pen la base de datos.   
Además de los permisos anteriores, para descifrar cualquier resultado de consulta o para cifrar cualquier parámetro de consulta (generados por la parametrización de las variables Transact-SQL), también debe tener acceso a la clave maestra de columna que protege las columnas de destino:   
- **Almacén de certificados: equipo local** : debe tener acceso de `Read` al certificado que se usa en una clave maestra de columna o puede ser el administrador del equipo.   
- **Azure Key Vault** : necesita los permisos de `get`, `unwrapKey`y comprobación en el almacén que contiene la clave maestra de columna.   
- **Proveedor del almacén de claves (CNG)** : el permiso y las credenciales requeridos que se le podrían solicitar al usar una clave o un almacén de claves dependen de la configuración del almacén o del proveedor de almacenamiento de claves (KSP).   
- **Proveedor de servicios criptográficos (CAPI)** : el permiso y las credenciales que se le podrían solicitar al usar una clave o un almacén de claves dependen del almacén y de la configuración del proveedor de servicios criptográficos (CSP).   

Para obtener más información, vea [Create and Store Column Master Keys (Always Encrypted) (Crear y almacenar claves maestras de columna (Always Encrypted))](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).


<a name="provisioncmk"></a>
## <a name="provisioning-column-master-keys-new-column-master-key"></a>Aprovisionamiento de claves maestras de columna (nueva clave maestra de columna)

El cuadro de diálogo **Nueva clave maestra de columna** permite generar una clave maestra de columna o elegir una clave existente en un almacén de claves y crear metadatos de clave maestra de columna para la clave creada o seleccionada en la base de datos.

1.  En el **Explorador de objetos**, vaya a la carpeta **Security > Always Encrypted Keys** de la base de datos.
2.  Haga clic con el botón derecho en la carpeta **Column Master Keys** y seleccione **Nueva clave maestra de columna…**. 
3.  En el cuadro de diálogo **Nueva clave maestra de columna** , escriba el nombre del objeto de metadatos de la clave maestra de columna.
4.  Seleccione un almacén de claves:
    - **Almacén de certificados, usuario actual** : indica la ubicación del almacén de certificados del usuario actual en el Almacén de certificados de Windows, que es el almacén personal. 
    - **Almacén de certificados, equipo local** : indica la ubicación del almacén de certificados del equipo local en el Almacén de certificados de Windows. 
    - **Almacén de claves de Azure** : deberá iniciar sesión en Azure (haga clic en **Iniciar sesión**). Una vez que haya iniciado sesión, podrá elegir una de las suscripciones de Azure y un almacén de claves.
    - **Proveedor de almacén de claves (CNG)** : indica un almacén de claves accesible a través de un proveedor de almacén de claves (KSP) que implementa la API Cryptography Next Generation (CNG). Normalmente, este tipo de almacén es un módulo de seguridad de hardware (HSM). Después de seleccionar esta opción, debe elegir un KSP. De forma predeterminada está seleccionado el**proveedor de almacén de claves de software de Microsoft** . Si quiere usar una clave maestra de columna almacenada en un HSM, seleccione un KSP para el dispositivo (debe estar instalado y configurado en el equipo antes de que abra el cuadro de diálogo).
    -   **Proveedor de servicios criptográficos (CAPI)** : almacén de claves accesible a través de un proveedor de servicios criptográficos (CSP) que implementa Cryptography API (CAPI). Normalmente, este almacén es un módulo de seguridad de hardware (HSM). Después de seleccionar esta opción, debe elegir un CSP.  Si quiere usar una clave maestra de columna almacenada en un HSM, seleccione un CSP para el dispositivo (debe estar instalado y configurado en el equipo antes de que abra el cuadro de diálogo).
    
    >   [!NOTE]
    >   Dado que CAPI es una API en desuso, la opción Proveedor de servicios criptográficos (CAPI) está deshabilitada de forma predeterminada. Puede habilitarla creando el valor DWORD CAPI Provider Enabled en la clave **[HKEY_CURRENT_USER\Software\Microsoft\Microsoft SQL Server\sql13\Tools\Client\Always Encrypted]** del Registro de Windows y estableciéndolo en 1. Debe usar CNG en lugar de CAPI, a menos que el almacén de claves no admita CNG.
   
    Para obtener más información sobre los anteriores almacenes de claves, vea [Create and Store Column Master Keys (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)(Crear y almacenar claves maestras de columna (Always Encrypted)).

5.  Elija una clave existente en el almacén de claves, o bien haga clic en el botón **Generar clave** o **Generar certificado** para crear una clave en el almacén de claves. 
6.  Haga clic en **Aceptar** y la nueva clave aparecerá en la lista. 

SQL Server Management Studio creará los metadatos para la clave maestra de columna en la base de datos. El cuadro de diálogo consigue esto generando y emitiendo una instrucción [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) .


<a name="provisioncek"></a> 
## <a name="provisioning-column-encryption-keys-new-column-encryption-key"></a>Aprovisionamiento de claves de cifrado de columnas (nueva clave de cifrado de columnas)

El cuadro de diálogo **Nueva clave de cifrado de columnas** permite generar una clave de cifrado de columnas, cifrarla con una clave maestra de columna y crear los metadatos de clave de cifrado de columnas en la base de datos.

1.  En el **Explorador de objetos**, vaya a la carpeta **Security &gt; Always Encrypted Keys** de la base de datos.
2.  Haga clic con el botón derecho en la carpeta **Column Encryption Keys** y seleccione **Nueva clave de cifrado de columnas…**. 
3.  En el cuadro de diálogo **Nueva clave de cifrado de columnas** , escriba el nombre del objeto de metadatos de la clave de cifrado de columnas.
4.  Seleccione un objeto de metadatos que represente la clave maestra de columna de la base de datos.
5.  Haga clic en **Aceptar**. 


SQL Server Management Studio generará una clave de cifrado de columnas y luego recuperará los metadatos para la clave maestra de columna seleccionada en la base de datos. Después, SQL Server Management Studio usará los metadatos de la clave maestra de columna para ponerse en contacto con el almacén de claves que contiene la clave maestra de columna y cifrar la clave de cifrado de columnas. Por último, se crearán en la base de datos los metadatos de la nueva clave de cifrado de columnas. El cuadro de diálogo consigue esto generando y emitiendo una instrucción [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) .

### <a name="permissions"></a>Permisos

Necesita tener los permisos de base de datos *ALTER ANY ENCRYPTION MASTER KEY* y *VIEW ANY COLUMN MASTER KEY DEFINITION* en la base de datos para que el cuadro de diálogo cree los metadatos de la clave de cifrado de columnas y tenga acceso a los metadatos de la clave maestra de columna.
Para tener acceso a un almacén de claves y usar la clave maestra de columna, es posible que necesite permisos en el almacén de claves o en la clave:
- **Almacén de certificados, equipo local** : debe tener acceso de lectura al certificado que se usa como una clave maestra de columna o ser el administrador del equipo.
- **Almacén de claves de Azure** : necesita los permisos *get*, *unwrapKey*, *wrapKey*, *sign*y *verify*  en el almacén que contiene la clave maestra de columna.
- **Proveedor de almacén de claves (CNG)** : se le podrían solicitar el permiso y las credenciales al usar una clave o un almacén de claves, en función del almacén y de la configuración del KSP.
- **Proveedor de servicios criptográficos (CAPI)** : se le podrían solicitar el permiso y las credenciales al usar una clave o un almacén de claves, en función del almacén y de la configuración del CSP.

Para obtener más información, vea [Create and Store Column Master Keys (Always Encrypted) (Crear y almacenar claves maestras de columna (Always Encrypted))](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

<a name="rotatecmk"></a>
## <a name="rotating-column-master-keys"></a>Rotación de claves maestras de columna

La rotación de una clave maestra de columna es el proceso por el cual se reemplaza una clave maestra de columna existente por otra nueva. Puede que necesite rotar una clave si está en peligro o para cumplir con las directivas o los reglamentos de la organización que exigen que las claves de cifrado roten de forma regular. La rotación de claves maestras de columna implica descifrar las claves de cifrado de columnas que están protegidas con la clave maestra de columna actual, volver a cifrarlas con la nueva clave maestra de columna y actualizar los metadatos de clave. Para obtener más información, vea [Overview of Key Management for Always Encrypted (Información general de administración de claves de Always Encrypted)](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md).

**Paso 1: aprovisionamiento de una nueva clave maestra de columna**

Aprovisione una nueva clave maestra de columna siguiendo los pasos descritos en la anterior sección Aprovisionamiento de claves maestras de columna.

**Paso 2: cifrado de las claves de cifrado de columna con la nueva clave maestra de columna**

Por lo general, una clave maestra de columna protege una o más claves de cifrado de columnas. Cada clave de cifrado de columnas tiene un valor cifrado, almacenado en la base de datos, que es el resultado de haber cifrado la clave de cifrado de columnas con la clave maestra de columna.
En este paso, cifrará cada una de las claves de cifrado de columnas (protegidas con la clave maestra de columna) que va a rotar con la nueva clave maestra de columna y almacenará el nuevo valor cifrado en la base de datos. Como resultado, cada clave de cifrado de columnas afectada por la rotación tendrá dos valores cifrados: uno cifrado con la clave maestra de columna antigua y otro reciente, cifrado con la nueva.

1.  En el **Explorador de objetos**, vaya a la carpeta **Security > Always Encrypted Keys > Column Master Keys** y encuentre la clave maestra de columna que va a rotar.
2.  Haga clic con el botón derecho en ella y seleccione **Rotar**.
3.  En el cuadro de diálogo **Rotación de clave maestra de columna** , seleccione el nombre de la nueva clave maestra de columna que creó en el paso 1 en el campo **Destino** .
4.  Revise la lista de claves de cifrado de columna, protegidas por las claves maestras de columna existentes. Estas claves se verán afectadas por la rotación.
5.  Haga clic en **Aceptar**.

SQL Server Management Studio obtendrá los metadatos de las claves de cifrado de columnas que están protegidas con la clave maestra de columna antigua y los metadatos de las claves maestras de columna antigua y nueva. Después, SSMS usará los metadatos de la clave maestra de columna para tener acceso al almacén de claves que contiene la clave maestra de columna antigua y descifrar las claves de cifrado de columnas. Posteriormente, SSMS obtendrá acceso al almacén de claves que contiene la nueva clave maestra de columna para generar un conjunto de valores cifrados de las claves de cifrado de columnas y, después, agregará los valores nuevos a los metadatos, para lo que generará y emitirá instrucciones [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) .

> [!NOTE]
> Asegúrese de que ninguna de las claves de cifrado de columnas, cifradas con la clave maestra de columna antigua, esté cifrada con otra clave maestra de columna. Dicho de otro modo, cada clave cifrada de columna afectada por la rotación debe tener exactamente un valor cifrado en la base de datos. Si alguna de las claves de cifrado de columnas afectadas tiene más de un valor cifrado, tendrá que quitarlo para poder continuar con la rotación (consulte el *paso 4* , en el que se explica cómo quitar un valor cifrado de una clave de cifrado de columna).

**Paso 3: configuración de sus aplicaciones con la nueva clave maestra de columna**

En este paso, debe garantizar que todas sus aplicaciones cliente que realicen consultas a las columnas de la base de datos protegidas con la clave maestra de columna y que vaya a rotar puedan acceder a la nueva clave maestra de columna (es decir, las columnas de la base de datos cifradas con una clave de cifrado de columnas que, a su vez, está cifrada con la clave maestra de columna, la cual se va a rotar). Este paso depende del tipo de almacén de claves en el que se encuentre la nueva clave maestra de columna. Por ejemplo:
- Si la nueva clave maestra de columna es un certificado guardado en el Almacén de certificados de Windows, tendrá que implementarlo en la misma ubicación del almacén de certificados (*Usuario actual* o *Equipo local*) que la especificada en la ruta de acceso de la clave de su clave maestra de columna en la base de datos. La aplicación debe poder acceder al certificado:
    - Si el certificado se guarda en la ubicación del almacén de certificados *Usuario actual* , se tendrá que importar en el almacén Usuario actual de la identidad de Windows (el usuario) de la aplicación.
    - En cambio, si el certificado se guarda en la ubicación del almacén de certificados *Equipo local* , la identidad de Windows de la aplicación deberá tener permiso para tener acceso al certificado.
- Si la nueva clave maestra de columna se guarda en el Almacén de claves de Microsoft Azure, la aplicación se debe implementar de forma que se pueda autenticar en Azure y tenga permiso para obtener acceso a la clave.

Para obtener más información, vea [Create and Store Column Master Keys (Always Encrypted) (Crear y almacenar claves maestras de columna (Always Encrypted))](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

> [!NOTE]
> En este momento de la rotación, tanto la clave maestra de columna antigua como la nueva son válidas y se pueden usar para obtener acceso a los datos.

**Paso 4: limpieza de los valores de clave de cifrado de columna cifrados con la clave maestra de columna antigua**

Una vez que haya configurado todas las aplicaciones para que usen la nueva clave maestra de columna, quite de la base de datos los valores de las claves de cifrado de columnas que estén cifradas con la clave maestra de columna *antigua* . Al quitar los valores antiguos, garantizará que está preparado para la siguiente rotación (recuerde que cada clave de cifrado de columnas protegida con una clave maestra de columna que se vaya a rotar debe tener exactamente un único valor cifrado).

Existe otro motivo para limpiar el valor antiguo antes de archivar o quitar la clave maestra de columna antigua, y está relacionado con el rendimiento: al realizar una consulta en una columna cifrada, es posible que un controlador cliente habilitado para Always Encrypted intente descifrar dos valores (el antiguo y el nuevo). El controlador no sabe cuál de las dos claves maestras de columna es válida en el entorno de la aplicación, por lo que recuperará los dos valores cifrados del servidor. Si no se puede descifrar uno de los valores, porque está protegido con la clave maestra de columna que no está disponible (por ejemplo, se trata de la clave maestra de columna que se ha quitado del almacén), el controlador tratará de descifrar otro valor con la clave nueva.

> [!WARNING]
> Si quita el valor de una clave de cifrado de columnas antes de que su clave maestra de columna correspondiente se haya puesto a disposición de una aplicación, esta última no podrá descifrar la columna de la base de datos.

1.  En el **Explorador de objetos**, vaya a la carpeta **Security > Always Encrypted Keys** y encuentre la clave maestra de columna existente que quiere reemplazar.
2.  Haga clic con el botón derecho en la clave maestra de columna existente y seleccione **Limpieza**.
3.  Revise la lista de valores de claves de cifrado de columna que se van a quitar.
4.  Haga clic en **Aceptar**.

SQL Server Management Studio emitirá instrucciones [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md) para quitar los valores cifrados de las claves de cifrado de columnas que están cifradas con la clave maestra de columna antigua.

**Paso 5: eliminación de metadatos de la clave maestra de columna antigua**

Si decide quitar la definición de la clave maestra de columna antigua de la base de datos, siga los pasos que se indican a continuación. 
1.  En el **Explorador de objetos**, vaya a la carpeta **Seguridad > Siempre claves cifradas > Claves maestras de columna** y encuentre la clave maestra de columna antigua que quiere quitar de la base de datos.
2.  Haga clic con el botón derecho en la clave maestra de columna antigua y seleccione **Eliminar**. De este modo, se generará y emitirá una instrucción [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md) para quitar los metadatos de la clave maestra de columna.
3.  Haga clic en **Aceptar**.

> [!NOTE]
> Es muy recomendable no eliminar permanentemente la antigua clave maestra de columna después de la rotación. Debería conservarla en su almacén de claves actual o archivarla en otra ubicación segura. Si restaura la base de datos desde un archivo de copia de seguridad a un punto en el tiempo anterior a la configuración de la nueva clave maestra de columna, necesitará la clave antigua para tener acceso a los datos.

### <a name="permissions"></a>Permisos

La rotación de una clave maestra de columna requiere los siguientes permisos de base de datos:

- **ALTER ANY COLUMN MASTER KEY** : es necesario para crear los metadatos de la nueva clave maestra de columna y eliminar los metadatos de la clave maestra de columna antigua.
- **ALTER ANY COLUMN ENCRYPTION KEY** : es necesario para modificar los metadatos de la clave de cifrado de columnas (agregar nuevos valores cifrados).
- **VIEW ANY COLUMN MASTER KEY DEFINITION** : es necesario para tener acceso a los metadatos de las claves maestras de columna y poder leerlos.
- **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** : es necesario para tener acceso a los metadatos de las claves de cifrado de columnas y poder leerlos. 

También debe tener acceso a las claves maestras de columna antigua y nueva en sus almacenes de claves. Para tener acceso a un almacén de claves y usar una clave maestra de columna, es posible que necesite permisos en el almacén de claves o en la clave:
- **Almacén de certificados, equipo local** : debe tener acceso de lectura al certificado que se usa como clave maestra de columna o ser el administrador del equipo.
- **Almacén de claves de Azure** : necesita los permisos *create*, *get*, *unwrapKey*, *wrapKey*, *sign*y *verify* en el almacén que contiene las claves maestras de columna.
- **Proveedor de almacén de claves (CNG)** : se le podrían solicitar el permiso y las credenciales al usar una clave o un almacén de claves, en función del almacén y de la configuración del KSP.
- **Proveedor de servicios criptográficos (CAPI)** : se le podrían solicitar el permiso y las credenciales al usar una clave o un almacén de claves, en función del almacén y de la configuración del CSP.

Para obtener más información, vea [Create and Store Column Master Keys (Always Encrypted) (Crear y almacenar claves maestras de columna (Always Encrypted))](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

<a name="rotatecek"></a> 
## <a name="rotating-column-encryption-keys"></a>Rotación de claves de cifrado de columnas

La rotación de una clave de cifrado de columnas implica descifrar los datos de todas las columnas cifrados con la clave que se va a rotar y volver a cifrarlos con la nueva clave de cifrado de columnas.

>[!NOTE]
> La rotación de una clave de cifrado de columnas puede tardar mucho tiempo si las tablas que contienen columnas cifradas con la clave que se va a rotar son grandes. Mientras se vuelven a cifrar los datos, las aplicaciones no pueden escribir en las tablas afectadas. Por lo tanto, la organización tiene que planear muy cuidadosamente cualquier rotación de claves de cifrado de columnas.
Para realizar la rotación de una clave de cifrado de columnas, use el Asistente para Always Encrypted.

1.  Para abrir el asistente para la base de datos, haga clic con el botón derecho en la base de datos, seleccione **Tareas**y, después, haga clic en **Cifrar columnas**.
2.  Revise la página **Introduction** y haga clic en **Next**.
3.  En la página **Selección de columna** , expanda las tablas y busque todas las columnas que quiera reemplazar que actualmente estén cifradas con la clave de cifrado de columnas antigua.
4.  Para cada columna cifrada con la clave de cifrado de columnas antigua, establezca la **Clave de cifrado** en una nueva clave generada automáticamente. **Nota:** También puede crear una clave de cifrado de columnas antes de ejecutar el asistente. Consulte la sección anterior *Aprovisionamiento de claves de cifrado de columnas* .
5.  En la página **Configuración de la clave maestra** , seleccione una ubicación para almacenar la clave nueva y seleccione un origen de clave maestra. Después, haga clic en **Siguiente**. **Nota:** Si usa una clave de cifrado de columnas existente (no una clave generada automáticamente), no debe realizar ninguna acción en esta página.
6.  En la página **Validación**, elija si quiere ejecutar inmediatamente el script o crear un script de PowerShell y, después, haga clic en **Siguiente**.
7.  En la página **Resumen** , revise las opciones que ha seleccionado, haga clic en **Finalizar** y cierre el asistente cuando finalice.
8.  En el **Explorador de objetos**, vaya a la carpeta **Seguridad &gt; Siempre claves cifradas&gt; Claves de cifrado de columna** y encuentre la clave de cifrado de columnas antigua que quiere quitar de la base de datos. Haga clic con el botón derecho en la clave y seleccione **Eliminar**.

### <a name="permissions"></a>Permisos

La rotación de una clave de cifrado de columnas requiere los siguientes permisos de base de datos: **ALTER ANY COLUMN MASTER KEY** : es obligatorio si se usa una nueva clave de cifrado de columnas generada automáticamente (también se generarán una nueva clave maestra de columna y sus metadatos nuevos).
**ALTER ANY COLUMN ENCRYPTION KEY** : es necesario para agregar metadatos a la nueva clave de cifrado de columnas.
**VIEW ANY COLUMN MASTER KEY DEFINITION** : es necesario para tener acceso a los metadatos de las claves maestras de columna y poder leerlos.
**VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** : es necesario para tener acceso a los metadatos de las claves de cifrado de columnas y poder leerlos.

También debe tener acceso a las claves maestras de columna de las claves de cifrado de columnas antigua y nueva. Para tener acceso a un almacén de claves y usar una clave maestra de columna, es posible que necesite permisos en el almacén de claves o en la clave:
- **Almacén de certificados, equipo local** : debe tener acceso de lectura al certificado que se usa como clave maestra de columna o ser el administrador del equipo.
- **Almacén de claves de Azure** : necesita los permisos get, unwrapKey y verify en el almacén que contiene la clave maestra de columna.
- **Proveedor de almacén de claves (CNG)** : se le podrían solicitar el permiso y las credenciales al usar una clave o un almacén de claves, en función del almacén y de la configuración del KSP.
- **Proveedor de servicios criptográficos (CAPI)** : se le podrían solicitar el permiso y las credenciales al usar una clave o un almacén de claves, en función del almacén y de la configuración del CSP.

Para obtener más información, vea [Create and Store Column Master Keys (Always Encrypted) (Crear y almacenar claves maestras de columna (Always Encrypted))](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

## <a name="performing-dac-upgrade-operations-when-database-or-dacpac-uses-always-encrypted"></a>Realización de operaciones de actualización de DAC cuando la base de datos o DACPAC usan Always Encrypted

Se admiten[operaciones DAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_3) en bases de datos y archivos DACPAC con esquemas que contienen columnas cifradas. Se aplica una serie de consideraciones especiales a la operación de actualización de DAC. Consulte [Actualizar una aplicación de capa de datos](../../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md) para obtener información sobre cómo realizar una operación de actualización de DAC en diversas herramientas, incluido SSMS. 

Cuando se actualiza una base de datos mediante un DACPAC y el DACPAC o la base de datos de destino tienen columnas cifradas, la operación de actualización desencadenará una operación de cifrado de datos si se cumplen todas las condiciones que se indican a continuación:
- La base de datos contiene una columna con datos.
- En el DACPAC existe la misma columna.
- La configuración de cifrado de la columna de la base de datos es diferente de la configuración de la columna correspondiente en el DACPAC. Consulte la tabla siguiente para obtener más información.

| Condición|Acción|
|:---|:---|
|La columna está cifrada en el DACPAC y no está cifrada en la base de datos.| Los datos de la columna se cifrarán.|
|La columna no está cifrada en el DACPAC y está cifrada en la base de datos.| Los datos de la columna se descifrarán (se quitará el cifrado de la columna).|
| La columna está cifrada en el DACPAC y en la base de datos, pero la columna del DACPAC usa un tipo de cifrado diferente o una clave de cifrado de columnas diferentes de los que usa la columna correspondiente de la base de datos.|Los datos de la columna se descifrarán y luego se volverán a cifrar para que coincida con la configuración de cifrado del DACPAC.|

> [!NOTE]
> Si la clave maestra de columna configurada para la columna de la base de datos o del DACPAC está almacenada en el Almacén de claves de Azure, se le pedirá que inicie sesión en Azure (si todavía no lo ha hecho).

### <a name="permissions"></a>Permisos

Para realizar una operación de actualización de DAC si Always Encrypted está configurado en el DACPAC o en la base de datos de destino, podría necesitar algunos de los permisos siguientes o todos, en función de las diferencias que existan entre el esquema del DACPAC y el esquema de la base de datos de destino.

*ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION*, *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION*

Si la operación de actualización desencadena una operación de cifrado de datos, también debe tener acceso a las claves maestras de columna configuradas para las columnas afectadas:
- **Almacén de certificados, equipo local** : debe tener acceso de lectura al certificado que se usa como clave maestra de columna o ser el administrador del equipo.
- **Almacén de claves de Azure** : necesita los permisos *create*, *get*, *unwrapKey*, *wrapKey*, *sign*y *verify* en el almacén que contiene la clave maestra de columna.
- **Proveedor de almacén de claves (CNG)** : se le podrían solicitar el permiso y las credenciales al usar una clave o un almacén de claves, en función del almacén y de la configuración del KSP.
- **Proveedor de servicios criptográficos (CAPI)** : se le podrían solicitar el permiso y las credenciales al usar una clave o un almacén de claves, en función del almacén y de la configuración del CSP.

Para obtener más información, vea [Create and Store Column Master Keys (Always Encrypted) (Crear y almacenar claves maestras de columna (Always Encrypted))](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

## <a name="migrating-databases-with-encrypted-columns-using-bacpac"></a>Migrar bases de datos con columnas cifradas con BACPAC

Al exportar una base de datos, todos los datos almacenados en columnas cifradas se recuperan y se incluyen en el [BACPAC](https://msdn.microsoft.com/library/ee210546.aspx#Anchor_4) resultante (en formato cifrado). El BACPAC resultante también contiene los metadatos de las claves de Always Encrypted.

Al importar el BACPAC en una base de datos, los datos cifrados del BACPAC se cargan en la base de datos y se vuelven a crear los metadatos de clave de Always Encrypted.

Si tiene una aplicación que está configurada para modificar o recuperar los datos cifrados almacenados en la base de datos de origen (la que exportó), no tendrá que hacer nada para permitir que la aplicación consulte los datos cifrados en la base de datos de destino, ya que las claves de ambas bases de datos son las mismas.


### <a name="permissions"></a>Permisos

Necesita los permisos *ALTER ANY COLUMN MASTER KEY* y *ALTER ANY COLUMN ENCRYPTION KEY* en la base de datos de origen. Necesita los permisos *ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION*y *VIEW ANY COLUMN ENCRYPTION* en la base de datos de destino.

## <a name="migrating-databases-with-encrypted-columns-using-sql-server-import-and-export-wizard"></a>Migrar bases de datos con columnas cifradas mediante el Asistente para importación y exportación de SQL Server

En comparación con el uso de archivos BACPAC, el [Asistente para importación y exportación de SQL Server](~/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md) ofrece un mayor control sobre la manera en que se gestionan los datos almacenados en columnas cifradas durante la migración de datos.

- Si el origen de datos es una base de datos que usa Always Encrypted, puede configurar la conexión de origen de datos para que los datos almacenados en columnas cifradas se descifren durante la operación de exportación o permanezcan cifrados.
- Si el destino de datos es una base de datos que usa Always Encrypted, puede configurar la conexión de destino de datos para que los datos dirigidos a columnas cifradas se descifren.

Para habilitar el descifrado (para el origen de datos) o el cifrado (para el destino de datos), debe configurar la conexión de origen o destino de datos de modo que use el [Proveedor de datos .NET Framework para SQL Server](https://msdn.microsoft.com/library/system.data.sqlclient.aspx) y debe establecer la palabra clave de la cadena de conexión Valor de cifrado de columnas en *Habilitado*.

En la tabla siguiente se enumeran los posibles escenarios de migración y su relación con Always Encrypted, junto con la configuración de origen y destino de datos para cada conexión.

| Escenario|Configuración de la conexión de origen| Configuración de la conexión de destino
|:---|:---|:---
|Cifrar los datos durante la migración (los datos están almacenados como texto no cifrado en el origen de datos y se migran a columnas cifradas en el destino de datos).| Proveedor de datos/controlador: *cualquiera*<br><br>Valor de cifrado de columnas = Deshabilitado<br><br>(Si se usan el Proveedor de datos de .NET Framework para SQL Server y .NET Framework 4.6 o posterior). | Proveedor de datos/controlador: *Proveedor de datos de .NET Framework para SQL Server* (se requiere .NET Framework 4.6 o posterior)<br><br>Valor de cifrado de columnas = Habilitado
| Descifrar los datos durante la migración (los datos están almacenados en columnas cifradas en el origen de datos y se migran como texto no cifrado al destino de datos; si el destino de datos es una base de datos, las columnas de destino no se cifran).<br><br>**Nota:** Las tablas de destino con columnas cifradas deben existir antes de la migración.|Proveedor de datos/controlador: *Proveedor de datos de .NET Framework para SQL Server* (se requiere .NET Framework 4.6 o posterior)<br><br>Valor de cifrado de columnas = Habilitado|Proveedor de datos/controlador: *cualquiera*<br><br>Valor de cifrado de columnas = Deshabilitado<br><br>(Si se usan el Proveedor de datos de .NET Framework para SQL Server y .NET Framework 4.6 o posterior).
|Volver a cifrar los datos durante la migración (los datos están almacenados en columnas cifradas en el origen de datos y se migran como texto no cifrado al destino de datos, a columnas que usan tipos de cifrado diferentes de los de las claves de cifrado de columnas).<br><br>**Nota:** Las tablas de destino con columnas cifradas deben existir antes de la migración.| Proveedor de datos/controlador: *Proveedor de datos de .NET Framework para SQL Server* (se requiere .NET Framework 4.6 o posterior)<br><br>Valor de cifrado de columnas = Habilitado|Proveedor de datos/controlador: *Proveedor de datos de .NET Framework para SQL Server* (se requiere .NET Framework 4.6 o posterior)<br><br>Valor de cifrado de columnas = Habilitado
|Mover datos cifrados sin descifrarlos.<br><br>**Nota:** Las tablas de destino con columnas cifradas deben existir antes de la migración.| Proveedor de datos/controlador: *cualquiera*<br>Valor de cifrado de columnas = Deshabilitado<br><br>(Si se usan el Proveedor de datos de .NET Framework para SQL Server y .NET Framework 4.6 o posterior).| Proveedor de datos/controlador: *cualquiera*<br>Valor de cifrado de columnas = Deshabilitado<br><br>(Si se usan el Proveedor de datos de .NET Framework para SQL Server y .NET Framework 4.6 o posterior).<br><br>El usuario debe tener ALLOW_ENCRYPTED_VALUE_MODIFICATIONS establecido en ON.<br><br>Para obtener más información, vea [Migración de información confidencial protegida mediante Always Encrypted](../../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md).


### <a name="permissions"></a>Permisos

Para **cifrar** o **descifrar** datos almacenados en el origen de datos, necesita tener los permisos *VIEW ANY COLUMN MASTER KEY DEFINITION* y *VIEW ANY COLUMN ENCRYPTION KEY DEFINITION* en la base de datos de origen.

También necesita tener acceso a las claves maestras de columna configuradas para las columnas, donde se almacenan los datos que se cifran o se descifran:
- **Almacén de certificados, equipo local** : debe tener acceso de lectura al certificado que se usa como clave maestra de columna o ser el administrador del equipo.
- **Almacén de claves de Azure** : necesita los permisos get, unwrapKey, wrapKey, sign y verify en el almacén que contiene la clave maestra de columna.
- **Proveedor de almacén de claves (CNG)** : el permiso y las credenciales que se le podrían solicitar al usar una clave o un almacén de claves dependen del almacén y de la configuración del proveedor de almacén de claves (KSP).
- **Proveedor de servicios criptográficos (CAPI)** : el permiso y las credenciales que se le podrían solicitar al usar una clave o un almacén de claves dependen del almacén y de la configuración del proveedor de servicios criptográficos (CSP).
Para obtener más información, vea [Create and Store Column Master Keys (Always Encrypted) (Crear y almacenar claves maestras de columna (Always Encrypted))](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md).

## <a name="see-also"></a>Ver también
- [Always Encrypted (motor de base de datos)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Asistente para Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-wizard.md)
- [Información general de administración de claves de Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Crear y almacenar claves maestras de columna (Always Encrypted)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)
- [Always Encrypted (desarrollo de clientes)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- [DROP COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/drop-column-master-key-transact-sql.md)
- [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)
- [ALTER COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-column-encryption-key-transact-sql.md)
- [DROP COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 
- [sys.column_master_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)
- [sys.column_encryption_keys (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)
- [Configurar Always Encrypted con PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)












