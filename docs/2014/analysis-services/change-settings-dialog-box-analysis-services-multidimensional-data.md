---
title: Cuadro de diálogo Cambiar configuración (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.process.batchsettingsdialog.f1
ms.assetid: 0041e042-d7ce-48f9-a690-a6dc65471ff3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 43dfc1dca2e60fe2f5e467556ee36c3add1a9da3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66088250"
---
# <a name="change-settings-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Cambiar configuración (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Cambiar configuración** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] y [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para cambiar la configuración que controla el procesamiento de los objetos enumerados en el cuadro de diálogo **Procesar** . Para mostrar el cuadro de diálogo **Cambiar configuración** , haga clic en **Cambiar configuración** en el cuadro de diálogo **Proceso** .  
  
> [!NOTE]  
>  La configuración especificada en este cuadro de diálogo invalida la configuración heredada de la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para los objetos enumerados en el cuadro de diálogo **Proceso** .  
  
## <a name="options"></a>Opciones  
 **Opciones de procesamiento**  
 Utilice esta pestaña para modificar la configuración relacionada con el orden de procesamiento, la tabla de reescritura y los objetos afectados por la operación de procesamiento. Esta pestaña contiene las siguientes opciones:  
  
 **Paralelo**  
 Haga clic en esta opción para procesar los objetos en paralelo.  
  
 **Tareas paralelas máximas**  
 Seleccione el número máximo de tareas que quiere que la operación de procesamiento ejecute en paralelo o elija **Dejar que el servidor decida** para que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seleccione el número óptimo de tareas paralelas.  
  
 **secuencial**  
 Haga clic en esta opción procesar los objetos de manera secuencial.  
  
 **Modo de transacción**  
 Elija el modo de transacción que se utiliza cuando los objetos se procesan en orden secuencial:  
  
-   **Una transacción** procesa todos los objetos de la misma transacción.  
  
-   **Transacciones independientes** procesa todos los objetos, incluidos los objetos dependientes, en transacciones independientes.  
  
> [!NOTE]  
>  Esta opción solo se habilita si se selecciona **Secuenciales** .  
  
 **Opción de tabla de reescritura**  
 Elija la opción usada para administrar la tabla de reescritura:  
  
-   **Create** crea una tabla de reescritura si no existe. Se produce un error si la tabla de reescritura ya existe.  
  
-   **Crear siempre** crea una tabla de reescritura si no existe o sobrescribe la tabla de reescritura existente si existe.  
  
-   **Usar existente** usa la tabla de reescritura existente si existe. Se produce un error si no existe una tabla de reescritura.  
  
 **Procesar objetos afectados**  
 Seleccione esta opción para incluir y procesar objetos que dependan de otros objetos incluidos en la operación de procesamiento.  
  
 **Errores de clave de dimensión**  
 Utilice esta pestaña para modificar la configuración relacionada con la configuración de errores de la operación de procesamiento. Esta pestaña contiene las siguientes opciones:  
  
 **Usar configuración de error predeterminada**  
 Seleccione esta opción para utilizar la configuración de errores predeterminada para los objetos en la operación de procesamiento.  
  
 **Utilizar la configuración de error personalizada**  
 Seleccione esta opción para definir la configuración de error para los objetos de la operación de procesamiento.  
  
 **Acción de error de clave**  
 Elija una de las siguientes acciones que tienen lugar cuando se encuentra una nueva clave que no se puede buscar durante el procesamiento:  
  
-   **Convert to Unknown** agrega la información del registro en el miembro desconocido.  
  
-   **Descartar registro** excluye la información del registro que se va a procesar con el objeto.  
  
 **Omitir recuento de errores**  
 Haga en esta opción clic para omitir los errores que se producen durante el procesamiento.  
  
 **Detener tras error**  
 Haga clic en esta opción para detener el procesamiento cuando se producen errores. Esta opción habilita las opciones **Número de errores** y **Acción ante el error** .  
  
 **Número de errores**  
 Escriba el número de errores que se ignorarán antes de que el proceso se detenga.  
  
 **Acción en el error**  
 Elija una de las siguientes acciones para que se realice cuando el número de errores supere el valor de **Número de errores**:  
  
-   **Detener el procesamiento** finaliza la operación de procesamiento.  
  
-   **Detener el registro** detiene el registro de errores, pero continúa la operación de procesamiento.  
  
 **No se encontró la clave**  
 Especifique una de las siguientes acciones para que se lleve a cabo cuando no se encuentre una clave al procesar un objeto:  
  
-   **Omitir error** omite el error.  
  
-   **Informar y continuar** notifica el error y continúa la operación de procesamiento.  
  
-   **Notificar y detener** informa del error y detiene la operación de procesamiento.  
  
 **Clave duplicada**  
 Especifique una de las siguientes acciones para que se lleve a cabo si se encuentra una clave duplicada al procesar un objeto:  
  
-   **Omitir error** omite el error.  
  
-   **Informar y continuar** notifica el error y continúa la operación de procesamiento.  
  
-   **Notificar y detener** informa del error y detiene la operación de procesamiento.  
  
 **Clave null convertida en Unknown**  
 Especifique una de las siguientes acciones para que se lleve a cabo cuando se agregue una clave de miembro NULL al miembro desconocido durante el procesamiento de un objeto:  
  
-   **Omitir error** omite el error.  
  
-   **Informar y continuar** notifica el error y continúa la operación de procesamiento.  
  
-   **Notificar y detener** informa del error y detiene la operación de procesamiento.  
  
 **Clave null no permitida**  
 Especifique una de las siguientes acciones para que se lleve a cabo si se encuentra una clave NULL que no está permitida cuando se procesa un objeto:  
  
-   **Omitir error** omite el error.  
  
-   **Informar y continuar** notifica el error y continúa la operación de procesamiento.  
  
-   **Notificar y detener** informa del error y detiene la operación de procesamiento.  
  
 **Ruta de acceso del registro de errores**  
 Escriba la ruta de acceso completa y un nombre para el archivo de registro de errores.  
  
 **Browse**  
 Haga clic en esta acción para abrir el cuadro de diálogo **Abrir** y seleccionar la ruta de acceso completa y el nombre de archivo correspondiente al archivo del registro de errores.  
  
 **Procesar objetos afectados**  
 Haga clic en esta acción para procesar los objetos que dependan de los objetos seleccionados en el cuadro de diálogo **Proceso** .  
  
## <a name="see-also"></a>Consulte también  
 [Analysis Services diseñadores y cuadros de diálogo &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Cuadro de diálogo procesar &#40;Analysis Services-datos multidimensionales&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  
