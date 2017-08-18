---
title: "Configurar la opción de configuración del servidor Memoria mínima por consulta | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- memory [SQL Server], queries
- minimum query memory
- queries [SQL Server], memory
- min memory per query option
ms.assetid: ecd3fb79-b4a6-432f-9ef5-530e0d42d5a6
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e49ed68ce5e3f4621017db6cd09d2eec680b77f2
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="configure-the-min-memory-per-query-server-configuration-option"></a>Configurar la opción de configuración del servidor Memoria mínima por consulta
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo configurar la opción de configuración de servidor **memoria mínima por consulta** en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La opción de **min memory per query** especifica la cantidad mínima de memoria (en kilobytes) que se va a asignar para la ejecución de una consulta. Por ejemplo, si se establece el valor 2.048 KB para la opción **min memory per query** , se garantiza que la consulta va a obtener esa cantidad de memoria total, como mínimo. El valor predeterminado es 1.024 KB. El valor mínimo es 512 KB y el valor máximo es 2 147 483 647 KB (2 GB).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para configurar la opción de memoria mínima por consulta, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [Después de configurar la opción de memoria mínima por consulta](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El valor especificado en min memory per query tiene prioridad sobre la opción [index create memory](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md). Si cambia ambas opciones y el valor de index create memory es inferior al de min memory per query, aparecerá un mensaje de advertencia, pero se establecerá el valor. Durante la ejecución de la consulta recibirá otra advertencia similar.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Esta opción es avanzada y solo debe cambiarla un administrador de base de datos con experiencia o un técnico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la titulación apropiada.  
  
-   El procesador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta determinar la cantidad óptima de memoria para asignar a una consulta. La opción min memory per query permite al administrador especificar la cantidad mínima de memoria que recibirá cada consulta. Generalmente, las consultas reciben una cantidad mayor de memoria si tienen operaciones de orden y hash en un gran volumen de datos. Aumentar el valor de la opción min memory per query puede mejorar el rendimiento para algunas consultas de pequeño o mediano tamaño, pero podría aumentar la competición por los recursos de la memoria. La opción de min memory per query incluye memoria asignada para ordenar.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
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
  
```tsql  
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
  
## <a name="see-also"></a>Vea también  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Configure the index create memory Server Configuration Option](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)  
  
  

