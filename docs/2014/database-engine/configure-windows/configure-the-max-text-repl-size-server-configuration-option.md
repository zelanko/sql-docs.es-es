---
title: Establecer la opción de configuración del servidor Tamaño de replicación de texto máximo | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- max text repl size option
ms.assetid: 3056cf64-621d-4996-9162-3913f6bc6d5b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e55268f499069fb6714aa07944997e1e92e7fc23
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62811579"
---
# <a name="configure-the-max-text-repl-size-server-configuration-option"></a>Establecer la opción de configuración del servidor Tamaño de replicación de texto máximo
  En este tema se describe cómo establecer la opción de configuración del servidor **tamaño de replicación de texto máximo** en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La opción de **tamaño de replicación de texto máximo** especifica el tamaño máximo (en bytes) `varchar(max)`de `nvarchar(max)`los `varbinary(max)`datos `xml`de `text`, `image` `ntext`,,,, y que se pueden agregar a una columna replicada o a una columna capturada en una sola instrucción INSERT, Update, WRITETEXT o UPDATETEXT. El valor predeterminado es 65 536 bytes. Un valor predeterminado de -1 indica que no hay límite de tamaño, excepto el impuesto por el tipo de datos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para configurar la opción de tamaño de replicación de texto máximo, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [después de configurar la opción de tamaño de replicación de texto máximo](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Esta opción se aplica a la replicación transaccional y a la captura de datos modificados. Cuando un servidor se configura para la replicación transaccional y la captura de datos modificados, el valor especificado se aplica a ambas características. La replicación de instantáneas y la replicación de mezcla hacen caso omiso de esta opción.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 De forma predeterminada, todos los usuarios tienen permisos de ejecución en **sp_configure** sin ningún parámetro o solo con el primero. Para ejecutar **sp_configure** con ambos parámetros y cambiar una opción de configuración, o para ejecutar la instrucción RECONFIGURE, un usuario debe tener el permiso ALTER SETTINGS en el servidor. Los roles fijos de servidor **sysadmin** y **serveradmin** tienen el permiso ALTER SETTINGS de forma implícita.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-configure-the-max-text-repl-size-option"></a>Para configurar la opción de tamaño de replicación de texto máximo  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor y seleccione **Propiedades**.  
  
2.  Haga clic en el nodo **Avanzado** .  
  
3.  En **Varios**, cambie la opción **Tamaño de replicación de texto máximo** al valor que desee.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-configure-the-max-text-repl-size-option"></a>Para configurar la opción de tamaño de replicación de texto máximo  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para configurar la opción `max text repl size` en `-1`.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;   
RECONFIGURE ;   
GO  
EXEC sp_configure 'max text repl size', -1 ;   
GO  
RECONFIGURE;   
GO  
  
```  
  
 Para obtener más información, vea [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="follow-up-after-you-configure-the-max-text-repl-size-option"></a><a name="FollowUp"></a> Seguimiento: después de configurar la opción de tamaño de replicación de texto máximo  
 La configuración surte efecto inmediatamente, sin necesidad de reiniciar el servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Replicación de SQL Server](../../relational-databases/replication/sql-server-replication.md)   
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)   
 [UPDATETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/updatetext-transact-sql)   
 [WRITETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/writetext-transact-sql)  
  
  
