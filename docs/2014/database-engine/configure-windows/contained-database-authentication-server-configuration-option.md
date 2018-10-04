---
title: contained database authentication (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- contained_database_authentication_TSQL
- contained database authentication
helpviewer_keywords:
- contained database, enabling
- contained database authentication option
ms.assetid: b80768d2-ac20-4035-a335-d9adb74b3f6e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5ea76cc1902f96f49218b2c2e550b601822ca1a3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130605"
---
# <a name="contained-database-authentication-server-configuration-option"></a>contained database authentication (opción de configuración del servidor)
  Utilice la opción **autenticación de base de datos independiente** para habilitar las bases de datos independientes en la instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Esta opción de servidor permite controlar la **autenticación de base de datos independiente**.  
  
-   Cuando la opción **autenticación de base de datos independiente** está desactivada (0) para la instancia, no se pueden crear bases de datos independientes ni tampoco adjuntarse a [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Cuando la opción **autenticación de base de datos independiente** está activada (1) para la instancia, se pueden crear bases de datos independientes y, también, adjuntarse a [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Una base de datos independiente incluye todos los metadatos y la configuración de la base de datos necesarios para definirla, y no tiene dependencias de configuración en la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] donde esté instalada. Los usuarios pueden conectarse a la base de datos sin autenticar un inicio de sesión en el nivel [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Aislar la base de datos del Motor de base de datos permite moverla fácilmente a otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al incluir toda la configuración de la base de datos en la base de datos, se permite que sus propietarios administren toda su configuración. Para obtener más información acerca de las bases de datos independientes, vea [Contained Databases](../../relational-databases/databases/contained-databases.md).  
  
 Si una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene bases de datos independientes, la configuración de **autenticación de base de datos independiente** se puede establecer en 0 mediante el uso de la instrucción **RECONFIGURE WITH OVERRIDE** . Al establecer **autenticación de base de datos independiente** en 0 se deshabilitará la autenticación de base de datos independiente para las bases de datos independientes.  
  
> [!IMPORTANT]  
>  Cuando se habilitan las bases de datos independientes, los usuarios de la base de datos con el permiso ALTER ANY USER, como los miembros de los roles de base de datos db_owner y db_accessadmin, pueden otorgar acceso a las bases de datos y, al hacerlo, otorgan acceso a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esto significa que el control sobre el acceso al servidor ya no se limita a los miembros con roles fijos de sysadmin y securityadmin, y a los inicios de sesión con el permiso ALTER ANY LOGIN y de servidor de CONTROL de nivel de servidor. Antes de permitir las bases de datos independientes, debe entender los riesgos asociados a ellas. Para más información, vea [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md).  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se habilitan las bases de datos independientes en la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
```tsql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
