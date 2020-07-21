---
title: Carga masiva de datos cifrados en columnas con Always Encrypted
description: Obtenga información sobre cómo hacer una carga masiva de datos a columnas que usan Always Encrypted con SQL Server.
ms.custom: seo-lt-2019
ms.date: 11/04/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, bulk import
ms.assetid: b2ca08ed-a927-40fb-9059-09496752595e
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 22ad17c49a2f084453c87f26b9c782404f93483d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784026"
---
# <a name="bulk-load-encrypted-data-to-columns-using-always-encrypted"></a>Carga masiva de datos cifrados en columnas con Always Encrypted
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

Para cargar datos cifrados sin tener que volver realizar comprobaciones de metadatos en el servidor durante las operaciones de copia masiva, cree el usuario con la opción **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** . Esta opción se ha diseñado para usarse con herramientas heredadas o flujos de trabajo de extracción, transformación y carga (ETL) de terceros que no pueden usar Always Encrypted. De esta forma, el usuario puede mover de forma segura los datos cifrados de un conjunto de tablas, que contengan las columnas cifradas, a otro conjunto de tablas con columnas cifradas (en la misma base de datos o en otra diferente).  

 ## <a name="the-allow_encrypted_value_modifications-option"></a>La opción ALLOW_ENCRYPTED_VALUE_MODIFICATIONS  
 Tanto [CREATE USER](../../../t-sql/statements/create-user-transact-sql.md) como [ALTER USER](../../../t-sql/statements/alter-user-transact-sql.md) tienen la opción ALLOW_ENCRYPTED_VALUE_MODIFICATIONS. Cuando el valor se establece en ON (la opción predeterminada es OFF), esta opción suprime las comprobaciones de metadatos criptográficos del servidor en operaciones de copia masiva, lo que permite al usuario copiar los datos de forma masiva entre tablas o bases de datos sin descifrar los datos.  
  
## <a name="data-migration-scenarios"></a>Escenarios de migración de datos  
En la siguiente tabla se muestra la configuración recomendada adecuada para varios escenarios de migración.  
 
![always-encrypted-migration](../../../relational-databases/security/encryption/media/always-encrypted-migration.PNG "always-encrypted-migration")  

## <a name="bulk-loading-of-encrypted-data"></a>Carga masiva de datos cifrados  
Utilice el siguiente proceso para cargar datos cifrados.  

1.  Establezca el valor de la opción en ON para el usuario en la base de datos que es el destino de la operación de copia masiva. Por ejemplo:  
 
   ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON;  
   ```  

2.  Ejecute la herramienta o aplicación de copia masiva que conectándose como ese usuario. Si la aplicación usa un controlador cliente con Always Encrypted habilitado, asegúrese de que la cadena de conexión del origen de datos no contiene **column encryption setting=enabled** para garantizar que los datos recuperados de las columnas cifradas permanecen cifrados. Para obtener más información, consulte [Desarrollo de aplicaciones con Always Encrypted](always-encrypted-client-development.md).  
  
3.  Vuelva a establecer el valor de la opción ALLOW_ENCRYPTED_VALUE_MODIFICATIONS en OFF. Por ejemplo:  

    ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = OFF;  
    ```  

## <a name="potential-for-data-corruption"></a>Posibilidad de daño en datos  
Si esta opción no se utiliza adecuadamente, pueden dañarse los datos. La opción **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** permite al usuario insertar los datos en columnas cifradas de la base de datos, incluidos los que se cifran con claves diferentes, los que se cifran incorrectamente o los que, directamente, no se cifran. Si el usuario copia accidentalmente los datos que no están correctamente cifrados mediante el esquema de cifrado (clave de cifrado de columna, algoritmo y tipo de cifrado) configurado para la columna de destino, no se pueden descifrar los datos (se dañan). Esta opción debe utilizarse con cuidado, ya que puede provocar que se dañen los datos de la base de datos.  

En el siguiente escenario se muestra cómo importar datos de forma incorrecta podría provocar que se dañen los datos:  

1.  El valor de la opción se establece en ON para un usuario.  
 
2.  El usuario ejecuta la aplicación que se conecta a la base de datos. La aplicación utiliza las API de operaciones masiva para insertar valores de texto sin formato en las columnas cifradas. La aplicación espera que un controlador cliente con Always Encrypted cifre los datos durante la inserción. Pero la aplicación no está configurada correctamente, por lo que termina usando un controlador que no admite Always Encrypted o la cadena de conexión no contiene **column encryption setting=enabled**.  

3.  La aplicación envía los valores de texto no cifrado al servidor. Como las comprobaciones de metadatos criptográficos se deshabilitan en el servidor para el usuario, dicho servidor permite que los datos incorrectos (texto no cifrado en lugar de texto cifrado correctamente) se inserten en una columna cifrada.  
 
4.  La misma aplicación u otra diferente se conecta a la base de datos por medio de un controlador con Always Encrypted habilitado y **column encryption setting=enabled** en la cadena de conexión, y recupera los datos. La aplicación espera que los datos se descifren de forma transparente. Sin embargo, el controlador no puede descifrar los datos porque los datos son texto cifrado de forma incorrecta.  

## <a name="best-practice"></a>Procedimiento recomendado  
 
Utilice mediante esta opción cuentas de usuario designadas para cargas de trabajo que vayan a ejecutarse durante un largo periodo.  
 
En las herramientas o las aplicaciones de copia masiva que se ejecutan en periodos breves y que necesitan mover los datos cifrados sin descifrarlos, establezca el valor de la opción en ON inmediatamente antes de ejecutar la aplicación y revierta el valor a OFF justo después de ejecutar la operación.  
 
No utilice esta opción para desarrollar nuevas aplicaciones. En su lugar, use un controlador de cliente que ofrezca una API para suprimir las comprobaciones de metadatos criptográficos para una sola sesión, como la opción AllowEncryptedValueModifications del proveedor de datos .NET Framework para SQL Server. Para más detalles, consulte [Copiar datos cifrados con SqlBulkCopy](develop-using-always-encrypted-with-net-framework-data-provider.md#copying-encrypted-data-using-sqlbulkcopy). 

## <a name="next-steps"></a>Pasos siguientes
- [Consulta de columnas mediante Always Encrypted con SQL Server Management Studio](always-encrypted-query-columns-ssms.md)
- [Desarrollo de aplicaciones con Always Encrypted](always-encrypted-client-development.md)

## <a name="see-also"></a>Consulte también  
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Migración de datos a o desde columnas mediante Always Encrypted con el Asistente para importación y exportación de SQL Server](always-encrypted-migrate-using-import-export-wizard.md)
- [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)   
- [ALTER USER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-user-transact-sql.md)   

