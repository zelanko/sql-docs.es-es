---
title: "Configuración de operaciones de índice en paralelo | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index parallel operations [SQL Server]
- processors [SQL Server], parallel index operations
- max degree of parallelism option
- MAXDOP index option, parallel index operations
- parallel index operations [SQL Server]
ms.assetid: 8ec8c71e-5fc1-443a-92da-136ee3fc7f88
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3e68d3b1d6d08153e24ec3afdb5102e5c1ae6c46
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="configure-parallel-index-operations"></a>Configurar operaciones de índice en paralelo
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En este tema se define el grado máximo de paralelismo y se explica cómo modificar este valor en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. En los equipos multiprocesador que ejecutan [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise o superior, las instrucciones de índice pueden usar varios procesadores para realizar las operaciones de examen, ordenación e indización asociadas a la instrucción de índice, al igual que hacen otras consultas. El número de procesadores utilizados para ejecutar una sola instrucción de índice viene determinado por la opción de configuración [Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) , la carga de trabajo actual y las estadísticas de índices. La opción max degree of parallelism determina el número máximo de procesadores que se utilizarán en la ejecución de planes paralelos. Si [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] detecta que el sistema está ocupado, el grado de paralelismo de la operación de índice se reduce automáticamente antes de comenzar la ejecución de la instrucción. [!INCLUDE[ssDE](../../includes/ssde-md.md)] también puede reducir el grado de paralelismo si la columna de clave inicial de un índice sin particiones tiene un número limitado de valores distintos o la frecuencia de cada valor distinto varía significativamente.  
  
> [!NOTE]  
>  Las operaciones de índices en paralelo no están disponibles en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea Características compatibles con las ediciones de SQL Server 2016.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para establecer el grado máximo de paralelismo, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El número de procesadores que utiliza el optimizador de consultas suele proporcionar un rendimiento óptimo. No obstante, las operaciones como la creación, reconstrucción o eliminación de índices de gran tamaño utilizan una gran cantidad de recursos y pueden provocar la falta de recursos para otras aplicaciones y operaciones de base de datos durante la operación de índice. Cuando se produce este problema, se puede configurar manualmente el número máximo de procesadores que se emplean para ejecutar la instrucción de índice limitando el número de procesadores que se usarán para la operación de índice.  
  
-   La opción de índice MAXDOP reemplaza la opción de configuración max degree of parallelism solo para la consulta que especifica esta opción. En la tabla siguiente se muestran los valores enteros válidos que se pueden especificar con la opción de configuración max degree of parallelism y la opción de índice MAXDOP.  
  
    |Valor|Descripción|  
    |-----------|-----------------|  
    |0|Especifica que el servidor determina el número de CPU que se usan, según la carga de trabajo del sistema actual. Éste es el valor predeterminado y recomendado.|  
    |1|Suprime la generación de planes paralelos. La operación se ejecutará en serie.|  
    |2-64|Limita el número de procesadores al valor especificado. Puede que se utilicen menos procesadores, dependiendo de la carga de trabajo actual. Si especifica un valor superior al número de CPU disponibles, se utilizará el número real de CPU disponibles.|  
  
-   La ejecución de índices en paralelo y la opción de índice MAXDOP se aplican a las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes:  
  
    -   CREATE INDEX  
  
    -   ALTER INDEX REBUILD  
  
    -   DROP INDEX (esta opción solo se aplica a los clúster)  
  
    -   ALTER TABLE ADD (índice) CONSTRAINT  
  
    -   ALTER TABLE DROP (índice clúster) CONSTRAINT  
  
-   La opción de índice MAXDOP no se puede especificar en la instrucción ALTER INDEX REORGANIZE.  
  
-   Los requisitos de memoria de las operaciones de índices con particiones que requieren ordenación pueden ser mayores si el optimizador de consultas aplica grados de paralelismo a la operación de generación. Cuanto mayores sean los grados de paralelismo, mayor será el requisito de memoria. Para obtener más información, consulte [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla o la vista.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-index"></a>Para establecer el grado máximo de paralelismo en un índice  
  
1.  En el Explorador de objetos, haga clic en el signo más para expandir la base de datos que contiene la tabla en la que desea establecer el grado máximo de paralelismo para un índice.  
  
2.  Expanda la carpeta **Tablas** .  
  
3.  Haga clic en el signo más para expandir la tabla en la que desea establecer el grado máximo de paralelismo para un índice.  
  
4.  Expanda la carpeta **Índices** .  
  
5.  Haga clic con el botón derecho en el índice para el que quiere establecer el grado máximo de paralelismo y seleccione **Propiedades**.  
  
6.  Debajo de **Seleccionar una página**, seleccione **Opciones**.  
  
7.  Seleccione **Grado máximo de paralelismo**y, a continuación, escriba un valor entre 1 y 64.  
  
8.  Haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-existing-index"></a>Para establecer el grado máximo de paralelismo en un índice existente  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    /*Alters the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table so that, if the server has eight or more processors, the Database Engine will limit the execution of the index operation to eight or fewer processors.  
    */  
    ALTER INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor  
    REBUILD WITH (MAXDOP=8);   
    GO  
    ```  
  
 Para obtener más información, vea [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
#### <a name="set-max-degree-of-parallelism-on-a-new-index"></a>Establecer el grado máximo de paralelismo en un nuevo índice  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE INDEX IX_ProductVendor_NewVendorID   
    ON Purchasing.ProductVendor (BusinessEntityID)  
    WITH (MAXDOP=8);  
    GO  
    ```  
  
 Para obtener más información, vea [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
  

