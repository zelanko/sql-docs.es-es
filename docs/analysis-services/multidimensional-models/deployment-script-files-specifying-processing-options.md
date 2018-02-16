---
title: Especificar opciones de procesamiento | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services deployments, processing options
- input files [Analysis Services]
- deploying [Analysis Services], processing options
- modifying processing options
- Analysis Services Deployment Wizard, processing options
ms.assetid: e9e50817-908e-4210-bc3d-8e2957568241
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 37535b41f5ae5e7c68a47d18a4b91253c7f54d81
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="deployment-script-files---specifying-processing-options"></a>Archivos de Script de implementación: especificar opciones de procesamiento
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
El [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente para implementación de lee las opciones de procesamiento de la \< *nombre del proyecto*>. deploymentoptions. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Este archivo se crea cuando se compila el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] utiliza las opciones de procesamiento especificadas en el **implementación** página de  *\<nombre del proyecto >* **páginas de propiedades** cuadro de diálogo para crear el \< *nombre del proyecto*>. deploymentoptions.  
  
## <a name="reviewing-the-processing-options-for-deployment"></a>Revisar las opciones de procesamiento para implementación  
 Los valores de configuración almacenados dentro del \< *nombre del proyecto*> .deploymentoptions son los siguientes:  
  
-   **Método de procesamiento** Este valor controla si los objetos implementados se procesan después de la implementación y el tipo de procesamiento que se realizará. Existen tres opciones de procesamiento:  
  
    -   Procesamiento predeterminado (valor predeterminado)  
  
    -   Procesamiento total  
  
    -   None  
  
-   **Opciones de tabla de reescritura** Si la reescritura está habilitada en el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , este valor define cómo controlarla. Existen tres opciones de tabla de reescritura:  
  
    -   De forma predeterminada, si existe una tabla de reescritura, se utilizará. Si no existe ninguna tabla de reescritura, se creará una nueva.  
  
    -   Si ya existe una tabla de reescritura, la implementación producirá errores. Si no existe ninguna tabla de reescritura, se creará una nueva.  
  
    -   Independientemente de si existe ya una tabla de reescritura o no, se crea una nueva tabla de reescritura. En este caso, el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eliminará la tabla existente y la reemplazará por una tabla de reescritura nueva.  
  
-   **Implementación transaccional** Este valor controla si la implementación de cambios de metadatos y de comandos de proceso se produce en una transacción única o en transacciones independientes.  
  
    -   Si esta opción es **True** (predeterminada), [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa todos los cambios de metadatos y todos los comandos de proceso en una sola transacción.  
  
    -   Si esta opción es **False**, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa los cambios de metadatos en una sola transacción e implementa cada comando de procesamiento en su propia transacción.  
  
## <a name="modifying-the-processing-options-for-deployment"></a>Modificar las opciones de procesamiento para implementación  
 Sin embargo, puede que necesite implementar el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto usando las opciones de procesamiento diferentes a las almacenadas en el \< *nombre del proyecto*>. deploymentoptions. Por ejemplo, puede que desee tener todos los objetos totalmente procesados, o procesados con la opción de procesamiento predeterminada, o que no se produzca ningún procesamiento. Si los cubos o las dimensiones están habilitadas para escritura, puede especificar si se utilizará una tabla de reescritura nueva o ya existente.  
  
 Para modificar las opciones de procesamiento utilizadas durante la implementación, puede editar y volver a generar el proyecto, o cambiar las opciones de procesamiento del archivo de entrada mediante uno de los métodos descritos en el siguiente procedimiento.  
  
#### <a name="to-change-processing-options-after-the-input-files-have-been-generated"></a>Para cambiar las opciones de procesamiento después de haber generado los archivos de entrada  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de forma interactiva. En la página **Opciones de procesamiento** , especifique las opciones de procesamiento del proyecto que se está implementando.  
  
     O bien  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el símbolo del sistema y ajuste el asistente de manera que se ejecute en modo de archivo de respuesta. Para obtener más información acerca del modo de archivo de respuesta, vea [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     O bien  
  
-   Modificar el \< *nombre del proyecto*>. deploymentoptions utilizando cualquier editor de texto.  
  
## <a name="see-also"></a>Vea también  
 [Especificar el destino de la instalación](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [Especificar opciones de implementación de roles y particiones](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)   
 [Especificar la configuración de implementación de soluciones](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
