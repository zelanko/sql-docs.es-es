---
title: Implementar proyectos de Analysis Services (SSDT) | Documentos de Microsoft
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
- deploy [Analysis Services]
- projects [Analysis Services], deploying
- Business Intelligence Development Studio, deploying projects [Analysis Services]
ms.assetid: 29490a5b-1573-4a35-9277-10c6a6e4ef0e
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dbfe19ac5da2fee064dd19d06aa1bf7992c3429b
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="deploy-analysis-services-projects-ssdt"></a>Implementar proyectos de Analysis Services (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Durante el desarrollo de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], a menudo implementará el proyecto en un servidor de desarrollo para crear la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que el proyecto define. Esto es necesario para probar el proyecto, por ejemplo para examinar las celdas del cubo, examinar los miembros de dimensión o comprobar las fórmulas de los indicadores clave de rendimiento (KPI).  
  
## <a name="deploying-a-project"></a>Implementar un proyecto  
 Puede implementar un proyecto por separado o implementar todos los proyectos de una solución. Al implementar un proyecto, tienen lugar varios hechos consecutivos. En primer lugar se genera el proyecto. Este paso crea los archivos de salida que definen la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y los objetos que la forman. A continuación se valida el servidor de destino. Por último, la base de datos de destino y sus objetos se crean en el servidor de destino. Durante la implementación, el motor de implementación reemplaza totalmente cualquier base de datos existente con el contenido del proyecto, a menos que el proyecto hubiera creado los objetos durante una implementación anterior.  
  
 Después de la implementación inicial, se genera un archivo IncrementalSnapshot.xml en la \<nombre del proyecto > \obj carpeta. Este archivo se usa para determinar si la base de datos o sus objetos del servidor de destino han cambiado fuera del proyecto. Si es así, se le solicitará que sobrescriba todos los objetos de la base de datos de destino. Si todos los cambios se realizaron en el proyecto y este está configurado para la implementación incremental, en el servidor de destino solamente se implementarán los cambios.  
  
 La configuración del proyecto y las opciones asociadas determinan las propiedades de implementación que se usarán para implementarlo. En los proyectos compartidos, cada programador puede usar su propia configuración, con las opciones de configuración que desee. Por ejemplo, cada programador puede especificar un servidor de pruebas distinto para trabajar independientemente de los demás programadores.  
  
## <a name="see-also"></a>Vea también  
 [Crear un proyecto de Analysis Services &#40; SSDT &#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)  
  
  
