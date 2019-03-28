---
title: sp_refresh_parameter_encryption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_refresh_parameter_encryption
- sp_refresh_parameter_encryption_TSQL
- sys.sp_refresh_parameter_encryption
- sys.sp_refresh_parameter_encryption_TSQL
helpviewer_keywords:
- sp_refresh_parameter_encryption
- Always Encrypted, sp_refresh_parameter_encryption
ms.assetid: 00b44baf-fcf0-4095-aabe-49fa87e77316
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f483c6fe53ab980893ba8e1104b46e073336b027
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58533987"
---
# <a name="sprefreshparameterencryption-transact-sql"></a>sp_refresh_parameter_encryption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Actualiza los metadatos de Always Encrypted para los parámetros de la no enlazada a esquema de procedimiento almacenado, función definida por el usuario, vista, desencadenador DML, desencadenador DDL de nivel de base de datos o desencadenador DDL de nivel de servidor en la base de datos actual. 

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sys.sp_refresh_parameter_encryption [ @name = ] 'module_name' 
    [ , [ @namespace = ] '<class>' ]
[ ; ]

<class> ::=
{ DATABASE_DDL_TRIGGER | SERVER_DDL_TRIGGER }
```

## <a name="arguments"></a>Argumentos

`[ @name = ] 'module_name'` Es el nombre del procedimiento almacenado, función definida por el usuario, vista, desencadenador DML, desencadenador DDL de nivel de base de datos o desencadenador DDL de nivel de servidor. *module_name* no puede ser un common language runtime (CLR) procedimiento almacenado o una función CLR. *module_name* no puede estar enlazada a esquema. *module_name* es `nvarchar`, no tiene ningún valor predeterminado. *module_name* puede ser un identificador formado por varias partes, pero solo puede hacer referencia a objetos en la base de datos actual.

`[ @namespace = ] ' < class > '` Es la clase del módulo especificado. Cuando *module_name* es un desencadenador DDL, `<class>` es necesario. El valor de `<class>` es `nvarchar(20)`. Las entradas válidas son `DATABASE_DDL_TRIGGER` y `SERVER_DDL_TRIGGER`.    

## <a name="return-code-values"></a>Valores de código de retorno  

0 (correcto) o un número distinto de cero (error)


## <a name="remarks"></a>Comentarios

Los metadatos de cifrado para los parámetros de un módulo pueden quedar obsoleto, si:   
* Propiedades de cifrado de una columna en una tabla se han actualizado las referencias de módulo. Por ejemplo, se ha quitado una columna y se ha agregado una nueva columna con el mismo nombre, pero un tipo de cifrado diferente, clave de cifrado o un algoritmo de cifrado.  
* El módulo hace referencia a otro módulo con los metadatos de cifrado del parámetro obsoleto.  

Cuando se modifican las propiedades de cifrado de una tabla, `sp_refresh_parameter_encryption` se debe ejecutar para los módulos que directa o indirectamente hace referencia a la tabla. Este procedimiento almacenado se puede llamar en esos módulos en cualquier orden, sin solicitar al usuario a la primera actualización al módulo interno antes de pasar a sus llamadores.

`sp_refresh_parameter_encryption` no afecta a ningún permiso, propiedades extendidas, o `SET` opciones que están asociados con el objeto. 

Para actualizar un desencadenador DDL de nivel de servidor, ejecute este procedimiento almacenado desde el contexto de cualquier base de datos.

> [!NOTE]
>  Las firmas asociadas con el objeto se anulan al ejecutar `sp_refresh_parameter_encryption`.

## <a name="permissions"></a>Permisos

Requiere `ALTER` permiso en el módulo y `REFERENCES` permiso en todas las colecciones de esquemas XML que hace referencia el objeto y tipos definidos por el usuario CLR.   

Cuando el módulo especificado es un desencadenador DDL de nivel de base de datos, requiere `ALTER ANY DATABASE DDL TRIGGER` permiso en la base de datos actual.    

Cuando el módulo especificado es un desencadenador DDL de nivel de servidor, requiere `CONTROL SERVER` permiso.

Para los módulos que se definen con la `EXECUTE AS` cláusula, `IMPERSONATE` se requiere el permiso en la entidad de seguridad especificada. Por lo general, la actualización de un objeto no cambia su `EXECUTE AS` principal, a menos que el módulo se ha definido con `EXECUTE AS USER` y el nombre de usuario de la entidad de seguridad ahora se resuelve como un usuario diferente que tenía en el momento el módulo se ha creado.
 
## <a name="examples"></a>Ejemplos

El ejemplo siguiente se crea una tabla y un procedimiento que hacen referencia a la tabla, configura Always Encrypted y, a continuación, se muestra cómo modificar la tabla y ejecutando el `sp_refresh_parameter_encryption` procedimiento.  

En primer lugar, cree la tabla inicial y un procedimiento almacenado que hacen referencia a la tabla.
```sql
CREATE TABLE [Patients]([PatientID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11), 
    [FirstName] [nvarchar](50) NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [MiddleName] [nvarchar](50) NULL,
    [StreetAddress] [nvarchar](50) NOT NULL,
    [City] [nvarchar](50) NOT NULL,
    [ZipCode] [char](5) NOT NULL,
    [State] [char](2) NOT NULL,
    [BirthDate] [date] NOT NULL,
 CONSTRAINT [PK_Patients] PRIMARY KEY CLUSTERED 
(
    [PatientID] ASC
) WITH 
    (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, 
     IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, 
     ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY];
GO

CREATE PROCEDURE [find_patient] @SSN [char](11)
AS
BEGIN
    SELECT * FROM [Patients] WHERE SSN=@SSN
END;
GO
```

A continuación, establezca las claves de Always Encrypted.
```sql
CREATE COLUMN MASTER KEY [CMK1]
WITH
(
       KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305'
);
GO

CREATE COLUMN ENCRYPTION KEY [CEK1]
WITH VALUES
(
       COLUMN_MASTER_KEY = [CMK1],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 
       0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085
);
GO
```


Por último, reemplazamos la columna SSN con la columna cifrada y, a continuación, ejecuta el `sp_refresh_parameter_encryption` procedimiento para actualizar los componentes de Always Encrypted.
```sql
ALTER TABLE [Patients] DROP COLUMN [SSN];
GO

ALTER TABLE [Patients] 
    ADD [SSN] [char](11) COLLATE Latin1_General_BIN2 
    ENCRYPTED WITH 
        (COLUMN_ENCRYPTION_KEY = [CEK1], 
        ENCRYPTION_TYPE = Deterministic, 
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') 
    NOT NULL;
GO

EXEC sp_refresh_parameter_encryption [find_patient];
GO
```

## <a name="see-also"></a>Vea también 

[Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[Asistente para Always Encrypted](../../relational-databases/security/encryption/always-encrypted-wizard.md)   

