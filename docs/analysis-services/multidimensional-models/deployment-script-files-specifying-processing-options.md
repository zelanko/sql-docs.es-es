---
title: Especificar las opciones de procesamiento | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54be969446b9c1b234860ce2a68c1208634246ce
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68178356"
---
# <a name="deployment-script-files---specifying-processing-options"></a>Archivos de Script de implementación: especificar opciones de procesamiento
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  El [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente para implementación de lee las opciones de procesamiento de la \< *nombre del proyecto*> .deploymentoptions file. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] crea este archivo cuando se genera el proyecto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa las opciones de procesamiento especificadas en el **implementación** página de  *\<nombre del proyecto >* **las páginas de propiedades** cuadro de diálogo para crear el \< *nombre del proyecto*> .deploymentoptions file.  
  
## <a name="reviewing-the-processing-options-for-deployment"></a>Revisar las opciones de procesamiento para implementación  
 Los valores de configuración almacenados dentro del \< *nombre del proyecto*> .deploymentoptions file son los siguientes:  
  
-   **Método de procesamiento** Este valor controla si los objetos implementados se procesan después de la implementación y el tipo de procesamiento que se realizará. Existen tres opciones de procesamiento:  
  
    -   Procesamiento predeterminado (valor predeterminado) detecta el estado del proceso de objetos de base de datos y realiza el procesamiento necesario para devolver objetos sin procesar o procesados parcialmente a un estado totalmente procesado.
  
    -   El procesamiento completo procesa un objeto y todos los objetos que contiene. Cuando se ejecuta Procesar completo en un objeto que ya se ha procesado, Analysis Services quita todos los datos del objeto y, a continuación, lo procesa. 
  
    -   Ninguno significa que no se realiza ningún procesamiento.


-   **Opciones de tabla de reescritura** Si la reescritura está habilitada en el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , este valor define cómo controlarla. Existen tres opciones de tabla de reescritura:  
  
    -   De forma predeterminada, si existe una tabla de reescritura, se utilizará. Si no existe ninguna tabla de reescritura, se creará una nueva.  
  
    -   Si ya existe una tabla de reescritura, la implementación producirá errores. Si no existe ninguna tabla de reescritura, se creará una nueva.  
  
    -   Independientemente de si existe ya una tabla de reescritura o no, se crea una nueva tabla de reescritura. En este caso, el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eliminará la tabla existente y la reemplazará por una tabla de reescritura nueva.  
  
-   **Implementación transaccional** Este valor controla si la implementación de cambios de metadatos y de comandos de proceso se produce en una transacción única o en transacciones independientes.  
  
    -   Si esta opción es **True** (predeterminada), [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa todos los cambios de metadatos y todos los comandos de proceso en una sola transacción.  
  
    -   Si esta opción es **False**, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa los cambios de metadatos en una sola transacción e implementa cada comando de procesamiento en su propia transacción.  
  
## <a name="modifying-the-processing-options-for-deployment"></a>Modificar las opciones de procesamiento para implementación  
 Sin embargo, es posible que deba implementar el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto con opciones de procesamiento diferentes a las almacenadas en el \< *nombre del proyecto*> .deploymentoptions file. Por ejemplo, puede que desee tener todos los objetos totalmente procesados, o procesados con la opción de procesamiento predeterminada, o que no se produzca ningún procesamiento. Si los cubos o las dimensiones están habilitadas para escritura, puede especificar si se utilizará una tabla de reescritura nueva o ya existente.  
  
 Para modificar las opciones de procesamiento utilizadas durante la implementación, puede editar y volver a generar el proyecto, o cambiar las opciones de procesamiento del archivo de entrada mediante uno de los métodos descritos en el siguiente procedimiento.  
  
#### <a name="to-change-processing-options-after-the-input-files-have-been-generated"></a>Para cambiar las opciones de procesamiento después de haber generado los archivos de entrada  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de forma interactiva. En la página **Opciones de procesamiento** , especifique las opciones de procesamiento del proyecto que se está implementando.  
  
     -o bien-  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el símbolo del sistema y ajuste el asistente de manera que se ejecute en modo de archivo de respuesta. Para obtener más información acerca del modo de archivo de respuesta, vea [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     -o bien-  
  
-   Modificar el \< *nombre del proyecto*> archivo .deploymentoptions con cualquier editor de texto.  
  
## <a name="see-also"></a>Vea también  
 [Especificar el destino de instalación](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [Especificar opciones de implementación de roles y particiones](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)   
 [Especificar la configuración para la implementación de soluciones](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
