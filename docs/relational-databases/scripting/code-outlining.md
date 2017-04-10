---
title: "Esquematizaci&#243;n de c&#243;digo | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Editor de consultas [SQL Server Management Studio], esquematizar código"
  - "Editor de consultas [SQL Server Management Studio], ocultar código"
ms.assetid: 556c7dfe-7bc8-4cab-a36f-2b753a05d3f1
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# Esquematizaci&#243;n de c&#243;digo
  Puede usar la característica de esquematización de los editores de consultas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para ocultar selectivamente el código mientras modifica las consultas. Esto permite ver más fácilmente el código en el que se está trabajando, sobre todo en archivos de consulta de gran tamaño.  
  
## Información general sobre la esquematización  
 De forma predeterminada, todo el código está visible al abrir una ventana de un editor de consultas. Las regiones de código se pueden contraer para ocultarlas. En el borde izquierdo de la ventana del editor, se ve una línea vertical que muestra un cuadrado con un signo menos (-) para identificar el inicio de cada región de código contraíble. Al hacer clic en un signo menos, el texto de la región de código se reemplaza por un cuadro que contiene puntos suspensivos (...), y el signo menos cambia a un signo más (+). Al hacer clic en un signo más, aparece el código contraído y el signo más cambia a un signo menos. Al mover el puntero sobre un cuadro que tiene puntos suspensivos, aparece una información sobre herramientas que muestra el código de la sección contraída.  
  
## Regiones de esquema del sistema  
 Cada editor de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] genera un conjunto de regiones de esquema predeterminadas definidas por el sistema.  
  
 Los editores de código MDX y DMX crean regiones de esquema para cada instrucción de varias líneas. Este es el único nivel de esquematización que admiten estos editores.  
  
### Regiones del Editor de consultas XMLA de Analysis Services  
 El Editor de consultas XMLA de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera una región de esquema para cada atributo XML de varias líneas. El editor anida las regiones de esquema correspondientes a las etiquetas anidadas. Por ejemplo, el Editor de consultas XMLA crea tres regiones de esquema para el documento siguiente.  
  
 ![Código XML que muestra la esquematización](../../relational-databases/scripting/media/editoutlinexmlfull.gif "Código XML que muestra la esquematización")  
  
 Al hacer clic en el signo menos de la línea \<InnerTag>, solo se contrae InnerTag, como se muestra en la ilustración siguiente.  
  
 ![Código XML con el nodo interno oculto](../../relational-databases/scripting/media/editoutlinexmlinnercol.png "Código XML con el nodo interno oculto")  
  
 Al mover el puntero sobre el cuadro que tiene los puntos suspensivos (...), el código de la región contraída aparece en una información sobre herramientas, como se muestra en la ilustración siguiente.  
  
 ![Código XML con información sobre herramientas que muestra el código oculto](../../relational-databases/scripting/media/editoutlinexmlmouse.gif "Código XML con información sobre herramientas que muestra el código oculto")  
  
 Al hacer clic en el signo menos de la línea \<MiddleTag>, se contraen MiddleTag e InnerTag, como se muestra en la ilustración siguiente.  
  
 ![Código XML con las etiquetas internas y centrales ocultas](../../relational-databases/scripting/media/editoutlinexmlmiddlecol.png "Código XML con las etiquetas internas y centrales ocultas")  
  
 Al hacer clic en el signo menos de la línea \<OuterTag>, se contraen las tres líneas, como se muestra en la ilustración siguiente.  
  
 ![Código XML con todas las tres etiquetas ocultas](../../relational-databases/scripting/media/editoutlinexmloutercol.png "Código XML con todas las tres etiquetas ocultas")  
  
### Regiones del Editor de consultas de Database Engine  
 El Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] genera regiones de esquema para cada elemento de la jerarquía siguiente:  
  
1.  Lotes. El primer lote es el código desde el principio del archivo hasta el primer comando GO o hasta el final del archivo si no hay ningún comando GO. Después del primer comando GO, hay un lote desde cada comando GO hasta el comando GO siguiente o hasta el final del archivo.  
  
2.  Bloques delimitados por las palabras clave siguientes:  
  
    -   BEGIN - END  
  
    -   BEGIN TRY - END TRY  
  
    -   BEGIN CATCH - END CATCH  
  
3.  Instrucciones de varias líneas.  
  
 Por ejemplo, el Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] crea tres regiones de esquema para la consulta siguiente:  
  
```  
CREATE PROCEDURE Sales.SampleProc --Outline region 1  
AS  
BEGIN --Outline region 2   
  SELECT GETDATE() AS TimeOfQuery;  
  SELECT * --Outline region 3  
  FROM sys.transmission_queue;  
  SELECT @@VERSION;  
END;  
GO  
```  
  
 Puede hacer clic en el signo menos de la línea `SELECT *` para contraer únicamente esa instrucción `SELECT` . Para contraer el bloque `BEGIN - END` completo, haga clic en el signo menos de la línea `BEGIN` . Para contraer el bloque completo hasta el comando `GO` , haga clic en el signo menos de la línea `CREATE PROCEDURE` . No se pueden contraer individualmente las líneas `SELECT GETDATE()` y `SELECT @@VERSION` porque son instrucciones de una sola línea y no se les asignan regiones de esquematización.  
  
  