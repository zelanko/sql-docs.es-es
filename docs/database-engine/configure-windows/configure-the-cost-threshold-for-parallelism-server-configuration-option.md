---
title: "Establecer la opción de configuración del servidor Umbral de costo para paralelismo | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: cost threshold for parallelism option
ms.assetid: dad21bee-fe28-41f6-9d2f-e6ababfaf9db
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f1896fc22ed586ecd532121300069c2a4d29a496
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="configure-the-cost-threshold-for-parallelism-server-configuration-option"></a>Establecer la opción de configuración del servidor Umbral de costo para paralelismo
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo establecer la opción de configuración del servidor **umbral de costo para paralelismo** en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La opción **Umbral de costo para paralelismo** permite especificar el umbral en el que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea y ejecuta planes paralelos para consultas. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea y ejecuta un plan paralelo para una consulta solo cuando el costo estimado para ejecutar un plan serie para la misma consulta es superior al valor establecido en **umbral de costo para paralelismo**. Este costo hace referencia a un costo estimado que es necesario para ejecutar el plan en serie en una configuración de hardware específica, y no es una unidad de tiempo. Puede establecer cualquier valor entre 0 y 32767 para la opción **umbral de costo para paralelismo** . El valor predeterminado es 5.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para configurar la opción de umbral de costo para paralelismo, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [Después de configurar la opción de umbral de costo para paralelismo](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Este costo hace referencia a una unidad de costo abstracta y no a una unidad de tiempo estimado. **cost threshold for parallelism** solo debe establecerse en multiprocesadores simétricos.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] omite el valor de **umbral de costo para paralelismo** en las siguientes condiciones:  
  
    -   El equipo tiene solo un procesador lógico.  
  
    -   Solo hay disponible un procesador lógico para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debido a la opción de configuración de la **máscara de afinidad** .  
  
    -   La opción **grado máximo de paralelismo** está establecida en 1.  
  
 Un procesador lógico es la unidad básica de hardware de procesador que permite al sistema operativo enviar una tarea o ejecutar un contexto de subproceso. Cada procesador lógico puede ejecutar solo un contexto de subproceso a la vez. El núcleo del procesador es el conjunto de circuitos que proporciona capacidad para descodificar y ejecutar instrucciones. El núcleo de un procesador puede contener uno o varios procesadores lógicos. La siguiente consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] se puede utilizar para obtener información de CPU para el sistema.  
  
```  
SELECT (cpu_count / hyperthread_ratio) AS PhysicalCPUs,   
cpu_count AS logicalCPUs   
FROM sys.dm_os_sys_info  
```  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Esta opción es avanzada y solo debe cambiarla un administrador de base de datos con experiencia o un técnico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la titulación apropiada.  
  
-   En determinados casos, puede elegirse un plan paralelo aunque el costo del plan de la consulta sea inferior al valor actual de **umbral de costo para paralelismo** . Esto se debe a que la decisión de utilizar un plan serie o un plan paralelo se basa en un costo estimado proporcionado antes de finalizar la optimización completa.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 De forma predeterminada, todos los usuarios tienen permisos de ejecución en **sp_configure** sin ningún parámetro o solo con el primero. Para ejecutar **sp_configure** con ambos parámetros y cambiar una opción de configuración, o para ejecutar la instrucción RECONFIGURE, un usuario debe tener el permiso ALTER SETTINGS en el servidor. Los roles fijos de servidor **sysadmin** y **serveradmin** tienen el permiso ALTER SETTINGS de forma implícita.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-configure-the-cost-threshold-for-parallelism-option"></a>Para configurar la opción de umbral de costo para paralelismo  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en un servidor y seleccione **Propiedades**.  
  
2.  Haga clic en el nodo **Avanzado** .  
  
3.  En **Paralelismo**, cambie la opción **CostThresholdForParallelism** al valor que desee. Escriba o seleccione un valor entre 0 y 32767.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-configure-the-cost-threshold-for-parallelism-option"></a>Para configurar la opción de umbral de costo para paralelismo  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para establecer el valor de la opción de `cost threshold for parallelism` en `10`.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'cost threshold for parallelism', 10 ;  
GO  
RECONFIGURE  
GO  
```  
  
 Para obtener más información, vea [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Seguimiento: Después de configurar la opción de umbral de costo para paralelismo  
 La configuración surte efecto inmediatamente, sin necesidad de reiniciar el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Configurar operaciones de índice en paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md)   
 [Sugerencias de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [affinity mask (opción de configuración del servidor)](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
