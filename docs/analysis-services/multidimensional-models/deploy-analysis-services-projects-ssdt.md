---
title: Implementar proyectos de Analysis Services (SSDT) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f610aab0862c05c52d280080512670b1dd425c3c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208954"
---
# <a name="deploy-analysis-services-projects-ssdt"></a>Implementar proyectos de Analysis Services (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Durante el desarrollo de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], a menudo implementará el proyecto en un servidor de desarrollo para crear la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que el proyecto define. Esto es necesario para probar el proyecto, por ejemplo para examinar las celdas del cubo, examinar los miembros de dimensión o comprobar las fórmulas de los indicadores clave de rendimiento (KPI).  
  
## <a name="deploying-a-project"></a>Implementar un proyecto  
 Puede implementar un proyecto por separado o implementar todos los proyectos de una solución. Al implementar un proyecto, tienen lugar varios hechos consecutivos. En primer lugar se genera el proyecto. Este paso crea los archivos de salida que definen la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y los objetos que la forman. A continuación se valida el servidor de destino. Por último, la base de datos de destino y sus objetos se crean en el servidor de destino. Durante la implementación, el motor de implementación reemplaza totalmente cualquier base de datos existente con el contenido del proyecto, a menos que el proyecto hubiera creado los objetos durante una implementación anterior.  
  
 Después de la implementación inicial, se genera un archivo IncrementalSnapshot.xml en la \<nombre del proyecto > \obj carpeta. Este archivo se usa para determinar si la base de datos o sus objetos del servidor de destino han cambiado fuera del proyecto. Si es así, se le solicitará que sobrescriba todos los objetos de la base de datos de destino. Si todos los cambios se realizaron en el proyecto y este está configurado para la implementación incremental, en el servidor de destino solamente se implementarán los cambios.  
  
 La configuración del proyecto y las opciones asociadas determinan las propiedades de implementación que se usarán para implementarlo. En los proyectos compartidos, cada programador puede usar su propia configuración, con las opciones de configuración que desee. Por ejemplo, cada programador puede especificar un servidor de pruebas distinto para trabajar independientemente de los demás programadores.  
  
## <a name="see-also"></a>Vea también  
 [Crear un proyecto de Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)  
  
  
