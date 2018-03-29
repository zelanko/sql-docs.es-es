---
title: Especificar la configuración de implementación de soluciones | Documentos de Microsoft
ms.custom: ''
ms.date: 03/27/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Analysis Services Deployment Wizard, configuration settings
- input files [Analysis Services]
- configuration options [Analysis Services]
- Analysis Services deployments, configuration settings
- deploying [Analysis Services], configuration settings
ms.assetid: 953814a3-85ef-40cc-b46a-d532aa7a6569
caps.latest.revision: ''
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c5cb1d30f65e38b69fbde629fb940b94c5864f8d
ms.sourcegitcommit: d6881107b51e1afe09c2d8b88b98d075589377de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="deployment-script-files---solution-deployment-config-settings"></a>Archivos de Script de implementación - ajustes de configuración de implementación de soluciones
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  El [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente para implementar lee la partición y el rol de opciones de implementación que se utilizan en el script de implementación de la \< *nombre del proyecto*> archivo. configSettings. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Este archivo se crea cuando se compila el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa los valores de configuración del proyecto actual para crear el \< *nombre del proyecto*> archivo. configSettings.  
  
## <a name="reviewing-the-configuration-settings-for-deployment"></a>Revisar los valores de configuración para implementación  
 Los siguientes son los valores de configuración almacenados en la \< *nombre del proyecto*> .configsettings archivo:  
  
-   **Cadenas de conexión de orígenes de datos** Se trata de las cadenas de conexión para cada origen de datos según los valores especificados en el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . El Id. de usuario y la contraseña siempre se quitan de la cadena de conexión antes de que el resto de la cadena se almacene en este archivo. Sin embargo, si el Asistente para la implementación está implementando directamente en una instancia de Analysis Services, puede agregar la información de Id. de usuario y contraseña correspondiente en el asistente para que el procesamiento de la base de datos de implementación sea correcto. Esta información de conexión no se almacenará en el script de implementación si el Asistente para la implementación guarda  
  
-   **Cuentas de suplantación** Este valor especifica el nombre de usuario que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza para ejecutar instrucciones en cada origen de datos. Si no se especifica ninguna cuenta de suplantación, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizará su cuenta de inicio de sesión para ejecutar instrucciones. Si a la cuenta de inicio de sesión de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se le conceden permisos directamente en el origen de datos, todos los administradores de todas las bases de datos de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tendrán acceso al origen de datos a través de la cuenta de inicio de sesión. Si se especifica una cuenta de usuario y una contraseña, esta información siempre se quita antes de que la información de suplantación se almacene en este archivo. Sin embargo, si el Asistente para la implementación está implementando directamente en una instancia de Analysis Services, puede agregar la información de Id. de usuario y contraseña correspondiente en el asistente para que el procesamiento de la base de datos de implementación sea correcto. Esta información de suplantación no se almacenará en el script de implementación si el Asistente para la implementación guarda uno.  
  
-   **Archivos de registro de errores de clave** Esta configuración especifica el nombre de archivo y la ruta de acceso del archivo de registro de errores de clave para cada cubo, grupo de medida, partición y dimensión de la base de datos.  
  
-   **Ubicaciones de almacenamiento** Esta configuración especifica la ubicación de almacenamiento de cada cubo, grupo de medida y partición de la base de datos. Si no se proporciona ningún valor para un objeto, el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizará la ubicación predeterminada para el objeto. Por ejemplo, las particiones utilizan la ubicación para el grupo de medida, los grupos de medida utilizan la ubicación para el cubo y los cubos utilizan la ubicación predeterminada para los objetos de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . La ubicación de almacenamiento puede ser una ruta de acceso UNC (Convención de nomenclatura universal) o local.  
  
-   **Servidor de informes** Esta configuración especifica el servidor de informes y la ubicación de carpeta de cada acción de informe definida en cada cubo de la base de datos.  
  
## <a name="modifying-the-configuration-settings-for-deployment"></a>Modificar los valores de configuración para la implementación  
 En algunos casos, debe implementar la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto usando una configuración distinta a las almacenadas en el \< *nombre del proyecto*> archivo. configSettings. Por ejemplo, puede que desee cambiar la cadena de conexión a uno o más orígenes de datos, o especificar ubicaciones de almacenamiento para particiones o grupos de medida específicos.  
  
 Para modificar la implementación de particiones y roles en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto, debe cambiar esta información dentro de la \< *nombre del proyecto*> .configsettings archivo, como se describe en el siguiente procedimiento. No se puede cambiar la configuración de particiones y roles dentro del proyecto porque el  *\<nombre del proyecto >* **páginas de propiedades** cuadro de diálogo de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] no muestra estas opciones.  
  
> [!NOTE]  
>  Los valores de configuración se pueden aplicar a todos los objetos o solo a los recientemente creados. Aplique los valores de configuración a los objetos recientemente creados solo si implementa objetos adicionales a una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] anteriormente implementada y no desea sobrescribir objetos existentes. Para especificar si los valores de configuración se aplican a todos los objetos o solo a los recientemente creados, establezca esta opción el \< *nombre del proyecto*>. deploymentoptions. Para obtener más información, vea [Especificar opciones de implementación de roles y particiones](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md).  
  
#### <a name="to-change-configuration-settings-after-the-input-files-have-been-generated"></a>Para cambiar los valores de configuración después de haber generado los archivos de entrada  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] interactivamente, y en la página **Valores de configuración** , especifique el valor de configuración para los objetos que vaya a implementar.  
  
     O bien  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el símbolo del sistema y ajuste el asistente de manera que se ejecute en modo de archivo de respuesta. Para obtener más información acerca del modo de archivo de respuesta, vea [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     O bien  
  
-   Modificar el \< *nombre del proyecto*> .configsettings archivo utilizando cualquier editor de texto.  
  
## <a name="see-also"></a>Vea también  
 [Especificar el destino de la instalación](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [Especificar opciones de implementación de roles y particiones](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)   
 [Especificar opciones de procesamiento](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  
