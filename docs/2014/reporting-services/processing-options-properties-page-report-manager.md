---
title: Opciones de procesamiento de la página de propiedades (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 28f07c70-7132-4d15-9505-4fdf31dc9cc0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 524fcaea873128ea4bde6ccdc213a29ec31cc77d
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59939161"
---
# <a name="processing-options-properties-page-report-manager"></a>Página de propiedades Opciones de procesamiento (Administrador de informes)
  Use la página de propiedades Opciones de procesamiento para establecer las propiedades de ejecución de informes del informe actualmente seleccionado. Estas opciones determinan cuándo se produce el procesamiento de datos para el informe. Pueden usarse para recuperar los datos de informe durante las horas de menor actividad. Si tiene un informe al que se obtiene acceso con frecuencia, se pueden almacenar en caché copias temporales del mismo para que los usuarios no tengan que esperar si tienen acceso al mismo informe con diferencia de minutos.  
  
> [!NOTE]  
>  Las características de historial de informes, instantáneas de ejecución y almacenamiento en caché no están disponibles en todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-processing-options-properties-page"></a>Para abrir la página de propiedades Opciones de procesamiento  
  
1.  Abra el Administrador de informes y busque el informe para el que desea establecer las propiedades de procesamiento.  
  
2.  Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página de propiedades General correspondiente al informe.  
  
4.  Seleccione la pestaña **Opciones de procesamiento** .  
  
## <a name="options"></a>Opciones  
 **Ejecutar este informe siempre con los datos más recientes**  
 Use esta opción cuando desee recuperar los datos de informe cuando el usuario selecciona el informe. Si hay una copia almacenada en caché disponible, se devuelve al usuario; en caso contrario, la recuperación de los datos y su representación tienen lugar cuando el usuario selecciona el informe.  
  
 Seleccione **No almacenar en caché copias temporales de este informe** para que el informe siempre se ejecute con los datos más recientes. Cada vez que un usuario abre el informe, se desencadena una consulta en el origen de datos que contiene los datos usados en el informe.  
  
 Seleccione **Guardar en caché una copia temporal del informe**para guardar en caché una copia temporal del informe cuando un usuario lo abra por primera vez. Los usuarios siguientes que ejecuten el informe dentro del período de almacenamiento en caché reciben la copia en caché del informe. El almacenamiento en memoria caché suele mejorar el rendimiento porque se devuelve el informe desde la memoria caché en lugar de procesarse de nuevo.  
  
 Los informes almacenados en caché deben expirar a la larga. Especifique el número de minutos para guardar la copia en caché del informe. Tan pronto como expire una copia temporal, ya no se devolverá de la memoria caché. La próxima vez que un usuario abra el informe, el servidor de informes volverá a procesarlo y colocará una copia del informe actualizado en la caché.  
  
 También se puede programar la expiración de un informe almacenado en caché utilizando una frecuencia que no sean minutos. Por ejemplo, para que un informe almacenado en caché expire al final del día, puede seleccionar una hora concreta de la noche después de la cual la copia deja de ser válida.  
  
 **Representar este informe a partir de una instantánea de ejecución de informes**  
 Use esta opción para recuperar un informe que se ha almacenado como instantánea en un momento que programe. Al elegir esta opción, puede programar el procesamiento de datos para que se produzca durante las horas de poca actividad. A diferencia de las copias almacenadas en caché, que se crean cuando un usuario abre el informe, una instantánea se crea y se actualiza según una programación. Las instantáneas no expiran, sino que siguen activas hasta que son reemplazadas por versiones más recientes.  
  
 Las instantáneas que se generan como resultado de la configuración de ejecución de un informe tienen las mismas características que las instantáneas de un historial de informe. La diferencia consiste en que solo hay una instantánea de ejecución de informes y, teóricamente, muchas de historial de informe. A las instantáneas del historial de informes se obtiene acceso desde la página Historial del informe, que almacena muchas instancias de un informe, según existió en diferentes momentos. Por otra parte, los usuarios obtienen acceso a las instantáneas de ejecución de  informes desde carpetas, como sucede en el caso de los informes activos. En el caso de las instantáneas de ejecución de informes, no existe nada que indique visualmente que el informe es una instantánea.  
  
 Seleccione la opción relacionada de **Crea una instantánea de informe cuando hace clic en el botón Aplicar de esta página** para crear una instantánea de informes al hacer clic en Aplicar. Esto genera la instantánea de informe de forma inmediata para que esté disponible antes de la hora de inicio programada.  
  
 **Tiempo de espera de ejecución de informes**  
 Especifique si el procesamiento del informe debe terminar después de que hayan transcurrido un número de segundos concreto. Si elige el valor predeterminado, para este informe se utilizará el valor de tiempo de espera especificado en la página Configuración del sitio.  
  
 Este valor se aplica al procesamiento de informes en un servidor de informes. No establece un tiempo de espera para el procesamiento de datos en el servidor de bases de datos que proporciona los datos para el informe. Sin embargo, el valor especificado debe ser el suficiente para completar el procesamiento de datos y el procesamiento de informes. El contador de procesamiento del informe empieza cuando se selecciona el informe y termina cuando éste se abre.  
  
## <a name="see-also"></a>Vea también  
 [Establecer las propiedades del procesamiento de informes](report-server/set-report-processing-properties.md)   
 [Informes almacenados en caché &#40;SSRS&#41;](report-server/caching-reports-ssrs.md)   
 [Crear, modificar y eliminar programaciones](subscriptions/create-modify-and-delete-schedules.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
