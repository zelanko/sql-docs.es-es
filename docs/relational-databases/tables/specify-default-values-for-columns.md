---
title: Especificar valores predeterminados para las columnas | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- columns [SQL Server], defaults
- default values
ms.assetid: 64514aed-b846-407b-992e-cf813f9a1a91
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 956e23e61cb97d5d1adecf4a06f40f734da42948
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="specify-default-values-for-columns"></a>Especificar valores predeterminados para las columnas
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Puede especificar un valor predeterminado que se escribirá en la columna de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Si no asigna un valor predeterminado y el usuario deja la columna en blanco, entonces:  
  
-   Si estableció la opción de permitir valores NULL, se insertará NULL en la columna.  
  
-   Si no se establece la opción para permitir valores NULL, la columna permanecerá en blanco, pero el usuario no podrá guardar la fila hasta que especifique un valor para la columna.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para especificar un valor predeterminado con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Si la entrada del campo **Valor predeterminado** reemplaza un valor predeterminado enlazado (que se muestra sin paréntesis), se le preguntará si quiere desenlazar el valor predeterminado y sustituirlo por el nuevo.  
  
-   Para escribir una cadena de texto, incluya el valor entre comillas simples ('); no debe usar comillas dobles (") porque están reservadas para los identificadores escritos entre comillas.  
  
-   Para especificar un valor predeterminado numérico, escriba el número sin comillas.  
  
-   Para especificar un objeto o función, escriba el nombre del objeto o función sin comillas.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-specify-a-default-value-for-a-column"></a>Para especificar un valor predeterminado para una columna  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en la tabla que contenga columnas cuya escala quiera cambiar y, después, haga clic en **Diseño**.  
  
2.  Seleccione la columna para la que desea especificar un valor predeterminado.  
  
3.  En la pestaña **Propiedades de columna** , escriba el nuevo valor predeterminado en la propiedad **Valor o enlace predeterminado** .  
  
    > [!NOTE]  
    >  Para especificar un valor predeterminado numérico, escriba el número. Para un objeto o función, escriba su nombre. Para un valor predeterminado alfanumérico escriba el valor entre comillas simples.  
  
4.  En el menú **Archivo** , haga clic en **Guardar***table name*.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-specify-a-default-value-for-a-column"></a>Para especificar un valor predeterminado para una columna  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    CREATE TABLE dbo.doc_exz ( column_a INT, column_b INT) ;  
    GO  
    INSERT INTO dbo.doc_exz (column_a)VALUES ( 7 ) ;  
    GO  
    ALTER TABLE dbo.doc_exz  
    ADD CONSTRAINT col_b_def  
    DEFAULT 50 FOR column_b ;  
    GO  
  
    ```  
  
 Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  
