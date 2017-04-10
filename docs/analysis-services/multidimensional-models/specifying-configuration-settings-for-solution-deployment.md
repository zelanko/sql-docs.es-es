---
title: "Especificar la configuraci&#243;n para la implementaci&#243;n de soluciones | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Asistente para la implementación de Analysis Services, opciones de configuración"
  - "archivos de entrada [Analysis Services]"
  - "configuración, opciones [Analysis Services]"
  - "implementaciones de Analysis Services, opciones de configuración"
  - "implementar [Analysis Services], opciones de configuración"
ms.assetid: 953814a3-85ef-40cc-b46a-d532aa7a6569
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Especificar la configuraci&#243;n para la implementaci&#243;n de soluciones
  El Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lee las opciones de implementación de roles y particiones que se usan en el script de implementación del archivo \<*nombre de proyecto*>.configsettings. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] crea este archivo cuando se genera el proyecto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa los valores de configuración del proyecto actual para crear el archivo \<*nombre de proyecto*>.configsettings.  
  
## Revisar los valores de configuración para implementación  
 A continuación se describen los valores de configuración almacenados en el archivo \<*nombre de proyecto*>.configsettings:  
  
-   **Cadenas de conexión de orígenes de datos** Se trata de las cadenas de conexión para cada origen de datos según los valores especificados en el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . El Id. de usuario y la contraseña siempre se quitan de la cadena de conexión antes de que el resto de la cadena se almacene en este archivo. Sin embargo, si el Asistente para la implementación está implementando directamente en una instancia de Analysis Services, puede agregar la información de Id. de usuario y contraseña correspondiente en el asistente para que el procesamiento de la base de datos de implementación sea correcto. Esta información de conexión no se almacenará en el script de implementación si el Asistente para la implementación guarda  
  
-   **Cuentas de suplantación** Este valor especifica el nombre de usuario que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza para ejecutar instrucciones en cada origen de datos. Si no se especifica ninguna cuenta de suplantación, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizará su cuenta de inicio de sesión para ejecutar instrucciones. Si a la cuenta de inicio de sesión de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se le conceden permisos directamente en el origen de datos, todos los administradores de todas las bases de datos de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tendrán acceso al origen de datos a través de la cuenta de inicio de sesión. Si se especifica una cuenta de usuario y una contraseña, esta información siempre se quita antes de que la información de suplantación se almacene en este archivo. Sin embargo, si el Asistente para la implementación está implementando directamente en una instancia de Analysis Services, puede agregar la información de Id. de usuario y contraseña correspondiente en el asistente para que el procesamiento de la base de datos de implementación sea correcto. Esta información de suplantación no se almacenará en el script de implementación si el Asistente para la implementación guarda uno.  
  
-   **Archivos de registro de errores de clave** Esta configuración especifica el nombre de archivo y la ruta de acceso del archivo de registro de errores de clave para cada cubo, grupo de medida, partición y dimensión de la base de datos.  
  
-   **Ubicaciones de almacenamiento** Esta configuración especifica la ubicación de almacenamiento de cada cubo, grupo de medida y partición de la base de datos. Si no se proporciona ningún valor para un objeto, el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizará la ubicación predeterminada para el objeto. Por ejemplo, las particiones utilizan la ubicación para el grupo de medida, los grupos de medida utilizan la ubicación para el cubo y los cubos utilizan la ubicación predeterminada para los objetos de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . La ubicación de almacenamiento puede ser una ruta de acceso UNC (Convención de nomenclatura universal) o local.  
  
-   **Servidor de informes** Esta configuración especifica el servidor de informes y la ubicación de carpeta de cada acción de informe definida en cada cubo de la base de datos.  
  
## Modificar los valores de configuración para la implementación  
 En algunos casos, puede que necesite implementar el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con valores de configuración diferentes a los almacenados en el archivo \<*nombre de proyecto*>.configsettings. Por ejemplo, puede que desee cambiar la cadena de conexión a uno o más orígenes de datos, o especificar ubicaciones de almacenamiento para particiones o grupos de medida específicos.  
  
 Para modificar la implementación de particiones y roles en un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], deberá cambiar esta información dentro del archivo \<*nombre de proyecto*>.configsettings, como se describe en el siguiente procedimiento. No puede cambiar la configuración de particiones y roles del proyecto porque el cuadro de diálogo **Páginas de propiedades** de *\<nombre de proyecto>* de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] no muestra estas opciones.  
  
> [!NOTE]  
>  Los valores de configuración se pueden aplicar a todos los objetos o solo a los recientemente creados. Aplique los valores de configuración a los objetos recientemente creados solo si implementa objetos adicionales a una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] anteriormente implementada y no desea sobrescribir objetos existentes. Para especificar si los valores de configuración se aplican a todos los objetos o solo a los creados recientemente, establezca esta opción en el archivo \<*nombre de proyecto*>.deploymentoptions. Para obtener más información, vea [Especificar opciones de implementación de roles y particiones](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md).  
  
#### Para cambiar los valores de configuración después de haber generado los archivos de entrada  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] interactivamente, y en la página **Valores de configuración** , especifique el valor de configuración para los objetos que vaya a implementar.  
  
     O bien  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el símbolo del sistema y ajuste el asistente de manera que se ejecute en modo de archivo de respuesta. Para obtener más información acerca del modo de archivo de respuesta, vea [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     O bien  
  
-   Modifique el archivo \<*nombre de proyecto*>.configsettings con cualquier editor de texto.  
  
## Vea también  
 [Especificar el destino de instalación](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)   
 [Especificar opciones de implementación de roles y particiones](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)   
 [Especificar opciones de procesamiento](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
  