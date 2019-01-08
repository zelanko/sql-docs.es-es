---
title: Configurar la recopilación de datos de uso para (PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 955ca6d6-9d5b-47a4-a87c-59bd23f1bf74
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f3544ce4297117be11b3ba68821e3b621fbc400
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52411282"
---
# <a name="configure-usage-data-collection-for-powerpivot-for-sharepoint"></a>Configurar la recolección de datos de uso para PowerPivot para SharePoint
  La recopilación de datos de uso es una característica propia de SharePoint para las granjas. PowerPivot para SharePoint usa y extiende este sistema para proporcionar informes en el panel de administración de PowerPivot que muestran cómo se usan los datos y servicios PowerPivot. Según cómo haya instalado SharePoint, la recopilación de datos de uso podría estar desactivada para la granja. El administrador de una granja debe habilitar el registro de uso para crear los datos de uso que aparecen en el Panel de administración de PowerPivot.  
  
 Para obtener información sobre los datos de uso en el Panel de administración de PowerPivot, vea [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md).  
  
 **En este tema:**  
  
 [Habilitar la recopilación de datos de uso y elegir los eventos que la desencadenan](#events)  
  
 [Establecer la ubicación de los archivos de registro](#configdb)  
  
 [Configurar los trabajos de temporizador utilizados en la recopilación de datos de uso](#jobs)  
  
 [Limitar durante cuánto tiempo se almacena el historial de datos de uso](#confighist)  
  
 [Definir las categorías de respuesta a las consultas rápida, media y lenta a efectos de los informes](#qrh)  
  
 [Especificar con qué frecuencia se notifican las estadísticas de consulta al sistema de recopilación de datos de uso](#ttr)  
  
 [Abra la página de aplicación de servicio PowerPivot en la configuración de acceso](#openconfig)  
  
 [La configuración predeterminada para la recopilación de datos de uso de PowerPivot](#defaultconfig)  
  
> [!IMPORTANT]  
>  Los datos de uso proporcionan una visión general de la forma en que los usuarios tienen acceso a los datos y los recursos, pero no garantizan la confiabilidad ni la persistencia de los datos en las operaciones del servidor y el acceso de los usuarios. Por ejemplo, si se reinicia un servidor, los datos de uso del evento se perderán y no se podrán recuperar. De igual forma, si los archivos de registro temporales alcanzan el tamaño máximo, no se agregarán nuevos datos hasta que se borren los archivos. Si requiere la capacidad de auditoría, considere usar las características de tipo de contenido y flujo de trabajo que SharePoint proporciona para generar un subsistema de auditoría para la granja. Para obtener más información, busque en la documentación de la comunidad y del producto en Internet.  
  
##  <a name="events"></a> Habilitar la recopilación de datos de uso y elegir los eventos que la desencadenan  
 Configurar la recopilación de datos de uso en Administración central de SharePoint.  
  
1.  En Administración central, haga clic en **Supervisión**.  
  
2.  En la sección **Informes**, haga clic en **Configurar la recolección de datos de uso y estado**.  
  
3.  Active **Habilitar la recolección de datos de uso**.  
  
4.  En la sección **Eventos para registrar** , active o desactive las casillas correspondientes para habilitar o deshabilitar los siguientes eventos de Analysis Services:  
  
    |Evento|Descripción|  
    |-----------|-----------------|  
    |**Conexiones de PowerPivot**|El evento de conexión de PowerPivot se utiliza para supervisar las conexiones al servidor de PowerPivot que se realizan en nombre de un usuario.|  
    |**Uso de datos de carga de PowerPivot**|El uso de datos de descarga de PowerPivot se utiliza para supervisar las solicitudes que cargan datos PowerPivot en la memoria del servidor. Un evento de carga se genera para los archivos de datos PowerPivot cargados desde una base de datos de contenido o desde la memoria caché.|  
    |**Uso de datos de descarga de PowerPivot**|El uso de datos de descarga de PowerPivot se utiliza para supervisar las solicitudes de descarga de un origen de datos PowerPivot después de un período de inactividad. El almacenamiento en memoria caché de un origen de datos PowerPivot en el disco se notificará como un evento de descarga.|  
    |**Uso de consultas de PowerPivot**|Uso de consultas de PowerPivot se emplea para supervisar los tiempos de procesamiento de las consultas para los datos que se cargan en una instancia de [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] .|  
  
    > [!NOTE]  
    >  El estado del servidor y las operaciones de actualización de datos también generan datos de uso, pero no hay ningún evento asociado a estos procesos.  
  
5.  También puede actualizar la ubicación de los archivos de registro. Para obtener más información, vea la próxima sección.  
  
6.  Haga clic en **Aceptar** para guardar los cambios.  
  
7.  Opcionalmente, puede especificar si se registran todos los mensajes o solo los errores. Para obtener más información acerca de cómo limitar los mensajes de eventos, consulte [configurar y ver archivos de registro de SharePoint y el registro de diagnóstico &#40;PowerPivot para SharePoint&#41;](configure-and-view-sharepoint-and-diagnostic-logging.md).  
  
##  <a name="configdb"></a> Establecer la ubicación de los archivos de registro  
 Los datos de uso de PowerPivot se almacenan inicialmente en archivos de registro de uso en el servidor local y, a continuación, se mueven periódicamente a las bases de datos de aplicación de servicio PowerPivot. La ubicación de los archivos de registro se establece en Administración central. La ubicación predeterminada es:  
  
 `C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\logs`  
  
 Para ver o cambiar estas propiedades, use la página **Recolección de datos de uso y estado** .  
  
1.  En la página Inicio de Administración central, haga clic en **Supervisión**.  
  
2.  En la sección de creación de informes, haga clic **Configurar la recopilación de datos de uso y estado**.  
  
3.  En Configuración de la recopilación de datos de uso, vea o modifique la ubicación, el nombre o el tamaño máximo del archivo. Si especifica un tamaño de archivo que es demasiado bajo, alcanzará el límite máximo y no se agregarán entradas nuevas hasta que su contenido se mueva a la base de datos central de recopilación de datos de uso.  
  
##  <a name="jobs"></a> Configurar los trabajos de temporizador utilizados en la recopilación de datos de uso  
 Los datos de estado y de uso de servidor de PowerPivot se mueven a ubicaciones diferentes en el sistema de recopilación de datos de uso mediante dos trabajos de temporizador:  
  
-   El trabajo de temporizador "Importación de datos de uso de Microsoft SharePoint Foundation" mueve el uso de PowerPivot a la base de datos de aplicación de servicio PowerPivot.  
  
-   El "trabajo de temporizador de procesamiento del panel de administración de PowerPivot" los datos al libro PowerPivot que sea el origen de datos para los informes administrativos integrados.  
  
 Si necesita actualizar los informes administrativos que aparecen con más frecuencia en el Panel de administración de PowerPivot, siga estos pasos.  
  
1.  En Administración central, haga clic en **Supervisión**.  
  
2.  Haga clic en **Revisar definiciones de trabajo** En la sección **Trabajos del temporizador** .  
  
3.  Haga clic en **Importación de datos de uso de Microsoft SharePoint Foundation**.  
  
4.  Haga clic en **Ejecutar ahora**. Si el botón **Ejecutar ahora** está deshabilitado, haga clic en **Habilitar** y, a continuación, haga clic en **Ejecutar ahora**.  
  
5.  En la lista Definiciones de trabajo, haga clic en **Trabajo de temporizador de procesamiento del panel de administración de PowerPivot**.  
  
6.  Haga clic en **Ejecutar ahora**.  
  
7.  Compruebe los informes para ver los datos de la actualización. Para obtener más información, vea [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md).  
  
##  <a name="confighist"></a> Limitar durante cuánto tiempo se almacena el historial de datos de uso  
 El historial de datos de uso se almacena para los eventos (conexiones, carga, descarga y procesamiento de consultas a petición) y la actualización de datos (procesamiento de datos programado). Aunque los datos de uso se recopilan a través del sistema de recopilación de datos de uso de SharePoint, los datos de los informes se mueven a una base de datos de aplicación de PowerPivot y a una base de datos de informes para conseguir un almacenamiento a más largo plazo. La configuración del historial de datos de uso controla cuánto tiempo se conservan en las bases de datos de aplicación de PowerPivot. El mismo límite se aplica por igual a todos los tipos de datos de uso almacenados en la misma base de datos de aplicación de servicio PowerPivot.  
  
1.  [Abra la página Aplicación de servicio PowerPivot](#openconfig).  
  
2.  En la sección **Recolección de datos de uso** , en **Historial de datos de uso**, escriba el número de días para los que desea mantener un registro de actividad de la actualización de datos para cada libro.  
  
    -   El valor predeterminado es 365 días.  
  
    -   0 especifica un almacenamiento ilimitado; los datos de uso se mantienen indefinidamente.  
  
    -   O bien, puede especificar un intervalo entre 1 y 5000.  
  
     Al disminuir el período de retención a un número menor de días, se eliminará cualquier dato que supere el nuevo límite. Por ejemplo, cambiar el valor de 365 a 30 ocasionará la eliminación de los datos de uso de toda la información histórica que se produjera hace más de 30 días. Solo se retienen los datos de los últimos 30 días.  
  
     Los datos se eliminan realmente cuando se produce el evento siguiente. El límite del historial de datos de uso solo se comprueba cuando el sistema procesa un evento.  
  
3.  Haga clic en **Aceptar**.  
  
 Para obtener más información acerca de cómo se recopilan y almacenan los datos de uso, consulte [PowerPivot Usage Data Collection](power-pivot-usage-data-collection.md).  
  
##  <a name="qrh"></a> Definir las categorías de respuesta a las consultas rápida, media y lenta a efectos de los informes  
 El rendimiento del procesamiento de las consultas se mide con las categorías predefinidas que definen un ciclo de solicitud-respuesta con el tiempo que se tarda en completarse. Las categorías predefinidas son: Trivial, Rápida, Esperada, Larga ejecución y Superado. Cada solicitud para un servidor de PowerPivot pertenecerá a una de las categorías en función del tiempo que tarde en completarse.  
  
 La información de las respuestas a las consultas se utiliza en los informes de actividad. Dentro de los informes, cada categoría se utiliza de manera diferente para revelar mejor las tendencias de rendimiento del sistema de PowerPivot. Las solicitudes triviales se excluyen completamente, por ejemplo, porque de ese modo se quita el ruido en los datos y se muestran las tendencias más significativas mediante las categorías restantes. Por el contrario, las estadísticas de solicitudes de ejecución prolongada o superadas se destacan en el informe para que los administradores o los propietarios de los libros puedan emprender la acción correctora inmediatamente.  
  
 Aunque no puede agregar ni eliminar categorías, puede definir los límites superior e inferior que determinan dónde termina una categoría y dónde comienza la siguiente. Si una organización utiliza contratos de nivel de servicio (SLA) para definir los niveles aceptables de disponibilidad y el rendimiento de los servidores, puede ajustar estas categorías para reflejar el Contrato de nivel de servicio que cree.  
  
1.  [Abra la página Aplicación de servicio PowerPivot](#openconfig).  
  
2.  En la sección **Recolección de datos de uso** , en **Límite superior de respuesta trivial** , especifique un valor (en milisegundos) que establezca el límite superior para completar una respuesta trivial. Algunas solicitudes que no entran en esta categoría normalmente son, entre otras, los pings de servidor, la iniciación de las sesiones y las consulta de metadatos. El valor predeterminado es 500 milisegundos (o medio segundo).  
  
3.  Como límite superior de las solicitudes rápidas, especifique un valor (en milisegundos) que establezca el límite superior para completar una respuesta rápida. Las solicitudes que entran en esta categoría son, entre otras, las consultas de conjuntos de datos muy pequeños o servidores de metadatos de conjuntos de datos grandes. El valor predeterminado es 1000 milisegundos (o un segundo).  
  
4.  En **Límite superior de respuesta esperada**, especifique un valor (en milisegundos) que establezca el límite superior para completar una respuesta en un plazo de tiempo promedio o esperado. Entre las solicitudes que entran en esta categoría se incluyen las de carga de datos en un visor. El valor predeterminado es de 3000 milisegundos (o tres segundos).  
  
5.  En **Límite superior de respuesta larga**, especifique un valor (en milisegundos) que establezca el límite superior para completar una respuesta de ejecución prolongada. Las solicitudes que entran en esta categoría se ejecutan mucho más tiempo de lo esperado, pero dentro de un intervalo que todavía es aceptable. El valor predeterminado es de 10000 milisegundos (o diez segundos).  
  
     Cualquier solicitud que supere este límite se clasifica como *Superada*. No hay ningún umbral configurable para *Superada*. Se deduce del límite superior que especifique como límite superior de las solicitudes de ejecución prolongada. Las solicitudes que entran en la categoría Superada se ejecutan más tiempo de lo que se permite en el contrato de nivel de servicio que se haya definido.  
  
6.  Haga clic en **Aceptar**.  
  
##  <a name="ttr"></a> Especificar con qué frecuencia se notifican las estadísticas de consulta al sistema de recopilación de datos de uso  
 El intervalo de tiempo de informe especifica la frecuencia con que las estadísticas de consulta se notifican al sistema de recopilación de datos de uso. Las estadísticas de consulta se acumulan en un proceso y se notifican como un evento único a intervalos regulares. Puede ajustar el intervalo para escribir más o menos a menudo en el archivo de registro.  
  
1.  [Abra la página Aplicación de servicio PowerPivot](#openconfig).  
  
2.  En la sección **Recolección de datos de uso** , en **Intervalo de informes de consulta**, escriba el número de segundos que hay que esperar antes de que el servidor notifique las estadísticas de consulta para todas las categorías (trivial, rápida, esperada, de ejecución prolongada y superada) como un único evento al sistema de recopilación de datos de uso.  
  
    -   El intervalo abarca de 1 a cualquier número entero positivo.  
  
    -   El valor predeterminado es de 300 segundos (o cinco minutos). Este valor se recomienda en entornos de granja dinámicos que ejecutan diversas aplicaciones y servicios.  
  
     Si eleva este valor a un número mucho mayor, podría perder los datos estadísticos antes de que se puedan notificar. Por ejemplo, si se reinicia el servicio, las estadísticas de consulta se perderán. Por el contrario, si los informes de actividad integrados muestran que los datos son insuficientes, considere disminuir el intervalo para obtener eventos para indicar el tiempo para la notificación con más frecuencia.  
  
3.  Haga clic en **Aceptar**.  
  
##  <a name="openconfig"></a> Abra la página de aplicación de servicio PowerPivot en la configuración de acceso  
 Debe ser administrador de un servicio o granja para modificar las configuraciones de las aplicaciones de servicio. Si definió varias aplicaciones de servicio PowerPivot en la granja, debe modificar cada una individualmente.  
  
1.  En Administración central de SharePoint, en **Administración de aplicaciones**, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Encuentre la aplicación de servicio PowerPivot. Puede identificar una aplicación de servicio por su tipo. Un tipo de aplicación de servicio PowerPivot es **Aplicación de servicio PowerPivot**.  
  
3.  Haga clic en el nombre de la aplicación de servicio PowerPivot. Se abrirá el panel de administración de PowerPivot.  
  
4.  En **Acciones**, haga clic en **Configurar las opciones de aplicación de servicio**. Se abrirá la página Configuración de aplicación de servicio PowerPivot.  
  
##  <a name="defaultconfig"></a> La configuración predeterminada para la recopilación de datos de uso de PowerPivot  
 La recopilación de datos de uso para las operaciones de servicio PowerPivot se puede habilitar con la configuración predeterminada para hacer que esté inmediatamente disponible en las aplicaciones que admiten la característica de integración de Analysis Services. La configuración predeterminada incluye eventos que desencadenan la recopilación de datos de uso, limita el tiempo que se almacenan los datos de uso y los umbrales para clasificar los tiempos de respuesta de las consultas.  
  
 En la siguiente tabla se muestran los valores predeterminados para la configuración de la recopilación de datos de uso.  
  
|Parámetro|Valor predeterminado|Tipo|Intervalo válido|  
|-------------|-------------------|----------|-----------------|  
|**Eventos de uso de Analysis Services** (Conexión, Carga, Descarga, Solicitudes)|\<habilitado >|Boolean|Estos valores están habilitados o deshabilitados.|  
|**Query Reporting interval**|300 (en segundos)|Integer|De 1 a cualquier entero positivo. El valor predeterminado es 5 minutos.|  
|**Usage data history**|365 (en días)|Integer|0 especifica ilimitado, pero también puede establecer un límite superior para que los datos históricos expiren y que se eliminen automáticamente. Los valores válidos para un período de retención limitado abarcan de 1 a 5000 (en días).|  
|Límite superior de respuesta trivial|500 (en milisegundos)|Integer|Establece un límite superior que define un intercambio de solicitudes y respuestas trivial. Cualquier solicitud que se complete entre 0 y 500 milisegundos es una solicitud trivial y se omite a los efectos del informe de errores.|  
|Límite superior de respuesta rápida|1000 (en milisegundos)|Integer|Establece un límite superior que define un intercambio de solicitudes y respuestas rápido.|  
|Límite superior de respuesta esperada|3000 (en milisegundos)|Integer|Establece un límite superior que define un intercambio de solicitudes y respuestas esperado.|  
|Límite superior de respuesta larga|10000 (en milisegundos)|Integer|Establece un límite superior que define un intercambio de solicitudes y respuestas de ejecución prolongada. Cualquier solicitud que supere este límite entra dentro de la categoría Superada, que no tiene ningún umbral superior.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de las opciones configuración &#40;PowerPivot para SharePoint&#41;](configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Recopilación de datos de uso de PowerPivot](power-pivot-usage-data-collection.md)  
  
  
