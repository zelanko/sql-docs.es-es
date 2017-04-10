---
title: "Configurar el almacenamiento de cadenas para dimensiones y particiones | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 987f6cfc-da82-4b2e-96ef-a8af88339e5f
caps.latest.revision: 21
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 21
---
# Configurar el almacenamiento de cadenas para dimensiones y particiones
  Puede volver a configurar el almacenamiento de cadenas para dar cabida a cadenas muy grandes en los atributos de dimensión o en las particiones que superan el límite de tamaño de archivo de 4 GB para los almacenes de cadenas. Si las dimensiones o las particiones incluyen almacenes de cadenas de este tamaño, puede evitar la restricción del tamaño del archivo si cambia la propiedad **StringStoresCompatibilityLevel** en el nivel de la dimensión o de la partición, tanto en objetos locales como vinculados (locales o remotos).  
  
 Tenga en cuenta que puede aumentar el almacenamiento de cadenas de aquellos objetos que requieren una capacidad adicional. En la mayoría de los modelos multidimensionales, los datos de cadena se asocian con dimensiones. Sin embargo, las particiones que contengan medidas de recuento distintivas encima de las cadenas también pueden beneficiarse de esta configuración. Dado que la configuración es para las cadenas, los datos numéricos no se ven afectados.  
  
 Los valores válidos de esta propiedad incluyen los siguientes:  
  
|Value|Description|  
|-----------|-----------------|  
|**1050**|Especifica la arquitectura predeterminada de almacenamiento de cadenas, que está sujeta a un tamaño de archivo máximo de 4 GB por almacén.|  
|**1100**|Especifica el almacenamiento mayor de cadenas, que admite hasta 4 mil millones de cadenas únicas por almacén.|  
  
> [!IMPORTANT]  
>  Si cambia la configuración del almacenamiento de cadenas de un objeto, será necesario volver a procesar el objeto propiamente dicho y los objetos dependientes. El procesamiento es necesario para completar el procedimiento.  
  
 Este tema contiene las siguientes secciones:  
  
-   [Acerca de los almacenes de cadenas](#bkmk_background)  
  
-   [Requisitos previos](#bkmk_prereq)  
  
-   [Paso 1: establezca la propiedad StringStoreCompatiblityLevel en las Herramientas de datos de SQL Server](#bkmk_step1)  
  
-   [Paso 2: procesar los objetos.](#bkmk_step2)  
  
##  <a name="bkmk_background"></a> Acerca de los almacenes de cadenas  
 La configuración del almacenamiento de cadenas es opcional, lo que significa que incluso las bases de datos creadas usan la arquitectura de almacenamiento de cadenas predefinida, que está sujeta al tamaño máximo de archivo de 4 GB. El uso de la arquitectura de almacenamiento mayor de cadenas tiene un impacto pequeño pero perceptible en el rendimiento. Debe utilizarla solo si los archivos de almacenamiento de cadenas están cercanos o en el límite máximo de 4 GB.  
  
> [!NOTE]  
>  Este valor no se aplica a los modelos de minería de datos. Actualmente, todavía es posible encontrar la limitación de tamaño de archivo de varios GB en los modelos que contienen estructuras de minería de datos.  
  
 En una base de datos multidimensional de Analysis Services, las cadenas se almacenan independientemente de los datos numéricos para permitir optimizaciones basadas en las características de los datos. Los datos de cadena normalmente se encuentran en atributos de dimensión que representan nombres o descripciones. También es posible tener datos de cadena en medidas de recuento distintivas. Los datos de cadena también se pueden usar en las claves.  
  
 Puede identificar un almacén de cadenas por su extensión de archivo (por ejemplo, los archivos asstore, .bstore, .ksstore o .string). De forma predeterminada, cada uno de estos archivos está sujeto a un límite máximo de 4 GB. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], puede invalidar el tamaño máximo de archivo especificando un mecanismo alternativo de almacenamiento que permite que un almacén de cadenas crezca según sea necesario.  
  
 A diferencia de la arquitectura predeterminada de almacenamiento de cadenas que limita el tamaño del archivo físico, el almacenamiento mayor de cadenas se basa en un número máximo de cadenas. El límite máximo para el almacenamiento mayor de cadenas es de 4 mil millones de cadenas únicas o 4 mil millones de registros, lo que ocurra primero. El almacenamiento mayor de cadenas crea registros de un tamaño uniforme, cada uno de los cuales es igual a una página de 64K. Si tiene cadenas muy largas que no caben en un solo registro, el límite efectivo será menor que 4 mil millones de cadenas.  
  
##  <a name="bkmk_prereq"></a> Requisitos previos  
 Debe tener una versión de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o una versión superior de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Las dimensiones y particiones deben usar el almacenamiento MOLAP.  
  
 El nivel de compatibilidad de la base de datos debe estar establecido en 1100. Si creó o implementó una base de datos mediante [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] y la versión [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o una versión superior de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], el nivel de compatibilidad de la base de datos ya está establecido en 1100. Si ha movido una base de datos creada en una versión anterior de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a ssSQL11, debe actualizar el nivel de compatibilidad. Para las bases de datos que desee mover, pero no implementar de nuevo, puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para establecer el nivel de compatibilidad. Para más información, vea [Nivel de compatibilidad de una base de datos multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md).  
  
##  <a name="bkmk_step1"></a> Paso 1: establezca la propiedad StringStoreCompatiblityLevel en las Herramientas de datos de SQL Server  
  
1.  Con [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto que contiene las dimensiones o particiones que desea modificar.  
  
2.  Para cambiar el almacenamiento de cadena para dimensiones, abra el Explorador de soluciones. Haga doble clic en la dimensión cuyo almacenamiento de cadenas está modificando.  
  
3.  En el Diseñador de dimensiones, en el panel Atributos, asegúrese de que está seleccionado el nodo primario de la dimensión (por ejemplo, si la dimensión es Clientes, seleccione Clientes y no uno de los atributos secundarios).  
  
4.  En el panel Propiedades, en la sección Avanzadas, establezca **StringStoresCompatibilityLevel** en **1100**. Repítalo para las demás dimensiones que necesiten un almacenamiento mayor; de lo contrario, deje las dimensiones restantes en el valor **1050** .  
  
5.  Para las particiones, abra un cubo en el Explorador de soluciones.  
  
6.  Haga clic en la pestaña Particiones.  
  
7.  Expanda la partición, seleccione la partición que necesita más memoria adicional y, a continuación, modifique la propiedad **StringStoresCompatibilityLevel** .  
  
8.  Guarde el archivo.  
  
##  <a name="bkmk_step2"></a> Paso 2: procesar los objetos.  
 La nueva arquitectura de almacenamiento se utilizará después de procesar los objetos. El hecho de procesar los objetos también sirve para demostrar que ha resuelto correctamente el problema de la restricción de almacenamiento, porque el error que notificaba previamente una condición de desbordamiento del almacén de cadenas ya no debe volver a aparecer.  
  
-   En el Explorador de soluciones, haga clic con el botón derecho en la dimensión que acaba de modificar y seleccione **Procesar**.  
  
 Debe utilizar la opción Proceso completo con cada objeto que utiliza la nueva arquitectura de almacenamiento de cadenas. Antes de procesar el objeto, asegúrese de ejecutar un análisis de impacto en la dimensión para comprobar si también es necesario reprocesar los objetos dependientes.  
  
## Vea también  
 [Herramientas y enfoques de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)   
 [Opciones y valores de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)   
 [Procesamiento y modos de almacenamiento de particiones](../Topic/Partition%20Storage%20Modes%20and%20Processing.md)   
 [Almacenamiento de dimensiones](../Topic/Dimension%20Storage.md)  
  
  