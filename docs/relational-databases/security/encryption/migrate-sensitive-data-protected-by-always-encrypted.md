---
title: Migración de información confidencial protegida mediante Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, bulk import
ms.assetid: b2ca08ed-a927-40fb-9059-09496752595e
caps.latest.revision: 11
author: aliceku
ms.author: aliceku
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8e1b17e46097ed7e88651858b571ac86d66ab9d8
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35701786"
---
# <a name="migrate-sensitive-data-protected-by-always-encrypted"></a>Migración de datos confidenciales protegidos mediante Always Encrypted
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
 Para cargar datos cifrados sin tener que volver realizar comprobaciones de metadatos en el servidor durante las operaciones de copia masiva, cree el usuario con la opción **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** . Esta opción se ha diseñado para usarse con herramientas heredadas de versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] (por ejemplo, bcp.exe) o flujos de trabajo de extracción, transformación y carga (ETL) de terceros que no pueden usar Always Encrypted. De esta forma, el usuario puede mover de forma segura los datos cifrados de un conjunto de tablas, que contengan las columnas cifradas, a otro conjunto de tablas con columnas cifradas (en la misma base de datos o en otra diferente).  
 -  
 ## <a name="the-allowencryptedvaluemodifications-option"></a>La opción ALLOW_ENCRYPTED_VALUE_MODIFICATIONS  
 Tanto [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) como [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) tienen la opción ALLOW_ENCRYPTED_VALUE_MODIFICATIONS. Cuando el valor se establece en ON (la opción predeterminada es OFF), esta opción suprime las comprobaciones de metadatos criptográficos del servidor en operaciones de copia masiva, lo que permite al usuario copiar los datos de forma masiva entre tablas o bases de datos sin descifrar los datos.  
  
## <a name="data-migration-scenarios"></a>Escenarios de migración de datos  
En la siguiente tabla se muestra la configuración recomendada adecuada para varios escenarios de migración.  
 
![Migración de Always Encrypted](../../../relational-databases/security/encryption/media/always-encrypted-migration.PNG "Migración de Always Encrypted")  

## <a name="bulk-loading-of-encrypted-data"></a>Carga masiva de datos cifrados  
Utilice el siguiente proceso para cargar datos cifrados.  

1.  Establezca el valor de la opción en ON para el usuario en la base de datos que es el destino de la operación de copia masiva. Por ejemplo:  
 
   ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON;  
   ```  

2.  Ejecute la herramienta o aplicación de copia masiva que conectándose como ese usuario. Si la aplicación usa un controlador cliente con Always Encrypted habilitado, asegúrese de que la cadena de conexión del origen de datos no contiene **column encryption setting=enabled** para garantizar que los datos recuperados de las columnas cifradas permanecen cifrados. Para obtener más información, vea [Always Encrypted &#40;desarrollo de cliente&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)).  
  
3.  Vuelva a establecer el valor de la opción ALLOW_ENCRYPTED_VALUE_MODIFICATIONS en OFF. Por ejemplo:  

    ```  
    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = OFF;  
    ```  

## <a name="potential-for-data-corruption"></a>Posibilidad de daño en datos  
Si esta opción no se utiliza adecuadamente, pueden dañarse los datos. La opción **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** permite al usuario insertar los datos en columnas cifradas de la base de datos, incluidos los que se cifran con claves diferentes, los que se cifran incorrectamente o los que, directamente, no se cifran. Si el usuario copia accidentalmente los datos que no están cifrados correctamente mediante el esquema de cifrado (clave de cifrado, algoritmo y tipo de cifrado) configurado para la columna de destino, no podrá descifrar los datos (se dañarán). Esta opción debe utilizarse con cuidado, ya que puede provocar que se dañen los datos de la base de datos.  

En el siguiente escenario se muestra cómo importar datos de forma incorrecta podría provocar que se dañen los datos:  

1.  El valor de la opción se establece en ON para un usuario.  
 
2.  El usuario ejecuta la aplicación que se conecta a la base de datos. La aplicación utiliza las API de operaciones masiva para insertar valores de texto sin formato en las columnas cifradas. La aplicación espera que un controlador cliente con Always Encrypted cifre los datos durante la inserción. Pero la aplicación no está configurada correctamente, por lo que termina usando un controlador que no admite Always Encrypted o la cadena de conexión no contiene **column encryption setting=enabled**.  

3.  La aplicación envía los valores de texto no cifrado al servidor. Como las comprobaciones de metadatos criptográficos se deshabilitan en el servidor para el usuario, dicho servidor permite que los datos incorrectos (texto no cifrado en lugar de texto cifrado correctamente) se inserten en una columna cifrada.  
 
4.  La misma aplicación u otra diferente se conecta a la base de datos por medio de un controlador con Always Encrypted habilitado y **column encryption setting=enabled** en la cadena de conexión, y recupera los datos. La aplicación espera que los datos se descifren de forma transparente. Sin embargo, el controlador no puede descifrar los datos porque los datos son texto cifrado de forma incorrecta.  

## <a name="best-practice"></a>Práctica recomendada  
 
Utilice mediante esta opción cuentas de usuario designadas para cargas de trabajo que vayan a ejecutarse durante un largo periodo.  
 
En las herramientas o las aplicaciones de copia masiva que se ejecutan en periodos breves y que necesitan mover los datos cifrados sin descifrarlos, establezca el valor de la opción en ON inmediatamente antes de ejecutar la aplicación y revierta el valor a OFF justo después de ejecutar la operación.  
 
No utilice esta opción para desarrollar nuevas aplicaciones. En su lugar, use un controlador de cliente (como ADO 4.6.1), que ofrece una API para suprimir las comprobaciones de metadatos criptográficos en una sola sesión.  

## <a name="see-also"></a>Ver también  
[CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)   
[ALTER USER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-user-transact-sql.md)   
[Always Encrypted &#40;motor de base de datos&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[Asistente para Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-wizard.md)   
[Always Encrypted &#40;desarrollo de cliente&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  
