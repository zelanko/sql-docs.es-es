---
title: Configurar la opción de configuración del servidor Memoria mínima por consulta | Microsoft Docs
ms.custom: ''
ms.date: 11/24/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- memory [SQL Server], queries
- minimum query memory
- queries [SQL Server], memory
- min memory per query option
- min memory grant
ms.assetid: ecd3fb79-b4a6-432f-9ef5-530e0d42d5a6
caps.latest.revision: 28
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e68c2617af6a2828e1183733ee53fdd142747f66
ms.sourcegitcommit: 155f053fc17ce0c2a8e18694d9dd257ef18ac77d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/06/2018
ms.locfileid: "34811919"
---
# <a name="configure-the-min-memory-per-query-server-configuration-option"></a>Configurar la opción de configuración del servidor Memoria mínima por consulta
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo configurar la opción de configuración de servidor **memoria mínima por consulta** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La opción de **min memory per query** especifica la cantidad mínima de memoria (en kilobytes) que se va a asignar para la ejecución de una consulta. Esto también se conoce como concesión de memoria mínima. Por ejemplo, si se establece el valor 2.048 KB para la opción **min memory per query** , se garantiza que la consulta va a obtener esa cantidad de memoria total, como mínimo. El valor predeterminado es 1.024 KB. El valor mínimo es 512 KB y el valor máximo es 2 147 483 647 KB (2 GB).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para configurar la opción de memoria mínima por consulta, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [Después de configurar la opción de memoria mínima por consulta](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El valor especificado en memoria mínima por consulta tiene prioridad sobre la opción [memoria para creación de índices](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md). Si cambia ambas opciones y el valor de index create memory es inferior al de min memory per query, aparecerá un mensaje de advertencia, pero se establecerá el valor. Durante la ejecución de la consulta, recibirá otra advertencia similar.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Esta opción es avanzada y solo debe cambiarla un administrador de base de datos con experiencia o un profesional certificado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   El procesador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta determinar la cantidad óptima de memoria para asignar a una consulta. La opción min memory per query permite al administrador especificar la cantidad mínima de memoria que recibirá cada consulta. Generalmente, las consultas reciben una cantidad mayor de memoria si tienen operaciones de orden y hash en un volumen de datos grande. Aumentar el valor de la opción min memory per query puede mejorar el rendimiento para algunas consultas de pequeño o mediano tamaño, pero podría aumentar la competición por los recursos de la memoria. La opción de memoria mínima por consulta incluye memoria asignada para las operaciones de ordenación.  

-    No establezca un valor demasiado alto para la opción de configuración del servidor Memoria mínima por consulta, especialmente en sistemas muy ocupados, ya que la consulta tendrá que esperar<sup>1</sup> hasta que pueda garantizar la memoria mínima solicitada o hasta que se supere el valor especificado en la opción de configuración del servidor Espera de consulta. Si hay más memoria disponible que el valor mínimo especificado requerido para ejecutar la consulta, se permite que la consulta utilice la memoria adicional, siempre y cuando pueda utilizar la memoria de forma eficaz.     

<sup>1</sup> En este caso, el tipo de espera normalmente es RESOURCE_SEMAPHORE. Para obtener más información, vea [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).

###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 De forma predeterminada, todos los usuarios tienen permisos de ejecución en **sp_configure** sin ningún parámetro o solo con el primero. Para ejecutar **sp_configure** con ambos parámetros y cambiar una opción de configuración, o para ejecutar la instrucción RECONFIGURE, un usuario debe tener el permiso ALTER SETTINGS en el servidor. Los roles fijos de servidor **sysadmin** y **serveradmin** tienen el permiso ALTER SETTINGS de forma implícita.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>Para configurar la opción de memoria mínima por consulta  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor y seleccione **Propiedades**.  
  
2.  Haga clic en el nodo **Memoria** .  
  
3.  En el cuadro **Cantidad mínima de memoria por consulta** , especifique la cantidad mínima de memoria (en kilobytes) que se va a asignar para la ejecución de una consulta.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>Para configurar la opción de memoria mínima por consulta  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para establecer el valor de la opción de `min memory per query` en `3500` kB.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'min memory per query', 3500 ;  
GO  
RECONFIGURE;  
GO    
```  
  
##  <a name="FollowUp"></a> Seguimiento: Después de configurar la opción de memoria mínima por consulta  
 La configuración surte efecto inmediatamente, sin necesidad de reiniciar el servidor.  
  
## <a name="see-also"></a>Ver también  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Establecer la opción de configuración del servidor Memoria para creación de índices](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)     
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
 [sys.dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)
  
  
