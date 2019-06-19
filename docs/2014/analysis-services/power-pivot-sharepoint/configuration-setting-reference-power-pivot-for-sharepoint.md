---
title: Configuración de la configuración de referencia (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 3b57dd3f-7820-4ba8-b233-01dc68908273
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 45ef593e13643ac38184f8b88cbe4cdf38f0126c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071888"
---
# <a name="configuration-setting-reference-powerpivot-for-sharepoint"></a>Referencia de las opciones de configuración (PowerPivot para SharePoint)
  En este tema se proporciona documentación de referencia para la configuración que utilizan las aplicaciones de servicio PowerPivot en una granja de servidores de SharePoint. Si está utilizando un script de PowerShell para configurar un servidor, o si desea buscar información de un valor concreto, la información de este tema proporciona descripciones detalladas.  
  
 Los valores de configuración se establecen para cada aplicación de servicio PowerPivot. Dentro de una granja de servidores, puede crear varias aplicaciones de servicios como medio de configurar instancias lógicas independientes de la misma instancia de servicio física. La configuración se almacena en la base de datos de aplicación de PowerPivot que se crea para cada aplicación de servicio que configure.  
  
 Si cambia la configuración, los cambios se recogen inmediatamente y se utilizan para las solicitudes y conexiones subsiguientes. Las operaciones en curso son gobernadas por la configuración que estuviera en vigor al comenzar dichas operaciones.  
  
 Haga clic en los siguientes vínculos para obtener más información acerca de áreas de configuración concretas:  
  
 [Tiempo de espera de carga de datos](#LoadingData)  
  
 [Grupos de conexiones](#ConnectionPool)  
  
 [Equilibrio de carga](#AllocationScheme)  
  
 [Actualización de datos](#DataRefresh)  
  
 [Recopilación de datos de uso](#UsageData)  
  
 Para obtener instrucciones sobre cómo crear una aplicación de servicio PowerPivot, vea [crear y configurar una aplicación de servicio PowerPivot en Administración Central](create-and-configure-power-pivot-service-application-in-ca.md).  
  
##  <a name="LoadingData"></a> Tiempo de espera de carga de datos  
 Las instancias de servidor de Analysis Services de la granja recuperan y cargan los datos PowerPivot. En función de cómo y cuándo se tuviera acceso a los datos en último lugar, estos se cargarán bien de una biblioteca de contenido o bien de una memoria caché de archivos local. Los datos se cargan en la memoria cada vez que se recibe una solicitud de procesamiento o consulta. Para lograr la máxima disponibilidad global del servidor, puede establecer un valor de tiempo de espera que indique al servidor que detenga una solicitud de datos de carga si no se puede completar dentro del tiempo asignado.  
  
|NOMBRE|Default|Valores válidos|Descripción|  
|----------|-------------|------------------|-----------------|  
|Tiempo de espera de carga de datos|1800 (en segundos)|1 a 3600|Especifica la cantidad de tiempo que una aplicación de servicio PowerPivot esperará una respuesta de una instancia de servidor de Analysis Services concreta.<br /><br /> De forma predeterminada, la aplicación de servicio esperará 30 minutos a una carga de datos de la instancia de servicio del motor a la que reenvió una solicitud concreta.<br /><br /> Si el origen de datos PowerPivot no se puede cargar dentro de este período de tiempo, el subproceso se detendrá y se iniciará uno nuevo.|  
  
##  <a name="ConnectionPool"></a> Grupos de conexiones  
 La aplicación de servicio PowerPivot crea y administra los grupos de conexiones para habilitar la reutilización de conexiones. Hay dos tipos de grupos de conexiones: uno para las conexiones de datos a datos de solo lectura y otra para las conexiones al servidor.  
  
 Los grupos de conexiones de datos contienen conexiones almacenadas en memoria caché para el origen de datos PowerPivot. Cada grupo de conexiones está basado en el contexto que estaba establecido cuando se cargó la base de datos. Este contexto incluye la identidad de la instancia de servicio física, el identificador de la base de datos y la identidad del usuario de SharePoint que solicita los datos. Se crea un grupo de conexiones independiente para cada combinación. Por ejemplo, las solicitudes de usuarios diferentes de la misma base de datos que se ejecuten en el mismo servidor utilizarán conexiones de grupos distintos.  
  
 El propósito de un grupo de conexiones es utilizar las conexiones almacenadas en memoria caché para las solicitudes de solo lectura de la misma base de datos de Analysis Services y el mismo usuario de SharePoint. La instancia de servicio PowerPivot es el servidor que tiene los datos cargados en memoria. El identificador de la base de datos es un identificador interno para las estructuras de datos en memoria del modelo de datos (una instancia de un modelo se crea como una base de datos de cubo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ). La información de versión se incorpora implícitamente en el identificador.  
  
 Los grupos de conexiones de servidor contienen las conexiones almacenadas en memoria caché de una instancia de la aplicación de servicio PowerPivot a una instancia de servidor de Analysis Services, donde la aplicación de servicio se conecta con permisos de administrador del sistema de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el servidor de Analysis Services. Estas conexiones se utilizan para emitir una solicitud de carga de base de datos y supervisar el estado del sistema.  
  
 Cada tipo de grupo de conexiones tiene límites superiores que puede establecer para asegurarse de que el uso de memoria del sistema es el más conveniente para la administración de las conexiones.  
  
|Name|Default|Valores válidos|Descripción|  
|----------|-------------|------------------|-----------------|  
|Tiempo de espera de grupo de conexiones|1800 (en segundos)|1 a 3600.|Este valor se aplica a los grupos de conexiones de datos.<br /><br /> Especifica cuánto tiempo puede permanecer inactiva una conexión en un grupo de conexiones antes de quitarse.<br /><br /> De forma predeterminada, la aplicación de servicio quitará una conexión si está inactiva durante más de cinco minutos.|  
|Tamaño máximo de grupo de conexiones de usuario|1000|-1, 0, o de 1 a 10000.<br /><br /> -1 especifica un número ilimitado de conexiones inactivas.<br /><br /> 0 significa que no se mantiene ninguna conexión inactiva. Las conexiones nuevas a un origen de datos PowerPivot se deben crear cada vez.|Este valor se aplica al número de conexiones inactivas en todos los conjuntos de conexiones de datos creados para una instancia de la aplicación de servicio PowerPivot concreta.<br /><br /> Se crean grupos de conexiones individuales para combinaciones únicas de un usuario de SharePoint, datos PowerPivot e instancia de servicio. Si tiene muchos usuarios que tienen acceso a orígenes de datos PowerPivot diversos, el rendimiento del servidor podría beneficiarse de un aumento del tamaño del grupo de conexiones.<br /><br /> Si hay más de 100 conexiones inactivas a una instancia de servicio PowerPivot, las conexiones que han pasado a estar inactivas recientemente se desconectan en lugar de devolverse al grupo.|  
|Tamaño máximo de grupo de conexiones de administración|200|-1, 0, o de 1 a 10000.<br /><br /> -1 especifica un número ilimitado de conexiones inactivas.|El número máximo de conexiones al servidor inactivas en todos los grupos de conexiones administrativos creados para las conexiones de aplicación de servicio PowerPivot a una instancia del servidor de Análisis Servicios. Las conexiones de servidor se utilizan en las solicitudes para cargar bases de datos y guardar los cambios de nuevo en la base de datos SharePoint.|  
  
##  <a name="AllocationScheme"></a> Equilibrio de carga  
 Una de las funciones que el servicio PowerPivot realiza es determinar dónde se cargarán los datos de Analysis Services entre las instancias de servicio PowerPivot disponibles. El valor `AllocationMethod` especifica los criterios con los que se selecciona una instancia de servicio.  
  
|Name|Default|Valores válidos|Descripción|  
|----------|-------------|------------------|-----------------|  
|Método de asignación|RoundRobin|Round Robin<br /><br /> Basado en estado|Esquema para asignar las solicitudes de carga entre dos o más instancias de servidor de Analysis Services.<br /><br /> De forma predeterminada, el servicio PowerPivot alternará las solicitudes basadas en el estado del servidor. Si se basa en el estado, las solicitudes se asignan al servidor que tiene el mayor número de recursos del sistema disponibles en función de la memoria disponible y la utilización de la CPU.<br /><br /> La operación por turnos rota las solicitudes entre los servidores disponibles en orden secuencial, independientemente del estado actual de la carga o del servidor.|  
  
##  <a name="DataRefresh"></a> Actualización de datos  
 Especifique el intervalo de horas que define un día laboral normal o típico en una organización. Esta configuración determina cuándo se produce el procesamiento de datos después del horario comercial en las operaciones de actualización de datos. El procesamiento después del horario comercial puede comenzar a la hora en que finaliza la jornada laboral. El procesamiento después del horario comercial es una opción de programación para los propietarios de documentos que desean actualizar un origen de datos PowerPivot con datos de transacciones que se generaron durante los horarios laborales normales.  
  
|Name|Default|Valores válidos|Descripción|  
|----------|-------------|------------------|-----------------|  
|Hora de inicio|04:00 a. m.|1 a 12 horas, donde el valor es un entero válido dentro de ese intervalo.<br /><br /> El tipo es Time.|Establece el límite inferior de un intervalo del horario laboral.|  
|Hora de finalización|08:00 p. m.|1 a 12 horas, donde el valor es un entero válido dentro de ese intervalo.<br /><br /> El tipo es Time.|Establece el límite superior de un intervalo del horario laboral.|  
|Cuenta de actualización de datos desatendida de PowerPivot|None|Identificador de una aplicación de destino|Esta cuenta se utiliza para ejecutar los trabajos de actualización de datos en nombre del propietario de una programación.<br /><br /> Se debe definir de antemano la cuenta de actualización de datos desatendida para poder hacer referencia a ella en la página de configuración de la aplicación del servicio. Para obtener más información, consulte [configurar la cuenta de actualización de datos desatendida de PowerPivot &#40;PowerPivot para SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md).|  
|Permitirles a los usuarios especificar credenciales de Windows personalizadas|Enabled|Boolean|Determina si la página de configuración de la actualización de datos programada muestra una opción que permita al propietario de una programación especificar una cuenta de usuario de Windows y una contraseña para ejecutar un trabajo de actualización de datos.<br /><br /> El Servicio de almacenamiento seguro debe estar habilitado para que esta opción funcione. Para obtener más información, consulte [configurar las credenciales almacenadas para la actualización de datos PowerPivot &#40;PowerPivot para SharePoint&#41;](../configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).|  
|Longitud máxima de historial de procesamiento|365|1 a 5000 días|Determina cuánto tiempo se conserva el historial de actualización de datos en la base de datos de aplicación de servicio PowerPivot. Para obtener más información, consulte [PowerPivot Usage Data Collection](power-pivot-usage-data-collection.md).|  
  
##  <a name="UsageData"></a> Recopilación de datos de uso  
 Los informes de uso que aparecen en el Panel de administración de PowerPivot pueden proporcionar información importante acerca de cómo se utilizan los libros habilitados para PowerPivot. Los siguientes valores de configuración controlan los aspectos de la recopilación de datos de uso para los eventos de servidor de PowerPivot que se presentan después en los informes de actividad o de uso.  
  
|NOMBRE|Default|Valores válidos|Descripción|  
|----------|-------------|------------------|-----------------|  
|Intervalo de informes de consulta|300 (en segundos)|1 a n segundos, donde n es un número entero válido.|Para asegurarse de que la recopilación de datos de uso no consume un exceso de la capacidad de transferencia de datos de la granja, se recopilan estadísticas de consulta en cada conexión y se notifican como un único evento. El intervalo de informes de consulta determina con qué frecuencia se notifica un evento. De forma predeterminada, las estadísticas de consulta se notifican cada cinco minutos.<br /><br /> Dado que las conexiones se cierran de inmediato en cuanto se envía una solicitud, el sistema genera un número muy grande de conexiones para incluso un único usuario que tenga acceso a un único origen de datos PowerPivot. Por esta razón, se crean grupos de conexiones para cada combinación de usuario y origen de datos PowerPivot, de modo que una vez creada una conexión, el mismo usuario pueda reutilizarla para los mismos datos. Periódicamente, en los intervalos especificados a través de esta opción de configuración, la aplicación de servicio PowerPivot notifica los datos de uso de cada conexión del grupo de conexiones.<br /><br /> Al aumentar el valor de tiempo de notificación, se registrarán menos eventos. Sin embargo, si se establece en un valor demasiado alto, se arriesga a perder los datos de los eventos si el servidor se reinicia o se cierra una conexión.<br /><br /> Al bajar el valor, se registrarán más eventos con una mayor frecuencia, lo que supone agregar más datos de uso relacionados con PowerPivot al sistema de recopilación de datos de la base de datos de uso de SharePoint.<br /><br /> Generalmente, no cambie esta opción de configuración a menos que esté intentando resolver un problema concreto (por ejemplo, si la base de datos de uso está creciendo demasiado rápidamente como resultado de los datos de uso de PowerPivot).|  
|Historial de datos de uso|365 (en días)|0, ó 1 a n días, donde n es un número entero válido.<br /><br /> 0 significa que el historial siempre se retiene y no se elimina nunca.|De forma predeterminada, los datos de uso se mantienen durante un año en la base de datos de aplicación de servicio PowerPivot. Los registros anteriores a un año se quitan de la base de datos.<br /><br /> Diariamente se comprueba si los datos históricos han expirado, cuando se ejecuta el trabajo de procesamiento de datos de uso de Microsoft SharePoint Foundation. El trabajo de temporizador leerá este valor y desencadenará un comando de eliminación de datos para el historial expirado en la base de datos de aplicación de servicio PowerPivot.|  
|Límite superior de respuesta trivial|500 (en milisegundos)|1 a n milisegundos, donde n es un número entero válido.|De forma predeterminada, el umbral para las solicitudes triviales es la mitad un segundo.<br /><br /> Entre las solicitudes triviales se incluyen los ping de servidor, las solicitudes de metadatos y el inicio de sesiones.|  
|Límite superior de respuesta rápida|1000 (en milisegundos)|1 a n milisegundos, donde n es un número entero válido.|De forma predeterminada, el umbral para las solicitudes rápidas es un segundo.<br /><br /> Las solicitudes rápidas son aquellas que tienen un conjunto de datos sumamente pequeño o las solicitudes de metadatos que abarcan conjuntos de miembros grandes.|  
|Límite superior de respuesta esperada|3000 (en milisegundos)|1 a n milisegundos, donde n es un número entero válido.|De forma predeterminada, el umbral para las solicitudes esperadas es de tres segundos.<br /><br /> Este umbral establece el límite superior de un tiempo de consulta esperado.|  
|Límite superior de respuesta larga|10000 (en milisegundos)|1 a n milisegundos, donde n es un número entero válido.|De forma predeterminada, el umbral para las solicitudes largas es de diez segundos.<br /><br /> Se trata de solicitudes que se ejecutan mucho más tiempo de lo esperado, pero que siguen perteneciendo a un intervalo aceptable.|  
  
## <a name="see-also"></a>Vea también  
 [Crear y configurar una aplicación de servicio PowerPivot en Administración Central](create-and-configure-power-pivot-service-application-in-ca.md)   
 [Actualización de datos PowerPivot con SharePoint 2010](../powerpivot-data-refresh-with-sharepoint-2010.md)   
 [Configurar la recopilación de datos de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [Configurar cuentas de servicio PowerPivot](configure-power-pivot-service-accounts.md)   
 [Panel de administración de PowerPivot y datos de uso](power-pivot-management-dashboard-and-usage-data.md)  
  
  
