---
title: Informes de conjuntos de recopilación de datos del sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], server activity
- server activity [SQL Server]
- reports [SQL Server], data collection
- reports [SQL Server], disk usage
- collection sets [SQL Server], reports
- data collector [SQL Server], reports
- reports [SQL Server], query statistics
- query statistics reports [SQL Server]
- disk usage reports [SQL Server]
ms.assetid: 0b126b8d-4fe7-443d-8a9a-c266350181e5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 39bd24414e2382557a22469da502bad91abe20b7
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100500"
---
# <a name="system-data-collection-set-reports"></a>Informes de conjuntos de recopilación de datos del sistema
  El recopilador de datos proporciona un informe histórico para cada uno de los conjuntos de recopilación de datos del sistema. Cada uno de los informes siguientes utiliza datos que están almacenados en el almacén de administración de datos:  
  
-   [Resumen de uso de disco](#Disk)  
  
-   [Historial de estadísticas de consultas](#Query)  
  
-   [Historial de actividad del servidor](#Server)  
  
 Puede utilizar estos informes para obtener información con el fin de supervisar la capacidad del sistema y solucionar problemas de rendimiento del sistema.  
  
##  <a name="Disk"></a> Informe Resumen de uso de disco  
 El informe Resumen de uso de disco contiene datos sobre el uso del espacio de disco de todas las bases de datos de la sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los datos que se proporcionan en los informes se obtienen con el conjunto de recopilación Uso de disco, que usa el tipo de recopilador de consultas T-SQL genérico.  
  
 Puede tener acceso al informe Resumen de uso de disco desde el Explorador de objetos. Para ver el informe, expanda la carpeta **Administración** , haga clic con el botón derecho en **Recopilación de datos**, seleccione **Informes**, **Almacén de administración de datos**y, después, haga clic en **Resumen de uso de disco**. Para obtener más información, vea [View a Collection Set Report &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md).  
  
### <a name="disk-usage-collection-set-report"></a>Informe del conjunto de recopilación Uso de disco  
 El informe del conjunto de recopilación Uso de disco proporciona información general del espacio en disco que usan todas las bases de datos de la sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y tendencias de crecimiento de los datos y archivos de registro de cada una de estas bases de datos.  
  
-   En la tabla de resumen se muestran el tamaño inicial (en megabytes) y el tamaño actual de todas las bases de datos instaladas en el servidor que el recopilador de datos supervisa.  
  
-   La información de las tendencias y del promedio de crecimiento se muestra gráfica y numéricamente tanto para los datos como para los archivos de registro.  
  
#### <a name="disk-usage-collection-set---database-databasename-subreport"></a>Subinforme Conjunto de recopilación Uso de disco - Base de datos: <nombre_de_base de datos>  
 El subinforme Conjunto de recopilación de uso de disco - Base de datos: *<nombre_de_base_de_datos>* se muestra al hacer clic en una línea de tendencia para una base de datos o archivo de registro concretos de la tabla de resumen del informe Conjunto de recopilación de uso de disco. Este informe proporciona una representación gráfica de las tendencias de crecimiento en el uso del espacio de disco sobre el período del informe. El uso de disco se organiza y se notifica según el espacio utilizado, el espacio de datos, el espacio sin asignar y el espacio de índice de los archivos de datos, y el espacio usado y el espacio sin usar de los archivos de registro.  
  
 La tabla debajo del gráfico muestra las horas de la recopilación de datos y los datos de uso correspondientes.  
  
#### <a name="disk-usage-for-database-databasename-subreport"></a>Subinforme Uso de disco para la base de datos : <nombre_de_base_de_datos>  
 El subinforme **Uso de disco para la base de datos:**_<nombre_de_base_de_datos>_ se muestra al hacer clic en un nombre de base de datos de la tabla de resumen del informe Conjunto de recopilación de uso de disco. Este informe proporciona un desglose numérico y gráfico del uso de espacio de los archivos del registro de transacciones y de datos. El uso de espacio de los archivos de datos se categoriza como un porcentaje asignado a las páginas de índice, el espacio sin asignar, a los datos y al espacio sin usar. Estas categorías se definen como se indica a continuación:  
  
|Categoría|Definición|  
|--------------|----------------|  
|Índice|Cantidad de espacio en disco utilizada para contener las páginas de índice.|  
|Sin asignar|La cantidad de espacio en disco disponible para la base de datos pero que aún no se ha asignado a ningún objeto.|  
|Datos|La cantidad de espacio en disco utilizada por páginas de datos.|  
|No utilizado|La cantidad de espacio de disco asignado a uno o más objetos, pero que aún no se ha usado.|  
  
 El uso de espacio para el archivo de registro de transacciones se categoriza como espacio usado y como espacio sin usar.  
  
 Los eventos de reducción automática y crecimiento automático se notifican tanto para los archivos de datos como para los archivos de registro si estos eventos se han producido en la base de datos. El informe muestra la hora de inicio y la duración de cada evento, y el cambio resultante en el tamaño de los archivos.  
  
 Se notifica el espacio en disco que usa cada archivo de datos en la base de datos. El espacio notificado como Espacio reservado es la cantidad de espacio utilizado más el espacio asignado al archivo pero que aún no se ha usado. El espacio notificado por Espacio utilizado es el espacio real que usa el archivo, excluyendo el espacio asignado.  
  
##  <a name="Query"></a> Informe Historial de estadísticas de consultas  
 El informe Historial de estadísticas de consultas contiene las estadísticas de ejecución de las consultas. Los datos utilizados en este informe se obtienen con el conjunto de recopilación Estadísticas de consultas, que utiliza el tipo de recopilador Actividad de consultas.  
  
 Puede obtener acceso al informe Historial de estadísticas de consultas mediante el Explorador de objetos. Para ver el informe, expanda la carpeta **Administración** , haga clic con el botón derecho en **Recopilación de datos**, seleccione **Informes**, seleccione **Almacén de administración de datos**y haga clic en **Historial de estadísticas de consultas**. Para obtener más información, vea [Ver un informe de conjunto de recopilación &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md).  
  
### <a name="selecting-data-to-include-in-the-report"></a>Seleccionar los datos para incluir en el informe  
 El informe incluye las estadísticas de ejecución de las consultas durante todo el período de recopilación de datos. Hay dos maneras de navegar a través de la escala de tiempo de la recopilación de datos con el fin de seleccionar un segmento de datos para verlo.  
  
 **Botones de navegación y control de escala de tiempo**  
  
 Utilice el control de escala de tiempo y los botones de navegación para moverse a través de la escala de tiempo o seleccionar un intervalo de fechas. Los botones de dirección permiten el desplazamiento a la izquierda y a la derecha de modo que se pueda mover hacia atrás o hacia delante a través de la escala de tiempo. De forma predeterminada, las flechas se mueven a través de la escala de tiempo en incrementos de cuatro horas. Mediante los botones del Ampliador, puede expandir o contraer este incremento de tiempo a uno de los siguientes valores: 15 minutos, 1 hora, 4 horas, 12 horas o 24 horas. El intervalo temporal actualmente seleccionado se indica con la parte resaltada de la escala de tiempo y se muestra en el texto debajo de la escala de tiempo. Estos valores, así como los datos del informe, se actualizan cada vez que se hace clic en la escala de tiempo o se utilizan los botones de navegación.  
  
 **Botón de calendario**  
  
 Utilice el botón de calendario para especificar la fecha de inicio, la hora de inicio y la duración de los datos que desea notificar.  
  
#### <a name="query-statistics-history-report"></a>Informe Historial de estadísticas de consultas  
 El gráfico Principales consultas por total de CPU muestra el gasto relativo de cada consulta para el intervalo de tiempo seleccionado según el uso total de CPU. Para mostrar una vista diferente del gasto relativo de la consulta, haga clic en uno de los hipervínculos que se proporcionan debajo del gráfico: **Duración**, **Total E/S**, **lecturas físicas**, o **escrituras lógicas**.  
  
 La tabla situada debajo del gráfico proporciona datos de consulta adicionales. Muestra el texto de cada consulta que se representa mediante un gráfico junto con información estadística detallada. Observe que las barras del gráfico son vínculos activos, como lo son cada una de las consultas que se muestran en la tabla. Al hacer clic en un vínculo activo, se abre el subinforme Detalles de consulta correspondiente a la consulta.  
  
#### <a name="query-details-subreport"></a>Subinforme Detalles de consulta  
 El subinforme Detalles de consulta proporciona todo el texto de la consulta. Al lado de la consulta se encuentra el hipervínculo **Editar texto de consulta** . Puede hacer clic en este vínculo para abrir la consulta en el Editor de consultas. La tabla situada debajo de la consulta proporciona estadísticas de ejecución de la consulta, como el promedio de duración por cada ejecución de una consulta.  
  
 Se muestra un gráfico de los planes de consulta y el promedio de duración por cada ejecución. Para mostrar una vista diferente del costo relativo de la consulta del plan, haga clic en uno de los hipervínculos que se muestran debajo del gráfico: **Duración**, **lecturas físicas**, o **escrituras lógicas**. La línea del gráfico es un elemento activo y puede hacer clic en cualquier punto para abrir el subinforme Detalles del plan de consulta.  
  
 La tabla situada debajo del gráfico muestra los diez primeros planes de consulta según el uso de CPU por ejecución. Cada número de la columna **Nº de planes** es un vínculo activo en el que se puede hacer clic para abrir el subinforme Detalles del plan de consulta.  
  
#### <a name="query-plan-details-subreport"></a>Subinforme Detalles del plan de consulta  
 Este informe muestra la información de un plan de consulta. Además de permitir modificar la consulta y ver las estadísticas de ejecución, el informe proporciona información detallada sobre el plan de consulta. El hipervínculo **Ver plan gráfico de ejecución de consulta** abre una representación gráfica del plan de ejecución para la consulta actual.  
  
## <a name="server-activity-history-report"></a>Informe Historial de actividad del servidor  
 El informe Historial de actividad del servidor contiene datos del consumo de recursos y de la actividad del servidor correspondientes al servidor y a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El conjunto de recopilación Actividad del servidor recopila los datos que se proporcionan en este informe y usa el tipo de recopilador de consultas T-SQL genérico y el tipo de recopilador Contadores de rendimiento.  
  
 Puede obtener acceso al informe Historial de actividad del servidor desde el Explorador de objetos. Para ver el informe, expanda la carpeta **Administración** , haga clic con el botón derecho en **Recopilación de datos**, seleccione **Informes**y **Almacén de administración de datos**y, después, haga clic en **Historial de actividad del servidor**. Para obtener más información, vea [Ver un informe de conjunto de recopilación &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md).  
  
### <a name="selecting-data-to-include-in-the-report"></a>Seleccionar los datos para incluir en el informe  
 El informe incluye la actividad del servidor correspondiente al período de recopilación de datos completo. Hay dos maneras de navegar a través de la escala de tiempo de la recopilación de datos con el fin de seleccionar un segmento de datos para verlo.  
  
 **Botones de navegación y control de escala de tiempo**  
  
 Utilice el control de escala de tiempo y los botones de navegación para moverse a través de la escala de tiempo o seleccionar un intervalo de fechas. Los botones de dirección permiten el desplazamiento a la izquierda y a la derecha de modo que se pueda mover hacia atrás o hacia delante a través de la escala de tiempo. De forma predeterminada, las flechas se mueven a través de la escala de tiempo en incrementos de cuatro horas. Mediante los botones del Ampliador, puede expandir o contraer este incremento de tiempo a uno de los siguientes valores: 15 minutos, 1 hora, 4 horas, 12 horas o 24 horas. El intervalo temporal actualmente seleccionado se indica con la parte resaltada de la escala de tiempo y se muestra en el texto debajo de la escala de tiempo. Estos valores, así como los datos del informe, se actualizan cada vez que se hace clic en la escala de tiempo o se utilizan los botones de navegación.  
  
 **Botón de calendario**  
  
 Utilice el botón de calendario para especificar la fecha de inicio, la hora de inicio y la duración de los datos que desea notificar.  
  
###  <a name="Server"></a> Informe Historial de actividad del servidor  
 El informe Historial de actividad del servidor muestra la vista inicial de la actividad del servidor para una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el sistema operativo host.  
  
 En la tabla siguiente se describen los gráficos que trazan la actividad del sistema y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el informe, y los subinformes detallados a los que se puede tener acceso a través de los gráficos.  
  
|Gráfico|Descripción del informe|  
|-----------|------------------------|  
|%CPU|Se tiene acceso a estos subinformes haciendo clic en cualquier punto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o en las líneas del gráfico Sistema del gráfico %CPU.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /> El informe Historial de estadísticas de consultas proporciona un gráfico de las consultas más caras en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una tabla debajo del gráfico muestra las consultas e incluye datos estadísticos para cada una. Puede hacer clic en una consulta para obtener detalles adicionales.<br /><br /> Sistema<br /> El informe Uso de CPU del sistema proporciona un gráfico del porcentaje de tiempo de CPU por procesador y datos estadísticos de cada proceso en formato tabular.|  
|Utilización de la memoria|Para consultar estos subinformes, haga clic en cualquier punto de las líneas del gráfico Sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el gráfico Utilización de la memoria.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /> El informe Utilización de la memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona gráficos para el uso de memoria de procesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , contadores de memoria, consumo de memoria interna por tipo y una tabla que ofrece datos sobre el promedio de utilización de la memoria por cada tipo de componente.<br /><br /> Sistema<br /> El informe Uso de memoria del sistema proporciona gráficos para la utilización de memoria y las frecuencias de aciertos de páginas y memoria caché, y una tabla que ofrece información sobre los bytes privados y el espacio de trabajo de cada proceso.|  
|Uso de E/S de disco|Para consultar estos subinformes, haga clic en cualquier punto de las líneas del gráfico Sistema o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el gráfico Uso de E/S de disco.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /> El informe Uso de E/S de disco de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona gráficos del tiempo de respuesta del disco y de la tasa de la transferencia de disco. En una tabla adicional se proporcionan estadísticas de los archivos virtuales por cada disco, base de datos y archivo.<br /><br /> Sistema<br /> El informe Uso de disco del sistema proporciona gráficos para el tiempo de respuesta del disco, el promedio de longitud de la cola de disco y la velocidad de transferencia de disco, y una tabla con información sobre las escrituras y lecturas de E/S de cada proceso.|  
|Uso de red|No hay ningún informe adicional disponible.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Esperas|El gráfico Esperas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra las esperas que encontraron los subprocesos que se ejecutan por cada categoría de espera. Puede tener acceso a un informe detallado haciendo clic en cualquier segmento del gráfico. Además de ofrecer estadísticas gráficas de las esperas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de un intervalo de tiempo más reducido, este informe proporciona información sobre las categorías de las esperas en formato tabular. Para cada categoría, como CPU y sus subcategorías, la tabla muestra el número de esperas, el tiempo de espera y el porcentaje de tiempo de espera total.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Actividad|Desde el gráfico Actividad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede tener acceso a diferentes aspectos de la actividad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los informes que puede obtener haciendo clic en un punto de la línea del gráfico Compilaciones SQL/s son los siguientes:<br /><br /> Conexiones y sesiones<br /><br /> Solicitudes<br /><br /> Frecuencia de aciertos de caché de plan<br /><br /> Características de TempDb|  
  
## <a name="see-also"></a>Vea también  
 [Recopilación de datos](data-collection.md)   
 [Ver un informe de conjunto de recopilación &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)  
  
  
