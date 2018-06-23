---
title: Copiar columnas de una tabla a otra (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- copying columns
- columns [SQL Server], copying
ms.assetid: 5f5e70dc-69f9-44b8-bc48-b5d51ac20d77
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 59fb6a9126b9467c8016082e6f4e5fab29b23c96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108291"
---
# <a name="copy-columns-from-one-table-to-another-database-engine"></a>Copiar columnas de una tabla a otra (motor de base de datos)
  En este tema se describe cómo copiar columnas de una tabla a otra, copiar solo la definición de la columna o copiar la definición y los datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para copiar columnas mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
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
  
2.  En el Explorador de objetos, haga clic con el botón secundario en **Vista** nodo y a continuación haga clic en **Nueva vista**.  
  
3.  En el menú **Diseñador de consultas** , seleccione **Cambiar tipo**y, a continuación, haga clic en **Insertar resultados**.  
  
4.  En el cuadro de diálogo **Elegir tabla de destino para Insertar resultados** , seleccione la tabla a la que desea copiar los datos y, a continuación, elija **Aceptar**.  
  
     Si va a copiar datos dentro de una tabla, puede agregar la tabla de origen como tabla de destino.  
  
    > [!NOTE]  
    >  El**Diseñador de consultas** no puede determinar con antelación las tablas y las vistas que se pueden actualizar. Por tanto, la lista de tablas del cuadro de diálogo **Elegir tabla de destino para Insertar resultados** mostrará todas las tablas y las vistas disponibles en la conexión de datos que está consultando, incluidas aquellas en las que no puede copiar filas.  
  
5.  Haga clic con el botón secundario en el cuerpo del panel Diagrama y, en el menú contextual, haga clic en **Agregar tabla a diagrama**.  
  
6.  En el cuadro de diálogo **Agregar tabla** , seleccione cada una de las tablas cuyos datos desea copiar, haga clic en **Agregar**y, a continuación, en **Cerrar**.  
  
     Las tablas aparecen en el panel Diagrama en forma abreviada.  
  
7.  En las tablas abreviadas, active las casillas de todas las columnas de las que desea copiar datos.  
  
8.  En el panel Criterios, en la columna **Anexar** , elija para cada columna de destino una columna de la que desea copiar datos.  
  
9. Indique las filas que desea copiar especificando condiciones de búsqueda en el panel Criterios. Para obtener más información, vea [Especificar condiciones de búsqueda &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md).  
  
     Si no especifica ninguna condición de búsqueda, se copiarán todas las filas de la tabla de origen en la tabla de destino.  
  
10. Si desea copiar información de resumen, especifique opciones de **Agrupar por** . Para obtener más información, vea [Resumir o agregar los valores de todas las filas de una tabla &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools.md).  
  
11. Haga clic en el botón **Ejecutar SQL** para ejecutar la consulta.  
  
     Cuando se ejecuta una consulta de inserción de resultados, los resultados no se incluyen en el [panel Resultados](../../ssms/visual-db-tools/results-pane-visual-database-tools.md). En su lugar, aparece un mensaje que indica cuántas filas se han copiado.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-copy-column-definitions-from-one-table-to-another"></a>Para copiar definiciones de columna de una tabla a otra  
  
1.  No puede copiar columnas individuales desde una tabla a otra tabla existente mediante instrucciones Transact-SQL. Sin embargo, puede crear una nueva tabla en el grupo de archivos predeterminado e insertar en ella las filas resultantes de la consulta mediante SELECT...INTO. Para obtener más información, vea [Cláusula INTO &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-into-clause-transact-sql).  
  
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
  
  
