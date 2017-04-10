---
title: "Administrar los cambios de las vistas del origen de datos y los or&#237;genes de datos | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modificar orígenes de datos"
  - "modificar vistas del origen de datos"
  - "vistas del origen de datos [Analysis Services], actualizaciones del esquema"
  - "orígenes de datos [Analysis Services], actualizaciones del esquema"
ms.assetid: 928c9f63-365a-43fd-9bbd-78828cc7e54d
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 25
---
# Administrar los cambios de las vistas del origen de datos y los or&#237;genes de datos
  Si se vuelve a ejecutar el Asistente para generar esquemas, éste volverá a utilizar el mismo origen de datos y vista del origen de datos que en la generación original. Si se agrega un origen de datos o una vista de origen de datos, el asistente no los utilizará. Si se elimina el origen de datos o la vista de origen de datos originales tras la generación inicial, debe ejecutarse el asistente desde el principio. También se eliminará la configuración anterior del asistente. Los objetos existentes en una base de datos subyacente enlazados a un origen de datos o vista de origen de datos eliminados se tratarán como objetos creados por el usuario la próxima vez que se ejecute el Asistente para generar esquemas.  
  
 Si la vista del origen de datos no refleja el estado actual de la base de datos subyacente en el momento de la generación, el Asistente para generar esquemas podría experimentar errores al generar el esquema de la base de datos del área de asunto. Por ejemplo, si la vista del origen de datos especifica que el tipo de datos de una columna es **int**, pero el tipo de datos de la columna es en realidad **string**, el Asistente para generar esquemas establecerá el tipo de datos de la clave externa en **INT** para que coincida con la vista del origen de datos, aunque se producirá un error al crear la relación dado que el tipo de datos real es **string**.  
  
 Por otra parte, no se generarán errores si se cambia la cadena de conexión de origen de datos a una base de datos distinta de la generación anterior. Se utilizará la nueva base de datos y no se realizarán cambios en la base de datos anterior.  
  
## Vea también  
 [Descripción de la generación incremental](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)  
  
  