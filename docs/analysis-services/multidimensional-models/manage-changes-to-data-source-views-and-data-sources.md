---
title: "Administrar los cambios en las vistas del origen de datos y orígenes de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying data sources
- modifying data source views
- data source views [Analysis Services], schema updates
- data sources [Analysis Services], schema updates
ms.assetid: 928c9f63-365a-43fd-9bbd-78828cc7e54d
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6526be940f14de19cc6409dbb5fdbcdace701b46
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="manage-changes-to-data-source-views-and-data-sources"></a>Administrar los cambios de las vistas del origen de datos y los orígenes de datos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Cuando se vuelve a ejecutar el Asistente para generar esquemas, vuelve a utilizar el mismo origen de datos y la vista del origen de datos que utiliza para la generación original. Si se agrega un origen de datos o una vista de origen de datos, el asistente no los utilizará. Si se elimina el origen de datos o la vista de origen de datos originales tras la generación inicial, debe ejecutarse el asistente desde el principio. También se eliminará la configuración anterior del asistente. Los objetos existentes en una base de datos subyacente enlazados a un origen de datos o vista de origen de datos eliminados se tratarán como objetos creados por el usuario la próxima vez que se ejecute el Asistente para generar esquemas.  
  
 Si la vista del origen de datos no refleja el estado actual de la base de datos subyacente en el momento de la generación, el Asistente para generar esquemas podría experimentar errores al generar el esquema de la base de datos del área de asunto. Por ejemplo, si la vista del origen de datos especifica que el tipo de datos de una columna es **int**, pero el tipo de datos de la columna es en realidad **string**, el Asistente para generar esquemas establecerá el tipo de datos de la clave externa en **INT** para que coincida con la vista del origen de datos, aunque se producirá un error al crear la relación dado que el tipo de datos real es **string**.  
  
 Por otra parte, no se generarán errores si se cambia la cadena de conexión de origen de datos a una base de datos distinta de la generación anterior. Se utilizará la nueva base de datos y no se realizarán cambios en la base de datos anterior.  
  
## <a name="see-also"></a>Vea también  
 [Descripción de la generación incremental](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)  
  
  
