---
title: Configurar el uso de espacio en disco (PowerPivot para SharePoint) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 201a3fda-f162-45d7-bf39-74dcb92fd0e6
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fbd3fcbe7aa757ac95f225f7da01d7d54116e10b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="configure-disk-space-usage-power-pivot-for-sharepoint"></a>Configurar el uso del espacio en disco (Power Pivot para SharePoint)
  Una implementación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usa el espacio en disco del equipo host para almacenar en memoria caché las bases de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para obtener recargas más rápidas. Cada base de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que se carga en la memoria primero se almacena en la memoria caché del disco para que se pueda volver a cargar rápidamente más tarde para atender las nuevas solicitudes. De forma predeterminada, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usa todo el espacio en disco disponible para almacenar en memoria caché las bases de datos, pero puede modificar este comportamiento estableciendo las propiedades que restringen cuánto espacio en disco se usa.  
  
 En este tema se explica cómo establecer los límites de espacio en disco.  
  
 En este tema no se proporciona orientación para la administración de espacio en disco de las bases de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (insertadas en libros de Excel) que se almacenan en bases de datos de contenido. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pueden ser grandes, con lo que se exige una mayor capacidad de almacenamiento en la granja. Además, si se habilita el control de versiones, podría tener fácilmente varias copias de los datos en la misma base de datos de contenido, con lo que aumenta más la cantidad de espacio en disco necesaria para el almacenamiento del contenido. Aunque las bases de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] son una consideración importante para la administración de disco, no se pueden administrar aparte del contenido almacenado en una granja de SharePoint. Tendrá que supervisar el espacio en disco más estrechamente a medida que aumente el uso de los libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en su negocio. También puede seguir la actividad de los libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en el Panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y quitar los libros que ya no se usen.  
  
## <a name="how-power-pivot-for-sharepoint-manages-cached-databases"></a>Cómo administra Power Pivot para SharePoint las bases de datos almacenadas en memoria caché  
 Para administrar su memoria caché, el Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ejecuta un trabajo en segundo plano a intervalos regulares para limpiar las bases de datos usadas o anticuadas que tienen versiones más recientes de una biblioteca de contenido. El propósito del trabajo de limpieza es descargar las bases de datos inactivas de la memoria y eliminar del sistema de archivos las bases de datos sin usar que están almacenadas en caché. El trabajo de limpieza es para el mantenimiento a largo plazo, con lo que se asegura de que las bases de datos del sistema no se conservan indefinidamente. En un servidor activo, las bases de datos podrían quitarse más a menudo debido a la presión de memoria en el servidor, como la eliminación de SharePoint o a las versiones más recientes de la base de datos en una biblioteca de contenido.  
  
 Aunque no puede programar el trabajo de limpieza, puede personalizar la administración de archivos en caché estableciendo propiedades de configuración del servidor que hacen lo siguiente:  
  
-   Establecer límites en la cantidad de espacio en disco que se usa en la memoria caché.  
  
-   Especificar cuántos datos hay que eliminar cuando se alcanza el espacio máximo en disco.  
  
## <a name="how-to-check-disk-space-usage"></a>Comprobar el uso de espacio en disco  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint se instala en los servidores de aplicaciones de una granja de SharePoint. Cada instalación tiene un directorio de datos que incluye una carpeta de copia de seguridad. La carpeta de copia de seguridad contiene todos los archivos de datos que la instancia de Analysis Services del equipo almacena en memoria caché. De forma predeterminada, la carpeta de copia de seguridad se puede encontrar en la ruta de acceso siguiente:  
  
 `%drive%:\Program Files\Microsoft SQL Server\MSAS10_50.PowerPivot\OLAP\Backup\Sandboxes\<serviceApplicationName>`  
  
 Para comprobar el espacio en disco total que se utiliza en la memoria caché, tiene que comprobar el tamaño de la carpeta de copia de seguridad. No hay ninguna propiedad en Administración central que notifique el tamaño de la memoria caché actual.  
  
 La carpeta de copia de seguridad proporciona un almacenamiento común en memoria caché para cualquier base de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que se cargue en la memoria en el equipo local. Si tiene varias aplicaciones de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] definidas en la granja, cualquiera de ellas puede usar el servidor local para cargar y almacenar después en la memoria caché los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Tanto la carga de datos como el almacenamiento en caché son operaciones de servidor de Analysis Services. Por tanto, el uso total de espacio en disco se administra en las instancias de Analysis Services, en la carpeta de copia de seguridad. La configuración que limita el uso del espacio en disco se establece así en la instancia de SQL Server Analysis Services que se ejecuta en un servidor de aplicaciones de SharePoint.  
  
 La memoria caché solo contiene las bases de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] las bases de datos se almacenan en varios archivos en una sola carpeta principal (la carpeta de copia de seguridad). Dado que las bases de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] están destinadas para usarse como datos internos en un libro de Excel, los nombres de base de datos se basan en los GUID en lugar de ser descriptivos. Una carpeta de GUID en  **\<Nombredeaplicacióndeservicio >** es la carpeta principal de un [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] base de datos. A medida que las bases de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se cargan en el servidor, se crean carpetas adicionales para cada una.  
  
 Dado que los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se pueden cargar en una instancia de Analysis Services de una granja, los mismos datos podrían almacenarse también en memoria caché en varios equipos de la granja. Esta práctica favorece el rendimiento sobre el uso del espacio en disco pero, como contrapartida, los usuarios consiguen un acceso más rápido a los datos si ya están disponibles en el disco.  
  
 Para reducir inmediatamente el consumo de espacio en disco, puede apagar el servicio y eliminar después una base de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de la carpeta de copia de seguridad. Eliminar manualmente archivos es una medida temporal, ya que una copia más reciente de la base de datos se almacenará en memoria caché de nuevo la próxima vez que se consulten los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Una solución definitiva es, por ejemplo, limitar la cantidad de espacio en disco que se usa en la memoria caché.  
  
 En el nivel de sistema, puede crear alertas de correo electrónico que notifiquen que hay poco espacio en disco. Microsoft System Center incluye una característica de alerta por correo electrónico. Para configurar las alertas, también puede utilizar un script de PowerShell, el Administrador de recursos del servidor de archivos o el Programador de tareas. Los vínculos siguientes proporcionan información útil para configurar notificaciones sobre la existencia de poco espacio en disco:  
  
-   [Novedades del Administrador de recursos del servidor de archivos](http://technet.microsoft.com/library/hh831746.aspx) (http://technet.microsoft.com/es-es/library/hh831746.aspx).  
  
-   [Guía paso a paso del Administrador de recursos del servidor de archivos de Windows Server 2008 R2](http://go.microsoft.com/fwlink/?LinkID=204875) (http://go.microsoft.com/fwlink/?LinkID=204875).  
  
-   [Setting low disk space alerts on Windows Server 2008](http://go.microsoft.com/fwlink/?LinkID=204870) (http://go.microsoft.com/fwlink/?LinkID=204870) (Establecer alertas de espacio en disco insuficiente en Windows Server 2008).  
  
## <a name="how-to-limit-the-amount-of-disk-space-used-for-storing-cached-files"></a>Limitar el espacio en disco utilizado para almacenar archivos en memoria caché  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar servicios en el servidor**.  
  
2.  Haga clic en **SQL Server Analysis Services**.  
  
     Observe que los límites se establecen en la instancia de Analysis Services que se ejecuta en el servidor físico y no en el nivel de aplicación de servicio. Todas las aplicaciones de servicio que utilicen la instancia local de Analysis Services están sujetos al mismo límite máximo de espacio en disco que se establece para esa instancia.  
  
3.  En Uso de disco, establezca un valor (en gigas) para **Espacio total en disco** para configurar un límite superior en la cantidad de espacio usado para el almacenamiento en caché. El valor predeterminado es 0, lo que permite que Analysis Services use todo el espacio en disco disponible.  
  
4.  En Uso de disco, en **Eliminar las bases de datos almacenadas en caché en las últimas ‘n’ horas** , especifique los criterios para el uso más reciente para vaciar la memoria caché cuando el espacio en disco llegue al límite máximo.  
  
     El valor predeterminado es 4 horas, lo que significa que todas las bases de datos que han estado inactivas durante cuatro horas o más se eliminan del sistema de archivos. Las bases de datos que están inactivas pero siguen en memoria se descargan y se eliminan del sistema de archivos.  
  
## <a name="how-to-limit-how-long-a-database-is-kept-in-the-cache"></a>Limitar cuánto tiempo se conserva en caché una base de datos  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en **Aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] predeterminada** para abrir el panel de administración.  
  
3.  En Acciones, haga clic en **Configurar las opciones de aplicación de servicio**.  
  
4.  En la sección Caché de disco, puede especificar cuánto tiempo permanece en memoria una base de datos inactiva para atender las nuevas solicitudes (de forma predeterminada, 48 horas) y cuánto tiempo se queda en caché (de forma predeterminada, 120 horas).  
  
     **Mantener base de datos inactiva en memoria** especifica cuánto tiempo permanece en memoria una base de datos inactiva para atender nuevas solicitudes de esos datos. Una base de datos activa se mantiene siempre en memoria mientras que se esté consultando, pero una vez que deja de estar activa, el sistema la mantendrá en memoria durante un período de tiempo adicional por si hay más solicitudes de esos datos.  
  
     Dado que las bases de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] se almacenan en caché primero y después se cargan en memoria, los archivos de base de datos usan el espacio en disco inmediatamente. Sin embargo, mientras la base de datos está activa (y durante las 48 horas posteriores), todas las solicitudes se dirigen en primer lugar a la base de datos en memoria, omitiendo la base de datos en caché. Después de 48 horas de inactividad, el archivo se descarga de la memoria, pero permanece en la memoria caché donde puede volver a cargarse rápidamente si la instancia del servidor local [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] intercepta una nueva solicitud de conexión de esos datos. Las solicitudes de conexión a una base de datos inactiva se sirven desde la memoria caché en lugar de desde la biblioteca de contenido, reduciendo el efecto en las bases de datos de contenido.  
  
     Es importante tener en cuenta que la biblioteca de contenido es la única ubicación permanente para las bases de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Se usan copias en caché solo si la base de datos de la biblioteca es la misma que la copia en el disco.  
  
     **Mantener base de datos inactiva en caché** especifica cuánto tiempo se conserva una base de datos inactiva en el sistema de archivos una vez descargado de la memoria. El trabajo de limpieza usa este valor para determinar qué archivos eliminar. El trabajo de limpieza elimina del disco todas las bases de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que hayan estado inactivas 168 horas (48 horas en memoria y 120 horas en memoria caché).  
  
5.  Haga clic en **Aceptar** para guardar los cambios.  
  
## <a name="next-steps"></a>Pasos siguientes  
 Una instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint proporciona reglas de estado para que pueda realizar una acción correctora cuando se detecten problemas en el estado, la configuración o la disponibilidad del servidor. Algunas de estas reglas utilizan la configuración para determinar las condiciones en las que se desencadenan las reglas de estado. Si va a optimizar activamente el rendimiento del servidor, puede que también desee consultar estos valores para garantizar que los predeterminados son la mejor opción para el sistema. Para más información, vea [Configuración de las reglas de mantenimiento de PowerPivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md).  
  
## <a name="see-also"></a>Vea también  
 [Administración y configuración del servidor de Power Pivot en Administración central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
