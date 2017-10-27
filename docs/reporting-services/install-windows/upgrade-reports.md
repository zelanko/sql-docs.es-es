---
title: Actualizar informes | Documentos de Microsoft
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reports [Reporting Services], upgrading
- published reports [Reporting Services], upgrades
- custom report items, upgrading
- Reporting Services, upgrades
- upgrading Reporting Services
- snapshots [Reporting Services], upgrading
- report definition files [Reporting Services]
- .rdl files
ms.assetid: a1a10c67-7462-4562-9b07-a8822188a161
caps.latest.revision: 70
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 640c298b1fbbc22561d04e62e236e683b186ef87
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---

# <a name="upgrade-reports"></a>Actualizar informes

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)]

  Los archivos de definición de informe (.rdl) se actualizan automáticamente de las maneras siguientes:  
  
-   Al abrir un informe en el Diseñador de informes de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], la definición de informe se actualiza al esquema RDL admitido actualmente. Al especificar un servidor de informes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] en las propiedades del proyecto, la definición de informe se guarda en un esquema compatible con el servidor de destino.  
  
-   Al actualizar una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a una instalación de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] , los informes e instantáneas existentes que se han publicado en un servidor de informes se compilan y actualizan automáticamente al nuevo esquema la primera vez que se procesan. Si no se puede actualizar automáticamente un informe, se procesa utilizando el modo de compatibilidad con versiones anteriores. La definición de informe se conserva en el esquema original.  
  
 Los informes no se actualizan al cargar un archivo de definición de informe directamente en el servidor de informes o sitio de SharePoint. La actualización de una definición de informe en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] es la única manera de actualizar el archivo .rdl.  
  
 Cuando un informe se actualiza localmente o en el servidor de informes, puede observar errores, advertencias y mensajes adicionales. Este es el resultado de los cambios en el modelo de objetos de informe interno y en los componentes de procesamiento, que hacen que estos mensajes se muestren cuando se detectan problemas subyacentes en el informe. Para obtener más información, consulte [Reporting Services Backward Compatibility][](../../reporting-services/reporting-services-backward-compatibility.md "compatibilidad con versiones anteriores | Reporting Services").  
  
 Para obtener más información sobre las nuevas características para [! INCLUIR[ssRSCurrent](../what-s-new-in-sql-server-reporting-services-ssrs.md).  

##  <a name="bkmk_versionsupported"></a> Versiones admitidas por la actualización  
 Se pueden actualizar los informes que se crearon en cualquier versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se incluyen las versiones siguientes:  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
##  <a name="bkmk_rdlfiles"></a> Archivos de definición de informe (.rdl) y el Diseñador de informes  
 Un archivo de definición de informe incluye una referencia al espacio de nombres RDL que especifica la versión del esquema de definición de informe que se utiliza para validar el archivo .rdl.  
  
 Cuando se abre un archivo .rdl en el Diseñador de informes en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], si el informe se ha creado para un espacio de nombres anterior, el Diseñador de informes crea automáticamente un archivo de copia de seguridad y actualiza el informe con el espacio de nombres actual. Esta es la única manera en que puede actualizar un archivo de definición de informe.  
  
 Las propiedades de implementación que establece pueden afectar al esquema en el que se guarda el archivo de definición de informe. Para obtener más información, vea [Implementación y compatibilidad de versiones en las herramientas de datos de SQL Server &#40;SSRS&#41;](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
 Puede cargar un archivo .rdl creado en una versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a la nueva versión y se actualiza automáticamente en el primer uso. El servidor de informes almacena el archivo de definición de informe en el formato original. El informe se actualiza automáticamente la primera vez que se ve, pero el archivo de definición de informe almacenado permanece intacto.  
  
 Para identificar el esquema RDL actual para un informe, para un servidor de informes o para el Diseñador de informes, vea [buscar la versión del esquema de definición de informe &#40; SSRS &#41; ](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
##  <a name="bkmk_publishedreports_and_snapshots"></a> Informes publicados e instantáneas de informe  
 Al usarse por primera vez, el servidor de informes intenta actualizar los informes publicados y las instantáneas de informe al nuevo esquema de definición de informe, lo que no requiere ninguna acción concreta del usuario. El intento de actualización tiene lugar cuando el usuario ve un informe o una instantánea de informe, o cuando el servidor de informes procesa una suscripción. La definición de informe no se reemplaza sino que continúa almacenada en el servidor de informes en su esquema original. Si no se puede actualizar un informe, se ejecuta en modo de compatibilidad con versiones anteriores.  
  
##  <a name="bkmk_backcompat"></a> Modo de compatibilidad con versiones anteriores  
 El procesador de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] procesa los informes que se actualizan correctamente. Los informes que no se pueden actualizar se procesan en el procesador de informes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , en el modo de compatibilidad con versiones anteriores. Ambos procesadores de informes no pueden procesar el mismo informe. Al usarse por primera vez, un informe se actualiza correctamente o se marca como compatible con las versiones anteriores.  
  
 Solo el procesador de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] admite las nuevas características. Si un informe no se puede actualizar, aún puede ver el informe representado pero las nuevas características no están disponibles. Para aprovechar las nuevas características, un informe debe actualizarse correctamente.  
  
##  <a name="bkmk_subreports"></a> Actualizar un informe con subinformes  
 Cuando un informe contiene subinformes, durante la actualización se puede dar uno de cuatro estados posibles:  
  
-   El informe principal y todos los subinformes pueden actualizarse correctamente. El procesador de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] los procesa.  
  
-   No se pueden actualizar el informe principal ni ninguno de los subinformes. El procesador de informes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] procesa los informes que se actualizan correctamente.  
  
-   Se puede actualizar el informe principal, pero no se pueden actualizar uno o varios subinformes. El procesador de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] procesa el informe principal, pero el informe representado muestra un mensaje similar a "Error: no se pudo procesar el subinforme" en la ubicación donde aparecería el subinforme que no se pudo actualizar.  
  
-   El informe principal no se puede actualizar, pero se pueden actualizar uno o varios subinformes. El procesador de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] procesa el informe principal, pero el informe representado muestra un mensaje similar a "Error: no se pudo procesar el subinforme" en la ubicación donde aparecería el subinforme.  
  
 Si ve un error similar a "Error: no se pudo procesar el subinforme", debe cambiar la definición del informe principal o del subinforme de modo que la misma versión del procesador de informes pueda procesar los informes.  
  
 Los informes detallados no tienen esta limitación porque se procesan como informes independientes.  
  
##  <a name="bkmk_CRIs"></a> Actualizar un informe con elementos de informe personalizados  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]Los informes de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podrían contener elementos de informe personalizados (CRI) proporcionados por proveedores de software de otros fabricantes que el administrador del sistema podría instalar en el equipo de creación de informes y en el servidor de informes. Los informes que contienen CRI se pueden actualizar de las maneras siguientes:  
  
-   Un servidor de informes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se actualiza a un servidor de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] . Los informes publicados en el servidor de informes se actualizan automáticamente al usarse por primera vez.  
  
-   Un informe de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se carga en un servidor de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] . El informe se actualiza automáticamente al usarse por primera vez.  
  
-   Un informe de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se abre en el Diseñador de informes de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Se crea una copia de seguridad del informe original. Se da uno de los dos casos siguientes:  
  
    1.  Todos los CRI del informe tienen características admitidas. Los CRI se convierten en elementos de informe en el nuevo esquema de definición de informe, de modo que el informe completo se actualiza. Si guarda el archivo, se guarda en el espacio de nombres RDL actual.  
  
    2.  Uno o varios CRI del informe tienen características no admitidas. Un cuadro de diálogo pregunta al usuario si desea convertir los CRI o dejarlos intactos.  
  
     Para obtener más información, vea [Abrir un informe en el Diseñador de informes](#OpeningaReport) , más adelante en este tema.  
  
 Para obtener información acerca de cómo identificar el espacio de nombres RDL actual para un servidor de informes, [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], o un informe, vea [buscar la versión del esquema de definición de informe &#40; SSRS &#41; ](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
### <a name="upgrading-reports-on-a-report-server"></a>Actualizar los informes en un servidor de informes  
 La primera vez que un informe de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se ejecuta en un servidor de informes actualizado a un servidor de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] , el informe se actualiza automáticamente al espacio de nombres de la definición de informe actual que admite el servidor de informes. El informe podría haber existido en el servidor de informes antes de la actualización, podría haberse cargado a través del Administrador de informes o haberse publicado en el servidor de informes desde el Diseñador de informes en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 En la tabla siguiente se muestra la acción de actualización que realiza el servidor de informes para los tipos específicos de CRI de un informe.  
  
|Tipo de CRI|Acción de actualización del servidor de informes|  
|--------------|----------------------------------|  
|CRI de otros proveedores|La actualización no se realiza.<br /><br /> El procesamiento lo realiza el procesador de informes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] procesa los informes que se actualizan correctamente.|  
  
###  <a name="OpeningaReport"></a> Abrir un informe con CRI en el Diseñador de informes  
 Al abrir un informe de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en el Diseñador de informes en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], el informe se actualizará al nuevo esquema de definición de informe. Según los CRI que contenga el informe, tendrá lugar alguna de las acciones siguientes:  
  
-   Se detectan CRI de otros proveedores. Si la versión del CRI que está instalada en el equipo de creación de informes no es compatible con el nuevo esquema de RDL, la superficie de diseño muestra un cuadro de texto con una X roja. Debe ponerse en contacto con el administrador del sistema para instalar las versiones nuevas del CRI de los otros proveedores que sean compatibles con el nuevo esquema de RDL.  
  
 Guardar un informe una vez actualizado en el entorno de creación de informes es la única manera de actualizar un informe existente al nuevo esquema de definición de informe.  
  
###  <a name="bkmk_convertCRIdialog"></a> Cuadro de diálogo Convertir CRI  
 Este informe contiene elementos de informe personalizados (CRI) con características no admitidas. Los CRI son extensiones del lenguaje RDL (Report Definition Language) que admiten objetos personalizados que muestran datos en un informe. Los CRI incluyen componentes de tiempo de diseño y de tiempo de ejecución proporcionados por otros fabricantes de software.  
  
> [!NOTE]  
>  La decisión de admitir elementos de informe personalizados en un servidor de informes debe tomarla el administrador del sistema. Para ver los CRI en un informe, los componentes CRI se deben instalar en el cliente de creación de informes para obtener una vista previa de un informe y se deben instalar en el servidor de informes para ver un informe publicado o cargado. Para obtener más información, vea [Elementos de informe personalizados](../../reporting-services/custom-report-items/custom-report-items.md) y la documentación del fabricante de software correspondiente.  
  
 Algunos CRI se pueden convertir en elementos de informe en el nuevo formato de definición de informe. Use la lista siguiente para decidir si se deben convertir los CRI de este informe:  
  
-   **Sí** : elija **Sí** para convertir todos los CRI del informe, siempre que sea posible. Las características no admitidas de los CRI no se pueden actualizar y se quitan del archivo de definición de informe. Al ver el informe, es posible que observe diferencias en la manera en que se muestran los CRI en el informe.  
  
-   **No** : elija **No** si no desea convertir los CRI del informe. El procesador de informes no puede mostrar la versión actual de estos CRI. Si el administrador del sistema tiene pensado instalar una nueva versión de los CRI de otros fabricantes de software que es compatible con el nuevo formato de definición de informe, debería elegir **No**. Hasta que estén disponibles las nuevas versiones, los CRI se muestran en el informe como un cuadro de texto vacío con una X roja.  
  
 En cualquier caso, el informe se actualiza al nuevo formato de definición de informe y se guarda una copia de seguridad del informe original como  *\<nombre del informe >* `-` Backup.rdl. Si guarda el informe en la herramienta de creación de informes, está guardando el informe actualizado en el nuevo formato de definición de informe. Si publica el informe, éste se guarda primero en su equipo y, a continuación, se publica en el servidor de informes. En realidad, está publicando la versión actualizada del informe en el servidor de informes.  
  
 Si no guarda el informe, el informe original no varía. Sin embargo, no se puede editar este informe en la versión de SQL Server 2016 de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o un entorno que usa un formato de definición de informe más reciente de creación de informes. Puede seguir ejecutando la versión original del informe cargándolo en un [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] servidor de informes mediante el portal web. Para obtener más información, consulte [Portal Web](../../reporting-services/web-portal-ssrs-native-mode.md).  
  
 En el caso de los informes cargados, no publicados, en un servidor de informes, el procesador de informes determina si se pueden actualizar al usarse por primera vez. Los informes que no se pueden actualizar se procesan en el modo de compatibilidad con versiones anteriores y siguen mostrándose igual que en la versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  

## <a name="next-steps"></a>Pasos siguientes

[Actualizar y migrar Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Cambios substanciales de SQL Server Reporting Services en SQL Server 2016](../../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md)   
[Cambios de comportamiento de SQL Server Reporting Services en SQL Server 2016](../../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md)   
[Funcionalidad de SQL Server Reporting Services no incluida en SQL Server 2016](../../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
[Elementos de informe personalizados](../../reporting-services/custom-report-items/custom-report-items.md)   
[Actualización de una base de datos del servidor de informes](../../reporting-services/install-windows/upgrade-a-report-server-database.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).

