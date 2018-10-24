---
title: Copiar columnas de una tabla a otra (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- copying columns
- columns [SQL Server], copying
ms.assetid: 5f5e70dc-69f9-44b8-bc48-b5d51ac20d77
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3f51ff3b290fca3284a72f1b5ba1ea2a38ff0cbb
ms.sourcegitcommit: 110e5e09ab3f301c530c3f6363013239febf0ce5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2018
ms.locfileid: "48906045"
---
# <a name="copy-columns-from-one-table-to-another-database-engine"></a>Copiar columnas de una tabla a otra (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  En este tema se describe cómo copiar columnas de una tabla a otra, copiar solo la definición de la columna o copiar la definición y los datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para copiar columnas mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Cuando se copia una columna con el tipo de datos de alias desde una base de datos a otra, el tipo de datos de alias podría no estar disponible en la base de datos de destino. En ese caso, se asignará a la columna el tipo de datos de base más parecido que esté disponible en la base de datos.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>Para copiar definiciones de columna de una tabla a otra  
  
1.  Abra la tabla con columnas que quiere copiar y la tabla en la que la quiere copiar haciendo clic con el botón derecho en las tablas y, después, en **Diseño**.  
  
2.  Haga clic en la pestaña de la tabla cuyas columnas desea copiar y seleccione esas columnas.  
  
3.  En el menú **Edición** , haga clic en **Copiar**.  
  
4.  Haga clic en la pestaña de la tabla en la que desea copiar las columnas.  
  
5.  Seleccione la columna que desea que siga a las columnas insertadas y en el menú **Edición** , haga clic en **Pegar**.  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>Para copiar columnas de datos de una tabla a otra  
  
1.  Siga las instrucciones para copiar las definiciones de columna mencionadas anteriormente.  
  
    > [!NOTE]  
    >  Antes de empezar a copiar los datos de una tabla a otra, asegúrese de que los tipos de datos de las columnas de destino son compatibles con los tipos de datos de las columnas de origen.  
  
2.  Abra una nueva ventana del Editor de consultas. 

3.  Haga clic con el botón derecho en el Editor de consultas y, luego, haga clic en **Diseñar consulta en el editor**. 

4.  En el cuadro de diálogo **Agregar tabla** , seleccione la tabla de origen y destino, haga clic en **Agregar**y, luego, cierre el cuadro de diálogo **Agregar tabla** . 

5.  Haga clic con el botón derecho en un área abierta del Editor de consultas, seleccione **Cambiar tipo** y, luego, haga clic en **Insertar resultados**.  

6.  En el cuadro de diálogo **Elegir tabla de destino para insertar resultados** , seleccione la tabla de destino. 

7.  En la parte superior del Diseñador de consultas, haga clic en la columna de origen de la tabla de origen.

8. El Diseñador de consultas acaba de crear una consulta INSERT. Haga clic en Aceptar para ubicar la consulta en la ventana original del Editor de consultas.  

9.  Ejecute la consulta para insertar los datos desde la tabla de origen a la tabla de destino.

  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>Para copiar definiciones de columna de una tabla a otra  
  
1.  No puede copiar columnas individuales desde una tabla a otra tabla existente mediante instrucciones Transact-SQL. Sin embargo, puede crear una nueva tabla en el grupo de archivos predeterminado e insertar en ella las filas resultantes de la consulta mediante SELECT...INTO. Para obtener más información, vea [Cláusula INTO &#40;Transact-SQL&#41;](../../t-sql/queries/select-into-clause-transact-sql.md).  
  
#### <a name="to-copy-data-from-one-table-to-another"></a>Para copiar columnas de datos de una tabla a otra  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE TABLE dbo.EmployeeSales  
    ( BusinessEntityID   varchar(11) NOT NULL,  
      SalesYTD money NOT NULL  
    );  
    GO  
    INSERT INTO dbo.EmployeeSales  
        SELECT BusinessEntityID, SalesYTD   
        FROM Sales.SalesPerson;  
    GO  
    ```  
  
  
