---
title: "Crear restricciones CHECK | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-tables"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "restricciones de tabla [SQL Server]"
  - "adjuntar restricciones CHECK"
  - "columnas [SQL Server], restricciones"
  - "restricciones [SQL Server], check"
  - "restricciones CHECK, adjuntar"
ms.assetid: b8756304-9454-4d39-996a-64516831b7df
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Crear restricciones CHECK
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Puede crear una restricción CHECK en una tabla para especificar los valores de datos aceptables en una o más columnas de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para crear una restricción CHECK nueva con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere permisos ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### Para crear una restricción CHECK nueva  
  
1.  En el **Explorador de objetos**, expanda la tabla a la que quiera agregar una restricción CHECK, haga clic con el botón derecho en **Restricciones** y haga clic en **Nueva restricción**.  
  
2.  En el cuadro de diálogo **Comprobar restricciones**, haga clic en el campo **Expresión** y, luego, en los puntos suspensivos **(…)**.  
  
3.  En el cuadro de diálogo **Expresión de restricción CHECK** , escriba expresiones SQL para la restricción CHECK. Por ejemplo, para limitar las entradas de la columna `SellEndDate` de la tabla `Product` a un valor que sea mayor o igual que la fecha de la columna `SellStartDate` o que sea un valor NULL, escriba:  
  
    ```  
    SellEndDate >= SellStartDate OR SellEndDate IS NULL  
    ```  
  
     O bien, para exigir que las entradas que se escriben en la columna `zip` tengan 5 dígitos, escriba:  
  
    ```  
    zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
    ```  
  
    > [!NOTE]  
    >  Asegúrese de que escribe los valores de restricción no numéricos entre comillas sencillas (').  
  
4.  Haga clic en **Aceptar**.  
  
5.  En la categoría **Identidad**, puede cambiar el nombre de la restricción CHECK y agregar una descripción (propiedad extendida) para la restricción.  
  
6.  En la categoría **Diseñador de tablas** , puede definir cuándo debe exigirse la restricción.  
  
    |**Para:**|**Seleccione Sí en los campos siguientes:**|  
    |-------------|---------------------------------------------|  
    |Pruebe la restricción en los datos existentes antes de que se creara la restricción|**Comprobar los datos existentes al crear o habilitar**|  
    |Exigir la restricción siempre que se produzca una operación de replicación en esta tabla|**Exigir para replicación**|  
    |Exigir la restricción siempre que se inserte o actualice una fila de esta tabla|**Exigir para comandos INSERT y UPDATE**|  
  
7.  Haga clic en **Cerrar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para crear una restricción CHECK nueva  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    ALTER TABLE dbo.DocExc   
       ADD ColumnD int NULL   
       CONSTRAINT CHK_ColumnD_DocExc   
       CHECK (ColumnD > 10 AND ColumnD < 50);  
    GO  
    -- Adding values that will pass the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (49);  
    GO  
    -- Adding values that will fail the check constraint  
    INSERT INTO dbo.DocExc (ColumnD) VALUES (55);  
    GO  
  
    ```  
  
 Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  