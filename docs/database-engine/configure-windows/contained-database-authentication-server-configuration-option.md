---
title: contained database authentication (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- contained database, enabling
- contained database authentication option
ms.assetid: b80768d2-ac20-4035-a335-d9adb74b3f6e
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2fc3dd9e41148919062fa4408e696a2f4e1a7d2a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="contained-database-authentication-server-configuration-option"></a>contained database authentication (opción de configuración del servidor)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Utilice la opción **autenticación de base de datos independiente** para habilitar las bases de datos independientes en la instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Esta opción de servidor permite controlar la **autenticación de base de datos independiente**.  
  
-   Cuando la opción **autenticación de base de datos independiente** está desactivada (0) para la instancia, no se pueden crear bases de datos independientes ni tampoco adjuntarse a [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Cuando la opción **autenticación de base de datos independiente** está activada (1) para la instancia, se pueden crear bases de datos independientes y, también, adjuntarse a [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Una base de datos independiente incluye todos los metadatos y la configuración de la base de datos necesarios para definirla, y no tiene dependencias de configuración en la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] donde esté instalada. Los usuarios pueden conectarse a la base de datos sin autenticar un inicio de sesión en el nivel [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Aislar la base de datos del Motor de base de datos permite moverla fácilmente a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al incluir toda la configuración de la base de datos en la base de datos, se permite que sus propietarios administren toda su configuración. Para obtener más información acerca de las bases de datos independientes, vea [Contained Databases](../../relational-databases/databases/contained-databases.md).  

> [!NOTE]
> Las bases de datos independientes siempre están habilitadas para [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] y [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] no se pueden deshabilitar.
  
 Si una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene bases de datos independientes, la configuración de **autenticación de base de datos independiente** se puede establecer en 0 mediante el uso de la instrucción **RECONFIGURE WITH OVERRIDE** . Al establecer **autenticación de base de datos independiente** en 0 se deshabilitará la autenticación de base de datos independiente para las bases de datos independientes.  
  
> [!IMPORTANT]  
>  Cuando se habilitan las bases de datos independientes, los usuarios de la base de datos con el permiso ALTER ANY USER, como los miembros de los roles de base de datos db_owner y db_accessadmin, pueden otorgar acceso a las bases de datos y, al hacerlo, otorgan acceso a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esto significa que el control sobre el acceso al servidor ya no se limita a los miembros con roles fijos de sysadmin y securityadmin, y a los inicios de sesión con el permiso ALTER ANY LOGIN y de servidor de CONTROL de nivel de servidor. Antes de permitir las bases de datos independientes, debe entender los riesgos asociados a ellas. Para más información, vea [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se habilitan las bases de datos independientes en la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
```sql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
