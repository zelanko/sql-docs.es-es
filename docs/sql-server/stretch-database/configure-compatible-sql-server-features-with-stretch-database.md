---
title: "Configurar características compatibles de SQL Server con Stretch Database | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8121ede-1aec-459b-b7b0-1408bb3e62fb
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 84464c4553eab6d8e65c0bf6b476ae728e2a8463
ms.lasthandoff: 04/11/2017

---
# <a name="configure-compatible-sql-server-features-with-stretch-database"></a>Configurar características compatibles de SQL Server con Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Realice pasos simples para configurar las siguientes características de SQL Server para trabajar con Stretch Database.
-   AlwaysOn
-   Always Encrypted
-   Cifrado de datos transparente (TDE)
-   Tablas temporales

## <a name="configure-always-on-with-stretch-database"></a>Configurar AlwaysOn con Stretch Database
Si usa AlwaysOn con Stretch Database, debe asegurarse de que la clave maestra de base de datos esté disponible en las réplicas secundarias. Stretch Database usa la clave maestra de base de datos para proteger las credenciales que usa para conectarse a la base de datos remota de Azure.

Una vez que configure el grupo de disponibilidad AlwaysOn, ejecute el procedimiento almacenado **sp_control_dbmasterkey_password** en cada réplica secundaria y proporcione la contraseña de la base de datos habilitada para Stretch. Para más información, consulte [sp_control_dbmasterkey_password](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md). 

## <a name="configure-always-encrypted-with-stretch-database"></a>Configurar Always Encrypted con Stretch Database
Si desea usar Always Encrypted en conjunto con Stretch Database, debe configurar el cifrado de las columnas seleccionadas antes de habilitar Stretch Database en la tabla.

Si ya habilitó Stretch Database en la tabla y desea usar columnas de Always Encrypted, deberá hacer lo siguiente.
1.   Deshabilite Stretch Database en la tabla y devuelva los datos remotos desde Azure. Para obtener más información, vea [Deshabilitar Stretch Database y recuperar datos remotos](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).
2.   Configure Always Encrypted en las columnas seleccionadas.
3. Vuelva a habilitar Stretch Database en la tabla. Para obtener más información, vea [Habilitación de Stretch Database para una base de datos](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).

## <a name="configure-transparent-data-encryption-tde-with-stretch-database"></a>Configurar Cifrado de datos transparente (TDE) con Stretch Database

Si TDE está habilitado en la base de datos local, no se habilitará automáticamente en el extremo remoto de Stretch Database. Recuerde habilitar TDE en el extremo remoto después de habilitar Stretch en la base de datos.

## <a name="configure-temporal-tables-with-stretch-database"></a>Configurar tablas temporales con Stretch Database
Si usa tablas temporales, puede habilitar Stretch Database en la tabla de historial, pero no en la tabla actual.
-   Para instrucciones sobre cómo usar tablas temporales con Stretch Database, consulte [Administración de la retención de datos históricos en las tablas temporales con versiones del sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md).
-   Para filtrar las filas que se van a migrar desde la tabla de historial con una ventana deslizante, consulte [Seleccionar las filas que se van a migrar mediante una función de filtro](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).
