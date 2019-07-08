---
title: Restaurar una clave maestra de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/02/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], importing
ms.assetid: 16897cc5-db8f-43bb-a38e-6855c82647cf
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 4dd095f8d4a9254b88680b13bffcf319960336f3
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67585613"
---
# <a name="restore-a-database-master-key"></a>Restaurar una clave maestra de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo restaurar la clave maestra de una base de datos en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
### <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
  
- Al restaurar la clave maestra, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] descifra todas las claves cifradas con la clave maestra actualmente activa y cifra estas claves con la clave maestra restaurada. Esta operación requiere un uso intensivo de recursos, por lo que debe programarse durante un período de baja demanda. Si la clave maestra de base de datos no se encuentra abierta, no puede abrirse o alguna de las claves cifradas con ella no pueden descifrarse, la operación de restauración no se puede realizar.  
  
- Si se producen errores durante cualquier descifrado, se producirán errores en la restauración. Puede utilizar la opción FORCE para omitir los errores, pero esta opción provocará la pérdida de los datos que no sea posible descifrar.  
  
- Si se cifró la clave maestra con la clave maestra de servicio, la clave maestra restaurada también se cifrará con la clave maestra de servicio.  
  
- Si no hay una clave maestra en la base de datos actual, RESTORE MASTER KEY creará una clave maestra. La nueva clave maestra no se cifrará automáticamente con la clave maestra de servicio.  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos
Necesita el permiso CONTROL en la base de datos.  
  
## <a name="using-sql-server-management-studio-with-transact-sql"></a>Usar SQL Server Management Studio con Transact-SQL  
  
### <a name="to-restore-the-database-master-key"></a>Para restaurar la clave maestra de una base de datos  
  
1. Recupere una copia de seguridad de la clave maestra de la base de datos, ya sea desde un medio físico de copia de seguridad o desde un directorio del sistema de archivos local.  
  
2. En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
3. En la barra de Estándar, haga clic en **Nueva consulta**.  
  
4. Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    ```sql
    -- Restores the database master key of the AdventureWorks2012 database.  
    USE AdventureWorks2012;  
    GO  
    RESTORE MASTER KEY   
        FROM FILE = 'c:\backups\keys\AdventureWorks2012_master_key'   
        DECRYPTION BY PASSWORD = '3dH85Hhk003#GHkf02597gheij04'   
        ENCRYPTION BY PASSWORD = '259087M#MyjkFkjhywiyedfgGDFD';  
    GO  
    ```  
  
    > [!NOTE]  
    > The file path to the key and the key's password (if it exists) will be different than what is indicated above. Please make sure that both are specific to your server and key set-up.  
  
 Para obtener más información, vea [RESTORE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/restore-master-key-transact-sql.md)  
