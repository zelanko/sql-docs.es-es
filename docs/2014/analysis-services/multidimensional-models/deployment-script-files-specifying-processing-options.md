---
title: Especificar opciones de procesamiento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services deployments, processing options
- input files [Analysis Services]
- deploying [Analysis Services], processing options
- modifying processing options
- Analysis Services Deployment Wizard, processing options
ms.assetid: e9e50817-908e-4210-bc3d-8e2957568241
author: minewiskan
ms.author: owend
ms.openlocfilehash: da6b52d4b1d6b4179a88860b5fe1dc79b92657cf
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546837"
---
# <a name="specifying-processing-options"></a>Especificar opciones de procesamiento
  El [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente para la implementación de Lee las opciones de procesamiento del \<*project name*> archivo. archivo deploymentoptions. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]crea este archivo al compilar el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]usa las opciones de procesamiento especificadas en la página **implementación** del *\<project name>* cuadro de diálogo páginas de **propiedades** para crear el \<*project name*> archivo. archivo deploymentoptions.  
  
## <a name="reviewing-the-processing-options-for-deployment"></a>Revisar las opciones de procesamiento para implementación  
 Los valores de configuración almacenados en el \<*project name*> archivo. archivo deploymentoptions son los siguientes:  
  
-   **Método de procesamiento** Este valor controla si los objetos implementados se procesan después de la implementación y el tipo de procesamiento que se realizará. Existen tres opciones de procesamiento:  
  
    -   Procesamiento predeterminado (valor predeterminado)  
  
    -   Procesamiento total  
  
    -   None  
  
-   **Opciones de tabla de reescritura** Si la reescritura está habilitada en el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , este valor define cómo controlarla. Existen tres opciones de tabla de reescritura:  
  
    -   De forma predeterminada, si existe una tabla de reescritura, se utilizará. Si no existe ninguna tabla de reescritura, se creará una nueva.  
  
    -   Si ya existe una tabla de reescritura, la implementación producirá errores. Si no existe ninguna tabla de reescritura, se creará una nueva.  
  
    -   Independientemente de si existe ya una tabla de reescritura o no, se crea una nueva tabla de reescritura. En este caso, el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eliminará la tabla existente y la reemplazará por una tabla de reescritura nueva.  
  
-   **Implementación transaccional** Este valor controla si la implementación de cambios de metadatos y de comandos de proceso se produce en una transacción única o en transacciones independientes.  
  
    -   Si esta opción es `True` (predeterminada), [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa todos los cambios de metadatos y todos los comandos de proceso en una sola transacción.  
  
    -   Si esta opción es `False`, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa los cambios de metadatos en una sola transacción e implementa cada comando de procesamiento en su propia transacción.  
  
## <a name="modifying-the-processing-options-for-deployment"></a>Modificar las opciones de procesamiento para implementación  
 Sin embargo, puede que tenga que implementar el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto con distintas opciones de procesamiento que las almacenadas en el \<*project name*> archivo. archivo deploymentoptions. Por ejemplo, puede que desee tener todos los objetos totalmente procesados, o procesados con la opción de procesamiento predeterminada, o que no se produzca ningún procesamiento. Si los cubos o las dimensiones están habilitadas para escritura, puede especificar si se utilizará una tabla de reescritura nueva o ya existente.  
  
 Para modificar las opciones de procesamiento utilizadas durante la implementación, puede editar y volver a generar el proyecto, o cambiar las opciones de procesamiento del archivo de entrada mediante uno de los métodos descritos en el siguiente procedimiento.  
  
#### <a name="to-change-processing-options-after-the-input-files-have-been-generated"></a>Para cambiar las opciones de procesamiento después de haber generado los archivos de entrada  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de forma interactiva. En la página **Opciones de procesamiento** , especifique las opciones de procesamiento del proyecto que se está implementando.  
  
     o bien  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el símbolo del sistema y ajuste el asistente de manera que se ejecute en modo de archivo de respuesta. Para obtener más información acerca del modo de archivo de respuesta, vea [Running the Analysis Services Deployment Wizard](running-the-analysis-services-deployment-wizard.md).  
  
     o bien  
  
-   Modifique el \<*project name*> archivo. archivo deploymentoptions con cualquier editor de texto.  
  
## <a name="see-also"></a>Consulte también  
 [Especificar el destino de instalación](deployment-script-files-specifying-the-installation-target.md)   
 [Especificar las opciones de implementación de roles y particiones](deployment-script-files-partition-and-role-deployment-options.md)   
 [Especificar la configuración para la implementación de soluciones](deployment-script-files-solution-deployment-config-settings.md)  
  
  
