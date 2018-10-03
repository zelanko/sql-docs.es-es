---
title: Actualizar informes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
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
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 1caf710a55ee548f7939ec65ead6397ccd4092d4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48179325"
---
# <a name="upgrade-reports"></a>Upgrade Reports
  Los archivos de definición de informe (.rdl) se actualizan automáticamente de las maneras siguientes:  
  
-   Al abrir un informe en el Diseñador de informes de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], la definición de informe se actualiza al esquema RDL admitido actualmente. Cuando se especifica un [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] el servidor de informes en las propiedades del proyecto, la definición de informe se guarda en un esquema que es compatible con el servidor de destino.  
  
-   Al actualizar una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a una instalación de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] , los informes e instantáneas existentes que se han publicado en un servidor de informes se compilan y actualizan automáticamente al nuevo esquema la primera vez que se procesan. Si no se puede actualizar automáticamente un informe, se procesa utilizando el modo de compatibilidad con versiones anteriores. La definición de informe se conserva en el esquema original.  
  
 Los informes no se actualizan al cargar un archivo de definición de informe directamente en el servidor de informes o sitio de SharePoint. La actualización de una definición de informe en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] es la única manera de actualizar el archivo .rdl.  
  
 Cuando un informe se actualiza localmente o en el servidor de informes, puede observar errores, advertencias y mensajes adicionales. Este es el resultado de los cambios en el modelo de objetos de informe interno y en los componentes de procesamiento, que hacen que estos mensajes se muestren cuando se detectan problemas subyacentes en el informe. Para obtener más información, vea [Compatibilidad con versiones anteriores de Reporting Services](../reporting-services-backward-compatibility.md).  
  
 Para obtener más información sobre las nuevas características para [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], consulte [What ' s New &#40;Reporting Services&#41;](../what-s-new-reporting-services.md).  
  
 En este tema:  
  
-   [Versiones admitidas por la actualización](#bkmk_versionsupported)  
  
-   [Archivos de definición de informe (.rdl) y el Diseñador de informes](#bkmk_rdlfiles)  
  
-   [Informes publicados e instantáneas de informe](#bkmk_publishedreports_and_snapshots)  
  
-   [Modo de compatibilidad con versiones anteriores](#bkmk_backcompat)  
  
-   [Actualizar un informe con subinformes](#bkmk_subreports)  
  
-   [Actualizar un informe con elementos de informe personalizados](#bkmk_CRIs)  
  
-   [Cuadro de diálogo Convertir CRI](#bkmk_convertCRIdialog)  
  
##  <a name="bkmk_versionsupported"></a> Versiones admitidas por la actualización  
 Se pueden actualizar los informes que se crearon en cualquier versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se incluyen las versiones siguientes:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 con Service Pack 1  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 con Service Pack 2  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
##  <a name="bkmk_rdlfiles"></a> Archivos de definición de informe (.rdl) y el Diseñador de informes  
 Un archivo de definición de informe incluye una referencia al espacio de nombres RDL que especifica la versión del esquema de definición de informe que se utiliza para validar el archivo .rdl.  
  
 Cuando se abre un archivo .rdl en el Diseñador de informes en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], si el informe se ha creado para un espacio de nombres anterior, el Diseñador de informes crea automáticamente un archivo de copia de seguridad y actualiza el informe con el espacio de nombres actual. Esta es la única manera en que puede actualizar un archivo de definición de informe.  
  
 Las propiedades de implementación que establece pueden afectar al esquema en el que se guarda el archivo de definición de informe. Para obtener más información, vea [Implementación y compatibilidad de versiones en las herramientas de datos de SQL Server &#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
 Puede cargar un archivo .rdl creado en una versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a un servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y se actualiza automáticamente al usarse por primera vez. El servidor de informes almacena el archivo de definición de informe en el formato original. El informe se actualiza automáticamente la primera vez que se ve, pero el archivo de definición de informe almacenado permanece intacto.  
  
> [!NOTE]  
>  Un informe que tenga el espacio de nombres de definición de informe de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no se puede publicar ni cargar en un servidor de informes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
 Para identificar el esquema RDL actual de un informe, un servidor de informes o del Diseñador de informes, vea [Buscar la versión del esquema de definición de informe &#40;SSRS&#41;](../reports/find-the-report-definition-schema-version-ssrs.md).  
  
##  <a name="bkmk_publishedreports_and_snapshots"></a> Informes publicados e instantáneas de informe  
 Al usarse por primera vez, el servidor de informes intenta actualizar los informes publicados y las instantáneas de informe al nuevo esquema de definición de informe, lo que no requiere ninguna acción concreta del usuario. El intento de actualización tiene lugar cuando el usuario ve un informe o una instantánea de informe, o cuando el servidor de informes procesa una suscripción. La definición de informe no se reemplaza sino que continúa almacenada en el servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en su esquema original. Si no se puede actualizar un informe, se ejecuta en modo de compatibilidad con versiones anteriores.  
  
##  <a name="bkmk_backcompat"></a> Modo de compatibilidad con versiones anteriores  
 El procesador de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] procesa los informes que se actualizan correctamente. Procesa un informe que no se puede actualizar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] procesador en el modo de compatibilidad con versiones anteriores de informes. Ambos procesadores de informes no pueden procesar el mismo informe. Al usarse por primera vez, un informe se actualiza correctamente o se marca como compatible con las versiones anteriores.  
  
 Solo el procesador de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] admite las nuevas características. Si un informe no se puede actualizar, aún puede ver el informe representado pero las nuevas características no están disponibles. Para aprovechar las nuevas características, un informe debe actualizarse correctamente.  
  
##  <a name="bkmk_subreports"></a> Actualizar un informe con subinformes  
 Cuando un informe contiene subinformes, durante la actualización se puede dar uno de cuatro estados posibles:  
  
-   El informe principal y todos los subinformes pueden actualizarse correctamente. El procesador de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] los procesa.  
  
-   No se pueden actualizar el informe principal ni ninguno de los subinformes. Se procesó el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] procesador de informes.  
  
-   Se puede actualizar el informe principal, pero no se pueden actualizar uno o varios subinformes. El procesador de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] procesa el informe principal, pero el informe representado muestra un mensaje similar a "Error: no se pudo procesar el subinforme" en la ubicación donde aparecería el subinforme que no se pudo actualizar.  
  
-   El informe principal no se puede actualizar, pero se pueden actualizar uno o varios subinformes. El procesador de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] procesa el informe principal, pero el informe representado muestra un mensaje similar a "Error: no se pudo procesar el subinforme" en la ubicación donde aparecería el subinforme.  
  
 Si ve un error similar a "Error: no se pudo procesar el subinforme", debe cambiar la definición del informe principal o del subinforme de modo que la misma versión del procesador de informes pueda procesar los informes.  
  
 Los informes detallados no tienen esta limitación porque se procesan como informes independientes.  
  
##  <a name="bkmk_CRIs"></a> Actualizar un informe con elementos de informe personalizados  
 Los informes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podrían contener elementos de informe personalizados (CRI) proporcionados por proveedores de software de otros fabricantes que el administrador del sistema podría instalar en el equipo de creación de informes y en el servidor de informes. Los informes que contienen CRI se pueden actualizar de las maneras siguientes:  
  
-   Un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servidor de informes se actualiza a un [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] servidor de informes. Los informes publicados en el servidor de informes se actualizan automáticamente al usarse por primera vez.  
  
-   Un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] informe se carga en un [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] servidor de informes. El informe se actualiza automáticamente al usarse por primera vez.  
  
-   Un informes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se abre en el Diseñador de informes de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Se crea una copia de seguridad del informe original. Se da uno de los dos casos siguientes:  
  
    1.  Todos los CRI del informe tienen características admitidas. Los CRI se convierten en elementos de informe en el nuevo esquema de definición de informe, de modo que el informe completo se actualiza. Si guarda el archivo, se guarda en el espacio de nombres RDL actual.  
  
    2.  Uno o varios CRI del informe tienen características no admitidas. Un cuadro de diálogo pregunta al usuario si desea convertir los CRI o dejarlos intactos.  
  
     Para obtener más información, vea [Abrir un informe en el Diseñador de informes](#OpeningaReport) , más adelante en este tema.  
  
 Para más información sobre cómo identificar el espacio de nombres RDL actual para un servidor de informes, [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o un informe, vea [Buscar la versión del esquema de definición de informe &#40;SSRS&#41;](../reports/find-the-report-definition-schema-version-ssrs.md).  
  
### <a name="upgrading-reports-on-a-report-server"></a>Actualizar los informes en un servidor de informes  
 La primera vez un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] informe se ejecuta en un servidor de informes que se ha actualizado a un [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] servidor de informes, el informe se actualiza automáticamente a admitidos por el servidor de informes uno de los nombres de definición de informe actual. El informe podría haber existido en el servidor de informes antes de la actualización, o podría haberse cargado a través del Administrador de informes o haberse publicado en el servidor de informes desde el Diseñador de informes en el informe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 En la tabla siguiente se muestra la acción de actualización que realiza el servidor de informes para los tipos específicos de CRI de un informe.  
  
|Tipo de CRI|Acción de actualización del servidor de informes|  
|--------------|----------------------------------|  
|CRI de otros proveedores|La actualización no se realiza.<br /><br /> Los procesa el procesador de informes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|CRI de gráficos de Dundas 2005 con características admitidas|Se actualizan al esquema RDL más reciente. Todos los CRI de gráficos de Dundas 2005 se convierten en regiones de datos de gráfico compatibles con [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].<br /><br /> Los procesa el procesador de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].|  
|CRI de Dundas 2005 Gauge con características admitidas|Se actualizan al esquema RDL más reciente. Todos los Dundas 2005 gauge se convierten para medir las regiones de datos que son compatibles con [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]<br /><br /> Los procesa el procesador de informes de [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)].|  
|CRI de Dundas 2005 Chart con características no admitidas|La actualización no se realiza.<br /><br /> Los procesa el procesador de informes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
|CRI de Dundas 2005 Gauge con características no admitidas|La actualización no se realiza.<br /><br /> Los procesa el procesador de informes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
###  <a name="OpeningaReport"></a> Abrir un informe con CRI en el Diseñador de informes  
 Al abrir un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] informe con CRI en el Diseñador de informes en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], el informe se actualizará al nuevo esquema de definición de informe. Según los CRI que contenga el informe, tendrá lugar alguna de las acciones siguientes:  
  
-   Se detectan CRI de otros proveedores. Si la versión del CRI que está instalada en el equipo de creación de informes no es compatible con el nuevo esquema de RDL, la superficie de diseño muestra un cuadro de texto con una X roja. Debe ponerse en contacto con el administrador del sistema para instalar las versiones nuevas del CRI de los otros proveedores que sean compatibles con el nuevo esquema de RDL.  
  
-   Se detectan CRI de Dudas 2005 Chart o de Dundas 2005 Gauge, y todas las instancias contienen una funcionalidad admitida. Todos los CRI de Dundas 2005 Chart o de Dundas 2005 Gauge se convierten en los elementos de informes de gráficos y medidores de Reporting Services que se ven en el cuadro de herramientas. Se conocen como elementos de informe de gráficos y medidores nativos.  
  
-   Se detectan CRI de Dundas 2005 Chart o de Gauge Dundas 2005 y alguna instancia tiene cierta funcionalidad no admitida. La funcionalidad no admitida se describe después de esta sección. Puede decidir si convertir todos los CRI en elementos de informe nativos.  
  
    -   Si los convierte, el informe se actualiza al nuevo esquema de RDL y los CRI de Dundas 2005 Chart y de Dundas 2005 Gauge se convierten en los elementos de informe de medidores y gráficos nativos correspondientes, pero se quita la funcionalidad no admitida. En el informe representado, podría ver diferencias en el modo en que se muestra el CRI.  
  
    -   Si decide no convertirlos, el informe se actualiza al nuevo esquema de RDL pero los CRI se tratan como si fueran de otros proveedores. Debe trabajar con el administrador del sistema y los otros proveedores para instalar CRI nuevos que sean compatibles con el nuevo esquema de informe. Si no hay disponibles CRI nuevos, el informe muestra un cuadro de texto con una X roja en el Diseñador de informes.  
  
 Guardar un informe una vez actualizado en el entorno de creación de informes es la única manera de actualizar un informe existente al nuevo esquema de definición de informe.  
  
### <a name="unsupported-dundas-2005-chart-custom-report-item-functionality"></a>Funcionalidad no admitida de los elementos de informe personalizados de gráficos de Dundas 2005  
 Entre la funcionalidad no admitida para los CRI de gráficos de Dundas 2005 se incluyen las características siguientes:  
  
-   Anotaciones.  
  
-   Elementos de leyenda personalizados.  
  
-   Atributos personalizados con los nombres siguientes:  
  
    -   CUSTOM_CODE_CS  
  
    -   CUSTOM_CODE_VB  
  
    -   CUSTOM_CODE_COMPILED_ASSEMBLY  
  
         Por ejemplo, si un archivo .rdl contiene la sección siguiente, tendrá que quitarla antes de actualizar:  
  
        ```  
        <CustomProperty>  
         <Name>CUSTOM_CODE_CS</Name>  
         <Value>dXNpWERwegfdfgiobxxl3bmc… </Value>  
        </CustomProperty>  
        ```  
  
### <a name="unsupported-dundas-2005-gauge-custom-report-item-functionality"></a>Funcionalidad no admitida de los elementos de informe personalizados de medidores de Dundas 2005  
 Entre la funcionalidad no admitida para los CRI de medidores de Dundas 2005 se incluyen las características siguientes:  
  
-   Indicadores numéricos.  
  
-   Indicadores de estado.  
  
-   Imágenes personalizadas.  
  
###  <a name="bkmk_convertCRIdialog"></a> Cuadro de diálogo Convertir CRI  
 Este informe contiene elementos de informe personalizados (CRI) con características no admitidas. Los CRI son extensiones del lenguaje RDL (Report Definition Language) que admiten objetos personalizados que muestran datos en un informe. Los CRI incluyen componentes de tiempo de diseño y de tiempo de ejecución proporcionados por otros fabricantes de software.  
  
> [!NOTE]  
>  La decisión de admitir elementos de informe personalizados en un servidor de informes debe tomarla el administrador del sistema. Para ver los CRI en un informe, los componentes CRI se deben instalar en el cliente de creación de informes para obtener una vista previa de un informe y se deben instalar en el servidor de informes para ver un informe publicado o cargado. Para obtener más información, consulte [elementos de informe personalizados](../custom-report-items/custom-report-items.md) y la documentación del proveedor del software de terceros.  
  
 Algunos CRI se pueden convertir en elementos de informe en el nuevo formato de definición de informe. Para obtener la lista de CRI que se pueden convertir, vea [actualizar informes](upgrade-reports.md). Use la lista siguiente para decidir si se deben convertir los CRI de este informe:  
  
-   **Sí** : elija **Sí** para convertir todos los CRI del informe, siempre que sea posible. Las características no admitidas de los CRI no se pueden actualizar y se quitan del archivo de definición de informe. Para obtener la lista de características no admitidas, consulte [actualizar informes](upgrade-reports.md). Al ver el informe, es posible que observe diferencias en la manera en que se muestran los CRI en el informe.  
  
-   **No** : elija **No** si no desea convertir los CRI del informe. El procesador de informes no puede mostrar la versión actual de estos CRI. Si el administrador del sistema tiene pensado instalar una nueva versión de los CRI de otros fabricantes de software que es compatible con el nuevo formato de definición de informe, debería elegir **No**. Hasta que estén disponibles las nuevas versiones, los CRI se muestran en el informe como un cuadro de texto vacío con una X roja.  
  
 En cualquier caso, el informe se actualiza al nuevo formato de definición de informe y se guarda una copia de seguridad del informe original como *\<Nombre del informe>* `-` Backup.rdl. Si guarda el informe en la herramienta de creación de informes, está guardando el informe actualizado en el nuevo formato de definición de informe. Si publica el informe, éste se guarda primero en su equipo y, a continuación, se publica en el servidor de informes. En realidad, está publicando la versión actualizada del informe en el servidor de informes.  
  
 Si no guarda el informe, el informe original no varía. Sin embargo, no podrá modificar este informe en la versión para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ni en un entorno de creación de informes que use un formato de definición de informes más nuevo. Puede seguir ejecutando la versión original del informe cargándolo en un [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] servidor de informes mediante el Administrador de informes. Para más información, vea [Cargar un archivo o un informe &#40;Administrador de informes&#41;](../reports/upload-a-file-or-report-report-manager.md).  
  
 En el caso de los informes cargados, no publicados, en un servidor de informes, el procesador de informes determina si se pueden actualizar al usarse por primera vez. Los informes que no se pueden actualizar se procesan en el modo de compatibilidad con versiones anteriores y siguen mostrándose igual que en la versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Actualizar y migrar Reporting Services](upgrade-and-migrate-reporting-services.md)   
 [Cambios importantes en SQL Server Reporting Services en SQL Server 2014](../breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)   
 [Cambios de comportamiento en SQL Server Reporting Services en SQL Server 2014](../behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [Funcionalidad no incluida en SQL Server Reporting Services en SQL Server 2014](../discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)   
 [Elementos de informe personalizados](../custom-report-items/custom-report-items.md)   
 [Actualización de una base de datos del servidor de informes](upgrade-a-report-server-database.md)  
  
  
