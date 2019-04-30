---
title: Esquematización de código | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Query Editor [SQL Server Management Studio], outlining code
- Query Editor [SQL Server Management Studio], hiding code
ms.assetid: 556c7dfe-7bc8-4cab-a36f-2b753a05d3f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c109b96192112a914b06748654c5a7e1510569e0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63209567"
---
# <a name="code-outlining"></a>Esquematización de código
  Puede usar la característica de esquematización de los editores de consultas de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] para ocultar selectivamente el código mientras modifica las consultas. Esto permite ver más fácilmente el código en el que se está trabajando, sobre todo en archivos de consulta de gran tamaño.  
  
## <a name="outlining-overview"></a>Información general sobre la esquematización  
 De forma predeterminada, todo el código está visible al abrir una ventana de un editor de consultas. Las regiones de código se pueden contraer para ocultarlas. En el borde izquierdo de la ventana del editor, se ve una línea vertical que muestra un cuadrado con un signo menos (-) para identificar el inicio de cada región de código contraíble. Al hacer clic en un signo menos, el texto de la región de código se reemplaza por un cuadro que contiene puntos suspensivos (...) y el signo menos cambia a un signo más (+). Al hacer clic en un signo más, aparece el código contraído y el signo más cambia a un signo menos. Al mover el puntero sobre un cuadro que tiene puntos suspensivos, aparece una información sobre herramientas que muestra el código de la sección contraída.  
  
## <a name="system-outline-regions"></a>Regiones de esquema del sistema  
 Cada editor de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] genera un conjunto de regiones de esquema predeterminadas definidas por el sistema.  
  
 Los editores de código MDX y DMX crean regiones de esquema para cada instrucción de varias líneas. Este es el único nivel de esquematización que admiten estos editores.  
  
### <a name="analysis-services-xmla-query-editor-regions"></a>Regiones del Editor de consultas XMLA de Analysis Services  
 El Editor de consultas XMLA de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] genera una región de esquema para cada atributo XML de varias líneas. El editor anida las regiones de esquema correspondientes a las etiquetas anidadas. Por ejemplo, el Editor de consultas XMLA crea tres regiones de esquema para el documento siguiente.  
  
 ![Código XML que muestra la esquematización](../../database-engine/media/editoutlinexmlfull.gif "Código XML que muestra la esquematización")  
  
 Al hacer clic en el signo menos de la línea \<InnerTag>, solo se contrae InnerTag, como se muestra en la ilustración siguiente.  
  
 ![Código XML con el nodo interno oculto](../../database-engine/media/editoutlinexmlinnercol.gif "Código XML con el nodo interno oculto")  
  
 Al mover el puntero sobre el cuadro que tiene los puntos suspensivos (...), el código de la región contraída aparece en una información sobre herramientas, como se muestra en la ilustración siguiente.  
  
 ![Código XML con información sobre herramientas que muestra el código oculto](../../database-engine/media/editoutlinexmlmouse.gif "Código XML con información sobre herramientas que muestra el código oculto")  
  
 Al hacer clic en el signo menos de la línea \<MiddleTag>, se contraen MiddleTag e InnerTag, como se muestra en la ilustración siguiente.  
  
 ![Código XML con las etiquetas internas y centrales ocultas](../../database-engine/media/editoutlinexmlmiddlecol.gif "Código XML con las etiquetas internas y centrales ocultas")  
  
 Al hacer clic en el signo menos de la línea \<OuterTag>, se contraen las tres líneas, como se muestra en la ilustración siguiente.  
  
 ![Código XML con todas las tres etiquetas ocultas](../../database-engine/media/editoutlinexmloutercol.gif "Código XML con todas las tres etiquetas ocultas")  
  
### <a name="database-engine-query-editor-regions"></a>Regiones del Editor de consultas de Database Engine  
 El Editor de consultas de [!INCLUDE[ssDE](../../../includes/ssde-md.md)] genera regiones de esquema para cada elemento de la jerarquía siguiente:  
  
1.  Lotes. El primer lote es el código desde el principio del archivo hasta el primer comando GO o hasta el final del archivo si no hay ningún comando GO. Después del primer comando GO, hay un lote desde cada comando GO hasta el comando GO siguiente o hasta el final del archivo.  
  
2.  Bloques delimitados por las palabras clave siguientes:  
  
    -   BEGIN - END  
  
    -   BEGIN TRY - END TRY  
  
    -   BEGIN CATCH - END CATCH  
  
3.  Instrucciones de varias líneas.  
  
 Por ejemplo, el Editor de consultas de [!INCLUDE[ssDE](../../../includes/ssde-md.md)] crea tres regiones de esquema para la consulta siguiente:  
  
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
  
  
