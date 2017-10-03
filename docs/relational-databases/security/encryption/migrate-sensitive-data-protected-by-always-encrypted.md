---
title: "Migración de información confidencial protegida mediante Always Encrypted | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/04/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Always Encrypted, bulk import
ms.assetid: b2ca08ed-a927-40fb-9059-09496752595e
caps.latest.revision: 11
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 20eb76a9e2cc89015167b5199f1a6f8dd5baec16
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="migrate-sensitive-data-protected-by-always-encrypted"></a>Migración de datos confidenciales protegidos mediante Always Encrypted
 <a name="to-load-encrypted-data-without-performing-metadata-checks-on-the-server-during-bulk-copy-operations-create-the-user-with-the-allowencryptedvaluemodifications-option-this-option-is-intended-to-be-used-by-legacy-tools-from-versions-of-includessnoversionincludesssnoversion-mdmd-older-than-includesssql15includessssql15-mdmd-such-as-bcpexe-or-by-using-third-party-extract-transform-load-etl-work-flows-that-cannot-use-always-encrypted-this-allows-a-user-to-securely-move-encrypted-data-from-one-set-of-tables-containing-encrypted-columns-to-another-set-of-tables-with-encrypted-columns-in-the-same-or-a-different-database"></a>Para cargar datos cifrados sin tener que volver realizar comprobaciones de metadatos en el servidor durante las operaciones de copia masiva, cree el usuario con la opción **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** . Esta opción se ha diseñado para usarse con herramientas heredadas de versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] (por ejemplo, bcp.exe) o flujos de trabajo de extracción, transformación y carga (ETL) de terceros que no pueden usar Always Encrypted. De esta forma, el usuario puede mover de forma segura los datos cifrados de un conjunto de tablas, que contengan las columnas cifradas, a otro conjunto de tablas con columnas cifradas (en la misma base de datos o en otra diferente).  
 -  
 -## Opción ALLOW_ENCRYPTED_VALUE_MODIFICATIONS  
 - Tanto [CREATE USER](https://msdn.microsoft.com/library/ms173463.aspx) como [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) tienen la opción ALLOW_ENCRYPTED_VALUE_MODIFICATIONS. Cuando el valor se establece en ON (la opción predeterminada es OFF), esta opción suprime las comprobaciones de metadatos criptográficos del servidor en operaciones de copia masiva, lo que permite al usuario copiar los datos de forma masiva entre tablas o bases de datos sin descifrar los datos.  
 -  
 -## Escenarios de migración de datos  
 - En la siguiente tabla se muestra la configuración recomendada adecuada para varios escenarios de migración.  
 -  
 - ![Migración de Always Encrypted](../../../relational-databases/security/encryption/media/always-encrypted-migration.PNG "Migración de Always Encrypted")  
 -  
 -## Carga masiva de datos cifrados  
 - Utilice el siguiente proceso para cargar datos cifrados.  
 -  
 -1.  Establezca el valor de la opción en ON para el usuario en la base de datos que es el destino de la operación de copia masiva. Por ejemplo:  
 -  
 -    ```  
 -    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON;  
 -    ```  
 -  
 -2.  Run your bulk copy application or tool connecting as that user. (If your application uses an Always Encrypted enabled client driver, make sure the connection string for the data source does not contain **column encryption setting=enabled** to ensure the data retrieved from encrypted columns remains encrypted. For more information, see [Always Encrypted &#40;client development&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md).)  
 -  
 -3.  Set the ALLOW_ENCRYPTED_VALUE_MODIFICATIONS option back to OFF. For example:  
 -  
 -    ```  
 -    ALTER USER Bob WITH ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = OFF;  
 -    ```  
 -  
 -## Potential for Data Corruption  
 - Improper use of this option can lead to data corruption. The **ALLOW_ENCRYPTED_VALUE_MODIFICATIONS** option allows the user to insert any data into encrypted columns in the database, including data that is encrypted with different keys, incorrectly encrypted, or not encrypted at all. If the user accidently copies the data that is not correctly encrypted using the encryption scheme (column encryption key, algorithm, encryption type) set up for the target column, you will not be able to decrypt the data (the data will be corrupted). This option must be used carefully, as it can lead to corrupting data in the database.  
 -  
 - The following scenario demonstrates how improperly importing data could lead to data corruption:  
 -  
 -1.  The option is set to ON for a user.  
 -  
 -2.  The user runs the application that connects to the database. The application uses bulk APIs to insert plain text values to encrypted columns. The application expects an Always Encrypted-enabled client driver to encrypt the data on insert. However, the application is misconfigured, so that either it ends up using a driver that does not support Always Encrypted or the connection string does not contain **column encryption setting=enabled**.  
 -  
 -3.  The application sends plaintext values to the server. As cryptographic metadata checks are disabled in the server for the user, the server lets the incorrect data (plaintext instead of correctly encrypted ciphertext) to be inserted into an encrypted column.  
 -  
 -4.  The same or another application connects to the database using an Always Encrypted-enabled driver and with **column encryption setting=enabled** in the connection string, and retrieves the data. The application expects the data to be transparently decrypted. However, the driver fails to decrypt the data because the data is incorrect ciphertext.  
 -  
 -## Best practice  
 -  
 --   Use designated user accounts for long running workloads using this option.  
 -  
 --   For short running bulk copy applications or tools that need to move encrypted data without decrypting it, set the option to ON immediately before running the application and set it back to OFF immediately after running the operation.  
 -  
 --   Do not use this option for developing new applications. Instead, use a client driver (such as  ADO 4.6.1) that offers an API for suppressing cryptographic metadata checks for a single session.  
 -  
 -## See Also  
 - [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md)   
 - [ALTER USER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-user-transact-sql.md)   
 - [Always Encrypted &#40;Database Engine&#41;](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 - [Always Encrypted Wizard](../../../relational-databases/security/encryption/always-encrypted-wizard.md)   
 - [Always Encrypted &#40;client development&#41;](../../../relational-databases/security/encryption/always-encrypted-client-development.md)  
