---
title: Configurar las propiedades de proyecto de Analysis Services (SSDT) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 582780b5c0e0a81fed17f4d4113c649063b00f46
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="configure-analysis-services-project-properties-ssdt"></a>Configurar las propiedades de un proyecto de Analysis Services (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se define con ciertas propiedades predeterminadas que afectan a la generación e implementación del proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Para cambiar las propiedades del proyecto, haga clic con el botón derecho en el objeto de proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, después, haga clic en **Propiedades**. O bien, puede hacer clic en **Propiedades** en el menú Proyecto.  
  
## <a name="property-description"></a>Descripción de propiedad  
 En la siguiente tabla se describe cada una de las propiedades del proyecto, se muestra su valor predeterminado y se ofrece información sobre cómo cambiar su valor.  
  
|Propiedad|Valor predeterminado|Description|  
|--------------|---------------------|-----------------|  
|Build / Deployment Server Edition|Edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizada para desarrollar el proyecto|Especifica la edición del servidor en que se implementarán finalmente los proyectos. Si se trabaja con varios desarrolladores de software simultáneamente en un proyecto, éstos deben saber cuál es la edición del servidor para saber qué características se deben incluir en el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|Build / Deployment Server Edition|Versión utilizada para desarrollar los proyectos|Especifica la versión del servidor en el que se implementarán finalmente los proyectos.|  
|Build / Outputs|/bin|Ruta de acceso relativa de la salida del proceso de generación del proyecto.|  
|Build / Remove Passwords|True|Especifica si las contraseñas conocidas se eliminarán de las cadenas de conexión que se escriban en el directorio de salida durante el proceso de generación. Las contraseñas se eliminan para aumentar la seguridad. Si se eliminan las contraseñas, deberán proporcionarse cuando se procese el proyecto implementado para que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenga acceso al origen de datos.|  
|Debugging / Start Object|\<Objeto activo >|Determina el objeto que se iniciará al iniciar la depuración.|  
|Deployment / Deployment Mode|Implementar solo cambios|De manera predeterminada, solo se implementan los cambios de los objetos del proyecto (siempre que no se hayan hecho otros cambios en los objetos directamente fuera del proyecto). También puede optar por implementar todos los objetos del proyecto durante cada implementación. Para que el rendimiento sea mejor, use Implementar solo cambios.|  
|Deployment / Processing Option|Valor de DB-Library|De manera predeterminada, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determinará el tipo de procesamiento necesario cuando se implementen los cambios de los objetos. Eso se suele traducir en el tiempo de implementación más breve. Sin embargo, también puede elegir un procesamiento completo o ningún procesamiento durante cada implementación.|  
|Deployment / Transactional Deployment|False|De manera predeterminada, la implementación de los objetos modificados o de todos los objetos no es transaccional con el procesamiento de los objetos implementados. La implementación puede ser correcta y persistir aunque se produzca un error de procesamiento. Puede cambiar este valor predeterminado para incluir la implementación y el procesamiento en una sola transacción.|  
|Implementación / Servidor de destino|localhost|De manera predeterminada, los objetos de base de datos del proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se implementarán en la instancia predeterminada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] del equipo local en el que se está usando [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] . Puede cambiar este valor predeterminado para especificar una instancia con nombre del equipo local o cualquier instancia de un equipo remoto en que tenga permiso para crear objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|Deployment / Database|\<nombre del proyecto >|De manera predeterminada, el nombre de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se crearán las instancias de los objetos del proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tras la implementación es el nombre del proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cuando se definió. Puede cambiar esta propiedad para cambiar el nombre de la base de datos en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificada por la propiedad Server.|  
  
## <a name="property-configurations"></a>Configuraciones de propiedades  
 Las propiedades se definen configuración por configuración. Las configuraciones de proyecto permiten a los programadores trabajar con un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con valores de compilación, depuración e implementación distintos sin editar directamente los archivos XML subyacentes del proyecto.  
  
 Un proyecto se crea inicialmente con una sola configuración, conocida como Programación. Puede crear otras configuraciones y pasar de una a otra en el Administrador de configuración.  
  
 Hasta que se creen configuraciones adicionales, todos los programadores utilizan la configuración común. Con todo, en las distintas fases de desarrollo del proyecto, por ejemplo durante la programación inicial y la fase de pruebas de un proyecto, cada uno de los programadores puede usar orígenes de datos distintos e implementar el proyecto en distintos servidores para objetivos distintos. Las configuraciones le permiten conservar estos valores distintos en distintos archivos de configuración.  
  
## <a name="see-also"></a>Vea también  
 [Compilar proyectos de Analysis Services & #40; SSDT & #41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [Implementar proyectos de Analysis Services & #40; SSDT & #41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  
