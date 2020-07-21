---
title: Restaurar la clave maestra de servicio | Microsoft Docs
description: Aprenda a restaurar la clave maestra de servicio en SQL Server mediante Transact-SQL. La clave maestra de servicio es la raíz de la jerarquía de cifrado de SQL Server.
ms.custom: ''
ms.date: 01/02/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- service master key [SQL Server], importing
- service master key [SQL Server], restoring
ms.assetid: 14bdbbbe-d384-4692-b670-4243d2466fe1
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: b4e2d053a232d374360177159cb3b97785f73a4f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898026"
---
# <a name="restore-the-service-master-key"></a>Restaurar la clave maestra de servicio
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  En este tema se describe cómo restaurar la clave maestra de servicio en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
> [!WARNING]  
> Es improbable que alguna vez deba restaurar la clave maestra de servicio. Si tiene que hacerlo, debe proceder con mucha precaución. Para obtener más información, consulte [Back Up the Service Master Key](../../../relational-databases/security/encryption/back-up-the-service-master-key.md).  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
### <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
  
- Al restaurar la clave maestra de servicio, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] descifra todas las claves y secretos cifrados con la clave maestra de servicio actual y, a continuación, los cifra con la clave maestra de servicio cargada desde el archivo de copia de seguridad.  
  
- Si se producen errores durante cualquier descifrado, se producirán errores en la restauración. Puede utilizar la opción FORCE para omitir los errores, pero esta opción provocará la pérdida de los datos que no sea posible descifrar.  
  
- La regeneración de la jerarquía de cifrado es una operación que requiere un uso intensivo de recursos. Debe programarla durante un período de baja demanda.  
  
> [!CAUTION]  
> La clave maestra de servicio es la raíz de la jerarquía de cifrado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . La clave maestra de servicio protege directa o indirectamente las demás claves del árbol. Si no es posible descifrar una clave dependiente durante una restauración forzada, se perderán los datos que protege la clave.  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
Requiere el permiso CONTROL SERVER en el servidor.  
  
## <a name="using-transact-sql"></a>Usar Transact-SQL  
  
### <a name="to-restore-the-service-master-key"></a>Para restaurar la clave maestra de servicio  
  
1. Recupere una copia de seguridad de la clave maestra de servicio, ya sea desde un medio físico de copia de seguridad o desde un directorio del sistema de archivos local.  
  
2. En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
3. En la barra de Estándar, haga clic en **Nueva consulta**.  
  
4. Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```sql
    -- Restores the service master key from a backup file.  
    RESTORE SERVICE MASTER KEY   
        FROM FILE = 'c:\temp_backups\keys\service_master_key'   
        DECRYPTION BY PASSWORD = '3dH85Hhk003GHk2597gheij4';  
    GO  
    ```  
  
    > [!NOTE]  
    > La ruta de acceso de archivo a la clave y la contraseña de la clave (si existe) serán distintas de las que se indica más arriba. Asegúrese de que ambas son específicas para la instalación del servidor y de la clave.
