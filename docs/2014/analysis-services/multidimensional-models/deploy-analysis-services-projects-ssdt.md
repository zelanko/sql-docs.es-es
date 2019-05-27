---
title: Implementar proyectos de Analysis Services (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- deploy [Analysis Services]
- projects [Analysis Services], deploying
- Business Intelligence Development Studio, deploying projects [Analysis Services]
ms.assetid: 29490a5b-1573-4a35-9277-10c6a6e4ef0e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5b6c79c2ea4355e9d889e235c8185a2460c0ed8c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66075389"
---
# <a name="deploy-analysis-services-projects-ssdt"></a>Implementar proyectos de Analysis Services (SSDT)
  Durante el desarrollo de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], a menudo implementará el proyecto en un servidor de desarrollo para crear la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que el proyecto define. Esto es necesario para probar el proyecto, por ejemplo para examinar las celdas del cubo, examinar los miembros de dimensión o comprobar las fórmulas de los indicadores clave de rendimiento (KPI).  
  
## <a name="deploying-a-project"></a>Implementar un proyecto  
 Puede implementar un proyecto por separado o implementar todos los proyectos de una solución. Al implementar un proyecto, tienen lugar varios hechos consecutivos. En primer lugar se genera el proyecto. Este paso crea los archivos de salida que definen la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y los objetos que la forman. A continuación se valida el servidor de destino. Por último, la base de datos de destino y sus objetos se crean en el servidor de destino. Durante la implementación, el motor de implementación reemplaza totalmente cualquier base de datos existente con el contenido del proyecto, a menos que el proyecto hubiera creado los objetos durante una implementación anterior.  
  
 Después de la implementación inicial, se genera un archivo IncrementalSnapshot.xml en la \<nombre del proyecto > \obj carpeta. Este archivo se usa para determinar si la base de datos o sus objetos del servidor de destino han cambiado fuera del proyecto. Si es así, se le solicitará que sobrescriba todos los objetos de la base de datos de destino. Si todos los cambios se realizaron en el proyecto y este está configurado para la implementación incremental, en el servidor de destino solamente se implementarán los cambios.  
  
 La configuración del proyecto y las opciones asociadas determinan las propiedades de implementación que se usarán para implementarlo. En los proyectos compartidos, cada programador puede usar su propia configuración, con las opciones de configuración que desee. Por ejemplo, cada programador puede especificar un servidor de pruebas distinto para trabajar independientemente de los demás programadores.  
  
## <a name="see-also"></a>Vea también  
 [Crear un proyecto de Analysis Services &#40;SSDT&#41;](create-an-analysis-services-project-ssdt.md)  
  
  
