---
title: Configurar una base de datos reflejada para usar la propiedad Trustworthy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- TRUSTWORTHY database option
- mirror database [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 6993b076-78ef-453e-b0ea-e341b8e5ee3e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ee6ecf05e0ecff96b60f8ffd586461989cb9e151
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47743133"
---
# <a name="set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql"></a>Configurar una base de datos reflejada para usar la propiedad Trustworthy (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Cuando se realiza una copia de seguridad de una base de datos, la propiedad TRUSTWORTHY de la base de datos se establece en OFF. Por lo tanto, TRUSTWORTHY siempre está en OFF en una nueva base de datos reflejada. Si la base de datos necesita marcarse como de confianza después de una conmutación por error, es necesario realizar pasos adicionales de configuración después de iniciar la creación de reflejo.  
  
> [!NOTE]  
>  Para obtener información sobre esta propiedad de base de datos, vea [Propiedad de base de datos TRUSTWORTHY](../../relational-databases/security/trustworthy-database-property.md).  
  
## <a name="procedure"></a>Procedimiento  
  
#### <a name="to-setup-a-mirror-database-to-use-the-trustworthy-property"></a>Para configurar una base de datos reflejada para usar la propiedad Trustworthy  
  
1.  En la instancia del servidor principal, compruebe que la base de datos principal tiene habilitada la propiedad Trustworthy.  
  
    ```  
    SELECT name, database_id, is_trustworthy_on FROM sys.databases   
    ```  
  
     Para obtener más información, vea [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).  
  
2.  Después de iniciar la creación de reflejo, compruebe que la base de datos es actualmente la base de datos principal, que la sesión utiliza un modo de funcionamiento sincrónico y que la sesión ya está sincronizada.  
  
    ```  
    SELECT database_id, mirroring_role, mirroring_safety_level_desc, mirroring_state_desc FROM sys.database_mirroring  
    ```  
  
     Para obtener más información, vea [sys.database_mirroring &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md).  
  
3.  Una vez sincronizada la sesión de creación de reflejo, realice una conmutación manual por error a la base de datos reflejada.  
  
     Puede hacer esto en SQL Server Management Studio o mediante Transact-SQL:  
  
    -   [Realizar manualmente la conmutación por error de una sesión de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [Realizar una conmutación por error manualmente de una sesión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/manually-fail-over-a-database-mirroring-session-transact-sql.md)  
  
4.  Active la propiedad de base de datos TRUSTWORTHY mediante el siguiente comando ALTER DATABASE:  
  
    ```  
    ALTER DATABASE <database_name> SET TRUSTWORTHY ON  
    ```  
  
     Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
5.  Si lo desea, realice la conmutación manual por error para regresar a la base de datos principal original.  
  
6.  Opcionalmente, cambie al modo asincrónico de alto rendimiento estableciendo SAFETY en OFF y asegurándose de que WITNESS también se ha establecido en OFF.  
  
     En Transact-SQL:  
  
    -   [Cambiar la seguridad de las transacciones en una sesión de creación de reflejo de la base de datos &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)  
  
    -   [Quitar el testigo de una sesión de creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
     En SQL Server Management Studio:  
  
    -   [Establecer una sesión de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
## <a name="see-also"></a>Ver también  
 [Propiedad de base de datos TRUSTWORTHY](../../relational-databases/security/trustworthy-database-property.md)   
 [Establecer una base de datos reflejada cifrada](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)  
  
  
