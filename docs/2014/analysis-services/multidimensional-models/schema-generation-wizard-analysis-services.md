---
title: Asistente para la generación de esquemas (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- relational schema [Analysis Services]
ms.assetid: 68bf7ba3-d0cb-437f-9a3e-9edc0999af19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2f8757044ba15f7b8c2567dd88e1ef3637d2e3f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073066"
---
# <a name="schema-generation-wizard-analysis-services"></a>Asistente para generar esquemas (Analysis Services)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] admite dos métodos para trabajar con esquemas relacionales al definir objetos OLAP en un proyecto o base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Normalmente, los objetos OLAP se definen en función de un modelo de datos lógico creado en una vista de origen de datos de un proyecto o base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Esta vista del origen de datos se define en función de elementos de esquema de uno o varios orígenes de datos relacionales, personalizados en la vista del origen de datos.  
  
 Como alternativa, puede definir los objetos OLAP en primer lugar, y después generar una vista del origen de datos, un origen de datos y el esquema de la base de datos relacional subyacente que admite estos objetos OLAP. Esta base de datos relacional se conoce como base de datos del área de asunto.  
  
 En ocasiones, este método se denomina diseño de arriba abajo, y se usa a menudo para crear prototipos y modelos de análisis. Cuando se emplea este método, se usa el Asistente para generar esquemas para crear la vista del origen de datos y los objetos de origen de datos subyacentes basándose en los objetos OLAP definidos en un proyecto o base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Este es un método iterativo. Es muy probable que tenga que volver a ejecutar el Asistente varias veces mientras cambia el diseño de las dimensiones y los cubos. Cada vez que ejecute el Asistente, este incorporará los cambios en los objetos subyacentes y, en la medida de lo posible, conservará los datos contenidos en las bases de datos subyacentes.  
  
 El esquema que se genera es un esquema de motor de base de datos relacional de SQL Server. El Asistente no genera esquemas para otros productos de bases de datos relacionales.  
  
 Los datos con los que se rellena la base de datos del área de asunto se agregan de forma independiente mediante las herramientas y técnicas que se usan para rellenar una base de datos relacional de SQL Server. En la mayoría de los casos, al ejecutar el Asistente, se conservan los datos, pero hay excepciones. Por ejemplo, si se elimina una dimensión o un atributo que contiene datos, es necesario quitar algunos de ellos. Si el Asistente para generar esquemas debe borrar algunos datos debido a un cambio en el esquema, aparecerá una advertencia antes de eliminar los datos y se podrá cancelar el nuevo proceso de generación.  
  
 Como regla general, todo cambio que se realice en un objeto generado originalmente mediante el Asistente para generar esquemas se sobrescribe cuando el Asistente para generar esquemas vuelve a generar el objeto. La principal excepción a esta regla es cuando se agregan columnas a una tabla que haya generado el Asistente para generar esquemas. En este caso, el Asistente para generar esquemas conserva las columnas que se hayan agregado a la tabla, así como los datos de dichas columnas.  
  
## <a name="in-this-section"></a>En esta sección  
 La tabla siguiente contiene una lista de temas adicionales en los que se explica cómo trabajar con el Asistente para generar esquemas.  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Usar el Asistente para generar esquemas &#40;Analysis Services&#41;](schema-generation-wizard-analysis-services.md)|Describe cómo generar el esquema para las bases de datos del área de asunto y del área de ensayo.|  
|[Descripción de esquemas de base de datos](understanding-the-database-schemas.md)|Describe el esquema que se genera para las bases de datos del área de asunto y del área de ensayo.|  
|[Descripción de la generación incremental](understanding-incremental-generation.md)|Describe las capacidades de generación incremental del Asistente para generar esquemas.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas del origen de datos en modelos multidimensionales](data-source-views-in-multidimensional-models.md)   
 [Orígenes de datos en modelos multidimensionales](data-sources-in-multidimensional-models.md)   
 [Orígenes de datos admitidos &#40;SSAS Multidimensional&#41;](supported-data-sources-ssas-multidimensional.md)  
  
  
