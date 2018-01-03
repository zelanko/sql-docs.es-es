---
title: "Establecer la opción de configuración del servidor Grado máximo de paralelismo | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- parallel queries [SQL Server]
- processors [SQL Server], parallel queries
- number of processors for parallel queries
- max degree of parallelism option
- MaxDop
ms.assetid: 86b65bf1-a6a1-4670-afc0-cdfad1558032
caps.latest.revision: "33"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 1dfcaed696576757a527cffaae753028587d4fe3
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="configure-the-max-degree-of-parallelism-server-configuration-option"></a>Establecer la opción de configuración del servidor Grado máximo de paralelismo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  En este tema se describe cómo establecer la opción de configuración del servidor **grado máximo de paralelismo (MAXDOP)** en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Cuando una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en un equipo con más de un microprocesador o CPU, detecta el mejor grado de paralelismo, es decir, el número de procesadores que se emplea para ejecutar una única instrucción en cada ejecución de planes en paralelo. Puede utilizar la opción **max degree of parallelism** (grado máximo de paralelismo) para limitar el número de procesadores que debe utilizarse en la ejecución de planes en paralelo. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considera los planes de ejecución en paralelo para las consultas, las operaciones de lenguaje de definición de datos (DDL) de índice, la inserción en paralelo, la modificación de columna en línea, la colección de estadísticas en paralelo y el rellenado de cursor estático y controlado por conjuntos de claves.

##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si el valor de la opción affinity mask no es el predeterminado, es posible que se limite el número de procesadores disponibles para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en sistemas de multiproceso simétrico (SMP).  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Esta opción es avanzada y solo debe cambiarla un administrador de base de datos con experiencia o un técnico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la titulación apropiada.  
  
-   Para que el servidor pueda determinar el Grado máximo de paralelismo, establezca esta opción en 0, que es el valor predeterminado. Si se establece el grado máximo de paralelismo en 0, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede usar todos los procesadores disponibles hasta un número de 64. Para suprimir la generación de planes paralelos, establezca la opción **max degree of parallelism** en 1. Establezca el valor en un número de 1 a 32.767 para especificar el número máximo de núcleos de procesador que puede usar una única ejecución de consulta. Si se especifica un valor superior al número de procesadores disponibles, se utilizará el número real de procesadores disponibles. Si el equipo tiene solo un procesador, el valor de **grado máximo de paralelismo** se pasará por alto.  
  
-   Puede omitir el valor de la opción max degree of parallelism especificando la sugerencia de consulta MAXDOP en la instrucción de la consulta. Para obtener más información, vea [Sugerencias de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
-   Las operaciones de índice que crean o vuelven a generar un índice, o que eliminan un índice clúster, pueden consumir recursos de forma intensiva. Puede omitir el valor de la opción max degree of parallelism para operaciones de índice especificando la opción de índice MAXDOP en la instrucción del índice. El valor de MAXDOP se aplica a la instrucción en tiempo de ejecución y no se almacena en los metadatos del índice. Para obtener más información, vea [Configurar operaciones de índice en paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
-   Además de las operaciones de consultas e índices, esta opción también controla el paralelismo de DBCC CHECKTABLE, DBCC CHECKDB y DBCC CHECKFILEGROUP. Puede deshabilitar los planes de ejecución en paralelo de estas instrucciones mediante el uso de la marca de seguimiento 2528. Para obtener más información, vea [Marcas de seguimiento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).

###  <a name="Guidelines"></a> Instrucciones  
Use las siguientes directrices al configurar el valor de configuración del servidor de **grado máximo de paralelismo**:

||||
|----------------|-----------------|-----------------|
|Servidor con un solo nodo NUMA|Menos de 8 procesadores lógicos|Mantener MAXDOP en ese número de procesadores lógicos o por debajo de este|
|Servidor con un solo nodo NUMA|Más de 8 procesadores lógicos|Mantener MAXDOP en 8|
|Servidor con varios nodos NUMA|Menos de 8 procesadores lógicos por nodo NUMA|Mantener MAXDOP en ese número de procesadores lógicos por nodo NUMA o por debajo de este|
|Servidor con varios nodos NUMA|Más de 8 procesadores lógicos por nodo NUMA|Mantener MAXDOP en 8|
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
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
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para configurar la opción `max degree of parallelism` en `8`.  
  
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
  
 Para obtener más información, vea [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="FollowUp"></a> Seguimiento: Después de configurar la opción de grado máximo de paralelismo  
 La configuración surte efecto inmediatamente, sin necesidad de reiniciar el servidor.  
  
## <a name="see-also"></a>Ver también  
 [affinity mask (opción de configuración del servidor)](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md) [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKFILEGROUP &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)   
 [Configurar operaciones de índice en paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md)   
 [Sugerencias de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md) [Establecer opciones de índice](../../relational-databases/indexes/set-index-options.md)  
 [Recommendations and guidelines for the "max degree of parallelism" configuration option in SQL Server](http://support.microsoft.com/help/2806535) (Recomendaciones y directrices relativas a la opción de configuración "grado máximo de paralelismo" en SQL Server)
  
  
