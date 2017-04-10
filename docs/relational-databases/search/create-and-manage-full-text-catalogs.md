---
title: "Crear y administrar cat&#225;logos de texto completo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-search"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "catálogos de texto completo [SQL Server], crear"
  - "búsqueda de texto completo [SQL Server], con SQL Server Management Studio"
ms.assetid: 824b7131-44a6-4815-89e6-62b7bab060e3
caps.latest.revision: 21
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 20
---
# Crear y administrar cat&#225;logos de texto completo
  Un catálogo de texto completo es un objeto virtual que no pertenece a ningún grupo de archivos; es un concepto lógico que hace referencia a un grupo de índices de texto completo.  
  
##  <a name="creating"></a> Crear un catálogo de texto completo  
  
#### Para crear un catálogo de texto completo  
  
1.  En el Explorador de objetos, expanda el servidor, expanda **Bases de datos** y, después, expanda la base de datos en la que quiere crear el catálogo de texto completo.  
  
2.  Expanda **Almacenamiento** y, después, haga clic con el botón derecho en **Catálogos de texto completo**.  
  
3.  Seleccione **Nuevo catálogo de texto completo**.  
  
4.  En el cuadro de diálogo **Nuevo catálogo de texto completo**, especifique la información del catálogo que va a volver a crear. Para obtener más información, vea [Búsqueda de texto completo](../Topic/New%20Full-Text%20Catalog%20\(General%20Page\).md).  
  
    > [!NOTE]  
    >  Los identificadores de los catálogos de texto completo comienzan por 00005 y se incrementan en uno con cada nuevo catálogo que se crea.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
   
  
##  <a name="props"></a> Ver las propiedades de un catálogo de texto completo  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] funciones como FULLTEXTCATALOGPROPERTY, se pueden usar para obtener el valor de diversas propiedades relacionadas con la indexación de texto completo. Esta información es útil para administrar y solucionar problemas de la búsqueda de texto completo.  
  
 En la siguiente tabla se muestran las propiedades relacionadas con los catálogos de texto completo.  
  
|Propiedad|Descripción|Función|  
|--------------|-----------------|--------------|  
|**AccentSensitivity**|Opción de distinción de acentos.|[FULLTEXTCATALOGPROPERTY](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)|  
|**ImportStatus**|Si se va a importar el catálogo de texto completo.|FULLTEXTCATALOGPROPERTY|  
|**IndexSize**|Tamaño, en megabytes (MB), del catálogo de texto completo.|FULLTEXTCATALOGPROPERTY|  
|**ItemCount**|Número de elementos de texto completo indizados que contiene actualmente el catálogo de texto completo.|FULLTEXTCATALOGPROPERTY|  
|**MergeStatus**|Si hay una combinación maestra en curso.|FULLTEXTCATALOGPROPERTY|  
|**PopulateCompletionAge**|Diferencia, en segundos, entre la terminación del último rellenado del índice de texto completo y 01/01/1990 00:00:00.|FULLTEXTCATALOGPROPERTY|  
|**PopulateStatus**|Estado del rellenado.<br /><br /> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|FULLTEXTCATALOGPROPERTY|  
|**UniqueKeyCount**|Número de claves únicas en el catálogo de texto completo.|FULLTEXTCATALOGPROPERTY|  
  
   
  
##  <a name="rebuildone"></a> Recompilar un catálogo de texto completo  
  
#### Para regenerar un catálogo de texto completo  
  
1.  En el Explorador de objetos, expanda el servidor, expanda **Bases de datos** y, después, expanda la base de datos que contiene el catálogo de texto completo que quiere volver a generar.  
  
2.  Expanda **Almacenamiento**y, a continuación, expanda **Catálogos de texto completo**.  
  
3.  Haga clic con el botón derecho en el nombre del catálogo de texto completo que quiere volver a generar y seleccione **Volver a generar**.  
  
4.  Ante la pregunta **¿Quiere eliminar el catálogo de texto completo y volver a generarlo?**, haga clic en **Aceptar**.  
  
5.  En el cuadro de diálogo **Volver a generar el catálogo de texto completo**, haga clic en **Cerrar**.  
  
   
  
##  <a name="rebuildall"></a> Recompilar todos los catálogos de texto completo para una base de datos  
  
#### Para recompilar los catálogos de texto completo de una base de datos  
  
1.  En el Explorador de objetos, expanda el servidor, expanda **Bases de datos** y, después, expanda la base de datos que contiene los catálogos de texto completo que quiere volver a generar.  
  
2.  Expanda **Almacenamiento** y, después, haga clic con el botón derecho en **Catálogos de texto completo**.  
  
3.  Seleccione **Volver a generar todo**.  
  
4.  Ante la pregunta **¿Quiere eliminar todos los catálogos de texto completo y volver a generarlos?**, haga clic en **Aceptar**.  
  
5.  En el cuadro de diálogo **Volver a generar todos los catálogos de texto completo**, haga clic en **Cerrar**.  
  
  
  
##  <a name="removing"></a> Quitar un catálogo de texto completo de una base de datos  
  
#### Para quitar un catálogo de texto completo de una base de datos  
  
1.  En el Explorador de objetos, expanda el servidor, expanda **Bases de datos** y expanda la base de datos que contiene el catálogo de texto completo que quiere quitar.  
  
2.  Expanda **Almacenamiento**y, a continuación, **Catálogos de texto completo**.  
  
3.  Haga clic con el botón derecho en el catálogo de texto completo que quiere quitar y seleccione **Eliminar**.  
  
4.  En el cuadro de diálogo **Eliminar objetos** , haga clic en **Aceptar**.  
  
  
## Vea también  
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)  
  
  