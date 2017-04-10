---
title: "Guardar un plan de ejecuci&#243;n en formato XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "planes de consulta XML [SQL Server]"
  - "abrir planes de ejecución"
  - "planes de presentación XML [SQL Server]"
  - "planes de ejecución [SQL Server], guardar"
  - "guardar planes de ejecución"
ms.assetid: c439e53b-56f3-4442-97c6-dabd48a203d8
caps.latest.revision: 25
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 25
---
# Guardar un plan de ejecuci&#243;n en formato XML
  Utilice [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para guardar planes de ejecución como archivos XML y para visualizarlos.  
  
 Para utilizar la característica de plan de ejecución en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]o para usar las opciones SET del plan de presentación XML, los usuarios deben disponer de los permisos adecuados para ejecutar la consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] para la que se está generando un plan de ejecución y deben tener el permiso SHOWPLAN para todas las bases de datos a las que haga referencia la consulta.  
  
### Para guardar un plan de consulta mediante las opciones SET del plan de presentación XML  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra un editor de consultas y conéctese a [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Active SHOWPLAN_XML con la siguiente instrucción:  
  
    ```  
    SET SHOWPLAN_XML ON;  
    GO  
    ```  
  
     Para activar STATISTICS XML, utilice la siguiente instrucción:  
  
    ```  
    SET STATISTICS XML ON;  
    GO  
    ```  
  
     SHOWPLAN_XML genera información del plan de ejecución de la consulta de tiempo de compilación de una consulta, pero no ejecuta la consulta. STATISTICS XML genera información del plan de ejecución de la consulta de tiempo de compilación de una consulta y ejecuta la consulta.  
  
3.  Ejecutar una consulta. Ejemplo:  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SET SHOWPLAN_XML ON;  
    GO  
    -- Execute a query.  
    SELECT BusinessEntityID   
    FROM HumanResources.Employee  
    WHERE NationalIDNumber = '509647174';  
    GO  
    SET SHOWPLAN_XML OFF;  
    ```  
  
4.  En el panel **Resultados**, haga clic con el botón derecho en el **Plan de presentación XML de Microsoft SQL Server** que contiene el plan de consulta y, después, haga clic en **Guardar resultados como**.  
  
5.  En el cuadro de diálogo **Guardar** **resultados de \<cuadrícula o texto>**, en el cuadro **Guardar como tipo**, haga clic en **Todos los archivos (\*.\*)**.  
  
6.  En el cuadro **Nombre de archivo**, proporcione un nombre con el formato \< nombre**>.sqlplan** y haga clic en **Guardar**.  
  
### Para guardar un plan de ejecución mediante las opciones de SQL Server Management Studio  
  
1.  Genere un plan de ejecución estimado o uno real mediante [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para obtener más información, vea [Mostrar el plan de ejecución estimado](../../relational-databases/performance/display-the-estimated-execution-plan.md) o [Mostrar un plan de ejecución real](../../relational-databases/performance/display-an-actual-execution-plan.md).  
  
2.  En la pestaña **Plan de ejecución** del panel de resultados, haga clic con el botón derecho en el plan de ejecución gráfico y elija **Guardar plan de ejecución como**.  
  
     Como alternativa, también puede elegir **Guardar plan de ejecución como** en el menú **Archivo** .  
  
3.  En el cuadro de diálogo **Guardar como**, asegúrese de que **Guardar como tipo** está establecido en **Archivos de plan de ejecución (\*.sqlplan)**.  
  
4.  En el cuadro **Nombre de archivo**, proporcione un nombre con el formato \< nombre**>.sqlplan** y haga clic en **Guardar**.  
  
### Para abrir un plan de consulta XML guardado en SQL Server Management Studio  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el menú **Archivo** , elija **Abrir**y, a continuación, haga clic en **Archivo**.  
  
2.  En el cuadro de diálogo **Abrir archivo**, establezca **Archivos de tipo** en **Archivos de plan de ejecución (\*.sqlplan)** para generar una lista filtrada de archivos de plan de consulta XML guardados.  
  
3.  Seleccione el archivo de plan de consulta XML que desea ver y haga clic en **Abrir**.  
  
     Como alternativa, en el Explorador de Windows, haga doble clic en un archivo con la extensión **.sqlplan**. El plan se abre en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## Vea también  
 [SET SHOWPLAN_XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)   
 [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md)  
  
  