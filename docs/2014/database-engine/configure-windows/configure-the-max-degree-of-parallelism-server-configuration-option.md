---
title: Establecer la opción de configuración del servidor Grado máximo de paralelismo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parallel queries [SQL Server]
- processors [SQL Server], parallel queries
- number of processors for parallel queries
- max degree of parallelism option
ms.assetid: 86b65bf1-a6a1-4670-afc0-cdfad1558032
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 46598cf66c80d07383fb033436bbe1792b1eec64
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62786964"
---
# <a name="configure-the-max-degree-of-parallelism-server-configuration-option"></a>Establecer la opción de configuración del servidor Grado máximo de paralelismo
  En este tema se describe cómo configurar el `max degree of parallelism` opción de configuración de servidor en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Cuando una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en un equipo con más de un microprocesador o CPU, detecta el mejor grado de paralelismo, es decir, el número de procesadores que se emplea para ejecutar una única instrucción en cada ejecución de planes en paralelo. Puede utilizar la opción `max degree of parallelism` para limitar el número de procesadores utilizados en la ejecución de planes paralelos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera los planes de ejecución en paralelo para las consultas, las operaciones de lenguaje de definición de datos (DDL) de índice y el rellenado de cursor estático y controlado por conjunto de claves.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para configurar el grado máximo de paralelismo opción, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Seguimiento:**  [Después de configurar la opción max degree of parallelism](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si el valor de la opción affinity mask no es el predeterminado, es posible que se limite el número de procesadores disponibles para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en sistemas de multiproceso simétrico (SMP).  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Esta opción es avanzada y solo debe cambiarla un administrador de base de datos con experiencia o un técnico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la titulación apropiada.  
  
-   Para que el servidor pueda determinar el Grado máximo de paralelismo, establezca esta opción en 0, que es el valor predeterminado. Si se establece el grado máximo de paralelismo en 0, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede usar todos los procesadores disponibles hasta un número de 64. Para suprimir la generación del plan paralelo, establezca `max degree of parallelism` en 1. Establezca el valor en un número de 1 a 32.767 para especificar el número máximo de núcleos de procesador que puede usar una única ejecución de consulta. Si se especifica un valor superior al número de procesadores disponibles, se utilizará el número real de procesadores disponibles. Si el equipo tiene solo un procesador, se omite el valor de `max degree of parallelism`.  
  
-   Puede omitir el valor de la opción max degree of parallelism especificando la sugerencia de consulta MAXDOP en la instrucción de la consulta. Para obtener más información, vea [Sugerencias de consulta &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query).  
  
-   Las operaciones de índice que crean o vuelven a generar un índice, o que eliminan un índice clúster, pueden consumir recursos de forma intensiva. Puede omitir el valor de la opción max degree of parallelism para operaciones de índice especificando la opción de índice MAXDOP en la instrucción del índice. El valor de MAXDOP se aplica a la instrucción en tiempo de ejecución y no se almacena en los metadatos del índice. Para obtener más información, vea [Configurar operaciones de índice en paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
-   Además de las operaciones de consultas e índices, esta opción también controla el paralelismo de DBCC CHECKTABLE, DBCC CHECKDB y DBCC CHECKFILEGROUP. Puede deshabilitar los planes de ejecución en paralelo de estas instrucciones mediante el uso de la marca de seguimiento 2528. Para obtener más información, vea [Marcas de seguimiento &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 De forma predeterminada, todos los usuarios tienen permisos de ejecución en **sp_configure** sin ningún parámetro o solo con el primero. Para ejecutar **sp_configure** con ambos parámetros y cambiar una opción de configuración, o para ejecutar la instrucción RECONFIGURE, un usuario debe tener el permiso ALTER SETTINGS en el servidor. Los roles fijos de servidor **sysadmin** y **serveradmin** tienen el permiso ALTER SETTINGS de forma implícita.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>Para configurar la opción de grado máximo de paralelismo  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en un servidor y seleccione **Propiedades**.  
  
2.  Haga clic en el nodo **Avanzado** .  
  
3.  En el cuadro **Grado máximo de paralelismo** , seleccione el número máximo de procesadores que se usarán en la ejecución de planes paralelos.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>Para configurar la opción de grado máximo de paralelismo  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para configurar la opción `max degree of parallelism` en `8`.  
  
```sql  
USE AdventureWorks2012 ;  
GO   
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
EXEC sp_configure 'max degree of parallelism', 8;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
```  
  
 Para obtener más información, vea [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Seguimiento: Después de configurar la opción max degree of parallelism  
 La configuración surte efecto inmediatamente, sin necesidad de reiniciar el servidor.  
  
## <a name="see-also"></a>Vea también  
 [affinity mask (opción de configuración del servidor)](affinity-mask-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checktable-transact-sql)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [DBCC CHECKFILEGROUP &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql)   
 [Configurar operaciones de índice en paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md)   
 [Sugerencias de consulta &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [Establecer opciones de índice](../../relational-databases/indexes/set-index-options.md)  
  
  
