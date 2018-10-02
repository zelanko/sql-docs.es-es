---
title: Explorador de Utilidad (Ayuda F1) | Microsoft Docs
ms.custom: ''
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
f1_keywords:
- sql13.swb.ue.navigation.f1
- sql13.SWB.UE.dac.details.F1
- sql13.SQB.UE.dac.details.F1
- utility details
helpviewer_keywords:
- Utility
- management
- data-tier application
ms.assetid: 8697e4a4-4f59-4cda-af71-7de86005bd4a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2bd5d38c0541a6e56b73cf5da321844eaa94fd5b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47702553"
---
# <a name="utility-explorer-f1-help"></a>Explorador de Utilidad (Ayuda F1)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En las secciones siguientes se documentan la funcionalidad de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y sus operaciones asociadas.  
  
  ## <a name="utility-dashboard-sql-server-utility"></a>Panel de la utilidad (utilidad de SQL Server)
 Para ver los datos en el panel de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione el nodo superior en el árbol del explorador de la utilidad (identificado como "Utilidad<UCP_Name>\\(nombreDeEquipo\UCP)"). El panel incluye un resumen y datos detallados de todas las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de todas las aplicaciones de capa de datos en la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para actualizar los datos en el panel, haga clic con el botón derecho en el nodo superior del árbol del explorador de la utilidad y seleccione **Actualizar**.  
  
 Para obtener más información sobre cómo crear un punto de control de la utilidad, vea [Crear un punto de control de la Utilidad de SQL Server &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md). Para obtener más información sobre cómo agregar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la Utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Inscribir una instancia de SQL Server &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md).  
 
  
### <a name="uielement-list"></a>Lista de UIElement  
 Estado de mantenimiento de la instancia administrada  
 El estado de mantenimiento de las instancias administrados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se muestra en a la izquierda del panel de contenido del explorador de la utilidad.  
  
 Los parámetros del estado de la instancia administrada son como sigue:  
  
-   Utilización de la CPU para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Utilización de archivos de base de datos.  
  
-   Utilización del espacio de volumen de almacenamiento.  
  
-   Utilización de la CPU para el sistema informático.  
  
-   El estado de cada parámetro se divide en tres categorías:  
  
-   Utilizado apropiadamente: número de instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no están infringiendo las directivas de utilización de recursos.  
  
-   Infrautilizado: número de recursos administrados que están infringiendo las directivas de infrautilización de recursos.  
  
-   Sobreutilizado: número de recursos administrados que están infringiendo las directivas de sobreutilización de recursos.  
  
-   No hay datos disponibles: no hay datos disponibles para las instancias administradas de SQL Server porque su instancia acaba de inscribirse y no se ha completado la primera operación de recopilación de datos, o bien porque hay un problema con la instancia administrada de SQL Server con respecto a la recopilación y carga de datos en el UCP.  
  
 El estado detallado de cada parámetro de estado se muestra en indicadores deslizantes. La zona a la derecha de los indicadores deslizantes muestra el número de instancias administradas que se encuentran en cada categoría de estado.  
  
 Para crear una vista filtrada de una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o una aplicación de nivel de datos, haga clic en el vínculo de una categoría de utilización al lado de su indicador deslizante en el panel de la utilidad. Por ejemplo, si hace clic en **CPU de instancia sobreutilizada** en el panel **Contenido del explorador de la utilidad** , SSMS crea una vista de lista filtrada de instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuya CPU está sobreutilizada en función de los valores de directiva actuales.  
  
 Observe que, al hacer clic en un vínculo de una categoría de utilización, se agrega **(filtrado)** al nodo correspondiente en el panel de navegación del explorador de la utilidad; es decir, **Instancias administradas** se etiqueta **Instancias administradas (filtrado)**. Para ver la configuración del filtro, haga clic con el botón derecho en el nodo en el panel de navegación y seleccione **Filtro**y, después, haga clic en **Configuración del filtro**. Para borrar la configuración del filtro, haga clic con el botón derecho en el nodo en el panel de navegación, seleccione **Filtro** y, después, haga clic en **Quitar filtro**.  
  
 Para obtener más información sobre cómo ver el estado de mantenimiento de instancias individuales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o para ver o cambiar la configuración de la directiva, vea [Detalles de las instancias administradas &#40;Utilidad de SQL Server&#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2).  
  
 Resumen de la utilidad  
 Muestra el número de instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el número de aplicaciones de capa de datos que administra la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Estado de las aplicaciones de capa de datos  
 El estado de mantenimiento de las aplicaciones de capa de datos se muestra en la parte derecha del panel de contenido del explorador de la utilidad.  
  
 Los parámetros de estado de las aplicaciones de capa de datos son como sigue:  
  
-   Utilización de la CPU para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Utilización de archivos de base de datos.  
  
-   Utilización del espacio de volumen de almacenamiento.  
  
-   Utilización de la CPU para el sistema informático.  
  
 El estado de cada parámetro se divide en tres categorías:  
  
-   Utilizado apropiadamente: número de aplicaciones de capa de datos que no están infringiendo las directivas de utilización de recursos.  
  
-   Sobreutilizado: número de aplicaciones de capa de datos que están infringiendo las directivas de sobreutilización de recursos.  
  
-   Infrautilizado: número de aplicaciones de capa de datos que están infringiendo las directivas de infrautilización de recursos.  
  
-   No hay datos disponibles: no hay datos disponibles para las aplicaciones de capa de datos porque la instancia administrada de SQL Server que contiene la aplicación de capa de datos no está efectuando la notificación de datos.  
  
 El estado detallado de cada parámetro de estado se muestra en indicadores deslizantes. La zona a la derecha de los indicadores deslizantes muestra el número de aplicaciones de capa de datos que se encuentran en cada categoría de estado. Para obtener más información sobre cómo ver el estado de mantenimiento de aplicaciones de capa de datos individuales o para ver o cambiar la configuración de la directiva, vea [Detalles de la aplicación de capa de datos implementada &#40;Utilidad de SQL Server&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
 Historial de la utilización del almacenamiento de la utilidad  
 El historial de utilización se muestra en un gráfico cronológico en la parte inferior del panel de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Observe que los datos sobre el momento muestran la fecha y hora locales del UCP mediante el tipo de datos datetime. Para más información, consulte el tema [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) . Al utilizar el modelo de objetos de la utilidad, observe que SSMS utiliza el tipo de datos datetimeoffset. Para más información, consulte el tema [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Utilice los botones de radio a la izquierda del área de presentación para cambiar los periodos de notificación del gráfico.  
  
 Las opciones de intervalo de notificación son:  
  
-   1 día; se muestra en intervalos de 15 minutos.  
  
-   1 semana; se muestra en intervalos de 1 día.  
  
-   1 mes; se muestra en intervalos de 1 semana.  
  
-   1 año; se muestra en intervalos de 1 mes.  
  
 Después de modificar el intervalo de notificación, los datos se actualizan automáticamente.  
  
 Utilización del almacenamiento de la utilidad  
 En la parte inferior derecha del panel, el gráfico circular sobre la utilización de almacenamiento muestra la proporción de espacio utilizado en comparación con el espacio disponible en los volúmenes de los equipos que contienen instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los datos de esta presentación se actualizan cada 15 minutos.  
 
 ## <a name="deployed-data-tier-application-details-sql-server-utility"></a>Detalles de la aplicación de capa de datos implementada (Utilidad de SQL Server)
  La información en la vista de aplicaciones de capa de datos implementadas del explorador de Utilidad facilita datos de utilización para las aplicaciones de capa de datos individuales, el historial de la utilización de la CPU, los detalles de la utilización del almacenamiento de nivel de archivo, y la capacidad para ver y actualizar los umbrales de directivas. Los umbrales de directivas se pueden supervisar en el nivel de la aplicación de capa de datos para la utilización de la CPU y para los archivos de datos y de registro de la base de datos. También puede ver los detalles de propiedades para las aplicaciones de capa de datos individuales.  
  
### <a name="uielement-list"></a>Lista de UIElement  
 Vista de lista  
 La vista de lista en el panel superior muestra los datos sobre las aplicaciones de capa de datos individuales. Los iconos de estado de mantenimiento proporcionan un resumen del estado para cada aplicación de capa de datos por categoría de utilización:  
  
-   Marca de verificación verde - ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") - Número de aplicaciones de capa de datos que no están infringiendo las directivas de uso de recursos. Los recursos se utilizan apropiadamente.  
  
-   Flecha verde hacia abajo - ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") - Los recursos están infrautilizados.  
  
-   Flecha roja hacia arriba - ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_up_arrow") - Los recursos están sobreutilizados.  
  
 La secuencia de columnas en la vista de lista se puede cambiar, para ello arrastre las columnas hacia la izquierda o la derecha. En la vista de lista, se pueden agregar o eliminar columnas, para ello haga clic en los encabezados de columna y seleccione columnas o anule su selección. El menú contextual también proporciona opciones de ordenación. La capacidad de ordenación también se puede activar si hace clic en la parte superior del nombre de una columna.  
  
 Para tener acceso a las opciones de filtro para la vista de lista de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic con el botón derecho en el nodo **Aplicaciones de capa de datos implementadas** en el panel de navegación del Explorador de Utilidad y seleccione **Filtro**. Una vez implementada la configuración del filtro, el nodo **Aplicaciones de capa de datos implementadas** en el Explorador de Utilidad se etiquetará con **Aplicaciones de capa de datos implementadas (filtradas)**. Para más información, consulte [Configuración del filtro &#40;Explorador de objetos y Explorador de Utilidad&#41;](http://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2).  
  
 De forma predeterminada, las siguientes columnas muestran información sobre el estado de mantenimiento de cada aplicación de capa de datos.  
  
-   Nombre: el nombre de la aplicación de capa de datos.  
  
-   CPU de la aplicación: muestra el estado de mantenimiento de la utilización del procesador para esta aplicación de capa de datos. El estado de mantenimiento para este parámetro se determina según la directiva de utilización de CPU establecida para la aplicación de capa de datos y la opción de configuración para la directiva de evaluación de recursos volátiles. Para obtener más información, vea [Reducir el ruido en las directivas de uso de la CPU &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para ver el historial de utilización del procesador para esta aplicación de capa de datos o para ver o cambiar los límites de la directiva, haga clic en la pestaña **Uso de CPU**.  
  
-   CPU del sistema informático: muestra el estado de mantenimiento de la utilización del procesador del sistema informático. El estado de mantenimiento para este parámetro se determina según la directiva de utilización de la CPU establecida para el sistema informático y la opción de configuración para la directiva de evaluación de recursos volátiles. Para obtener más información, vea [Reducir el ruido en las directivas de uso de la CPU &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para ver el historial de utilización del procesador para esta aplicación de capa de datos o para ver o cambiar los límites de la directiva, haga clic en la pestaña **Uso de CPU**.  
  
-   Espacio de archivo: muestra un resumen de los estados de mantenimiento de la utilización del espacio de archivo para cada aplicación de capa de datos.  
  
    -   Marca de comprobación verde: los estados de mantenimiento para todos los grupos de archivos y el grupo de archivos de registro son sobreutilizado o infrautilizado.  
  
    -   Flecha verde hacia abajo: el estado de mantenimiento para al menos un grupo de archivos o para el grupo de archivos de registro es infrautilizado, no hay grupos de archivos ni un grupo de archivos de registro que estén sobreutilizados.  
  
    -   Flecha roja hacia arriba: el estado de mantenimiento para al menos un grupo de archivos o el grupo de archivos de registro es sobreutilizado. Tenga en cuenta que si una base de datos se encuentra en estado de “emergencia”, el estado de mantenimiento mostrará el espacio de archivo de registro excesivo sobreutilizado.  
  
     Para ver o cambiar los límites de la directiva de espacio de archivo, haga clic en la pestaña **Uso del almacenamiento** .  
  
-   Espacio de volumen: muestra un resumen de los estados de mantenimiento de la utilización del espacio de volumen para todos los volúmenes que contienen bases de datos que pertenecen a la aplicación de capa de datos seleccionada. Si el estado de mantenimiento de cualquier volumen está sobreutilizado, el estado de mantenimiento del espacio de volumen se notificará como sobreutilizado en la vista de lista. Si el estado de mantenimiento de cualquier volumen está infrautilizado y no hay volúmenes que estén sobreutilizados, el estado de mantenimiento del espacio de volumen se notificará como infrautilizado en la vista de lista. De lo contrario, el estado de mantenimiento del espacio de volumen se notificará como utilizado apropiadamente en la vista de lista. Para ver o cambiar los límites de la directiva, haga clic en la pestaña **Uso del almacenamiento** .  
  
-   Tipo de directiva: indica si las directivas predeterminadas globales y directivas personalizadas invalidadas están habilitadas para la aplicación de capa de datos.  
  
-   Nombre de instancia: muestra el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda las aplicaciones de capa de datos.  
  
 Otras de las columnas que se pueden mostrar con el menú contextual en la zona del encabezado de la columna de vista de lista:  
  
-   Nombre de la base de datos  
  
-   Fecha de implementación  
  
-   De confianza: (True o False)  
  
-   Intercalación  
  
-   Nivel de compatibilidad: (por ejemplo, Versión100)  
  
-   Cifrado habilitado: (True o False)  
  
-   Modelo de recuperación: (simple, completo u optimizado para cargas masivas)  
  
-   Último momento notificado: esta columna muestra la fecha y hora local del UCP mediante el tipo de datos datetime. Para más información, consulte el tema [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) . Al utilizar el modelo de objetos de la utilidad, observe que SSMS utiliza el tipo de datos datetimeoffset. Para más información, consulte el tema [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Pestaña Uso de la CPU  
 La pestaña Uso de la CPU muestra gráficos en paralelo de datos históricos para la aplicación de capa de datos y la utilización de la CPU del sistema informático.  
  
 El gráfico muestra el historial de utilización del procesador para el intervalo especificado en los botones de radio a la derecha de la zona de visualización. Para cambiar el intervalo de presentación y actualizar el conjunto de datos, seleccione un botón de radio en la lista.  
  
 Las opciones de intervalo son las siguientes:  
  
-   1 día; se muestra en intervalos de 15 minutos.  
  
-   1 semana; se muestra en intervalos de 1 día.  
  
-   1 mes; se muestra en intervalos de 1 semana.  
  
-   1 año; se muestra en intervalos de 1 mes.  
  
 Pestaña Uso del almacenamiento  
 La pestaña Uso del almacenamiento tiene una vista de árbol que muestra los detalles de utilización del almacenamiento para los archivos de base de datos y archivos de registro que pertenecen a la aplicación de capa de datos seleccionada en la vista de lista. Observe que los datos sobre el momento muestran la fecha y hora locales del UCP mediante el tipo de datos datetime. Para más información, consulte el tema [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) . Al utilizar el modelo de objetos de la utilidad, observe que SSMS utiliza el tipo de datos datetimeoffset. Para más información, consulte el tema [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 La presentación se puede agrupar según el grupo de archivos o según el volumen. Para utilizar la vista de árbol de grupo de archivos, seleccione el botón de radio **Grupo de archivos** en **Archivos agrupados por:** selección.  
  
 Los datos que se muestran en el gráfico del historial de la utilización del almacenamiento cambian en función del nodo seleccionado en la vista de árbol:  
  
-   Seleccione el nodo de grupo de archivos para mostrar un gráfico del espacio de archivo que utilizan todos los archivos de datos que pertenecen al grupo de archivos seleccionado.  
  
-   Seleccione el nodo de archivo de registro para mostrar un gráfico del espacio de archivo que utilizan todos los archivos de registro que pertenecen a la base de datos seleccionada.  
  
-   Seleccione el nodo de base de datos para mostrar un gráfico que contenga el espacio que utilizan todos los archivos de datos y archivos de registro que pertenecen a la base de datos seleccionada.  
  
 Para ver el estado de utilización del almacenamiento de archivos individuales, haga clic en el signo más junto a un nombre de archivo en la vista de árbol.  
  
 Los iconos de estado de mantenimiento ofrecen el estado resumido para cada grupo de archivos con respecto a los umbrales de la directiva:  
  
-   Marca de comprobación verde: la utilización del espacio de archivo de al menos un archivo de datos en el grupo de archivos no está sobreutilizada ni infrautilizada.  
  
-   Flecha verde hacia abajo: la utilización del espacio de archivo de al menos un archivo de datos en el grupo de archivos está infrautilizada y no hay archivos sobreutilizados en el grupo de archivos.  
  
-   Flecha roja hacia arriba: el uso del espacio de archivo para todos los archivos de datos en el grupo de archivos está sobreutilizado. Tenga en cuenta que si una base de datos se encuentra en estado de “emergencia”, el estado de mantenimiento mostrará el espacio de archivo de registro excesivo sobreutilizado.  
  
 Para ver los archivos según el volumen, seleccione el botón de radio **Volumen** en **Agrupar archivos por:** selección. El gráfico del historial de la utilización de almacenamiento muestra el espacio de archivo que utilizan todos los archivos de datos y todos los archivos de registro en el volumen de almacenamiento. Expanda el árbol para ver los detalles de los archivos de datos de la base de datos y de los archivos de registro individuales.  
  
 Los iconos de estado se utilizan para proporcionar el estado para cada volumen:  
  
-   Marca de verificación verde: los recursos se utilizan apropiadamente.  
  
-   Flecha verde hacia abajo: los recursos están infrautilizados.  
  
-   Flecha roja hacia arriba: los recursos está sobreutilizados.  
  
 El medidor junto a cada nombre de archivo en la pestaña Uso del almacenamiento representa la cantidad de espacio que utiliza el archivo con respecto a la capacidad efectiva del archivo. El valor porcentual que aparece junto al medidor es la proporción de la cantidad de espacio utilizado por el archivo con respecto a la capacidad efectiva del archivo. La información sobre las herramientas ofrece datos que se utilizan para calcular los porcentajes para cada volumen y para cada archivo en comparación con la capacidad efectiva.  
  
 Si no se configura el archivo para que crezca de forma automática, la capacidad efectiva será la cantidad de espacio que se asigne al archivo. Si se configura el archivo para que crezca de forma automática, la capacidad efectiva es la suma de la cantidad de espacio que en esos momentos se asigna al archivo y la cantidad de espacio disponible actualmente en el volumen.  
  
 Las directivas de utilización de almacenamiento se pueden configurar para los archivos de datos y para los archivos de registro. Para ver o cambiar los umbrales de la directiva de utilización de almacenamiento para los archivos, haga clic en el vínculo a la **directiva de archivos** en la parte inferior del panel Uso del almacenamiento. Para ver o cambiar los umbrales de la directiva de utilización del almacenamiento para un volumen de almacenamiento, haga clic en el vínculo a la **directiva de volumen** en la parte inferior del panel Uso del almacenamiento.  
  
 Para invalidar los umbrales de la directiva predeterminada, haga clic en el botón de radio **Invalidar directiva predeterminada**, especifique los valores de los límites superior e inferior y, a continuación, haga clic en **Aceptar**.  
  
 Para más información sobre cómo cambiar la tolerancia correspondiente a las infracciones de directivas, consulte [Reducir el ruido en las directivas de uso de CPU &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 Pestaña Detalles de propiedades  
 Los detalles de propiedades enumerados para las aplicaciones de capa de datos incluyen las siguientes categorías:  
  
-   Nombre de la base de datos  
  
-   Fecha de implementación  
  
-   De confianza: (True o False)  
  
-   Intercalación  
  
-   Nivel de compatibilidad: (por ejemplo, Versión100)  
  
-   Cifrado habilitado: (True o False)  
  
-   Modelo de recuperación: (simple, completo u optimizado para cargas masivas)  
  
-   Último momento notificado: esta columna muestra la fecha y hora local del UCP mediante el tipo de datos datetime. Para más información, consulte el tema [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) . Al utilizar el modelo de objetos de la utilidad, observe que SSMS utiliza el tipo de datos datetimeoffset. Para más información, consulte el tema [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) .

## <a name="managed-instance-details-sql-server-utility"></a>Detalles de las instancias administradas (Utilidad de SQL Server)
 La información de la vista Instancias administradas del Explorador de Utilidad proporciona los detalles de utilización para las instancias individuales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el historial de uso de la CPU, los detalles de utilización del almacenamiento en el nivel de archivo y la capacidad de ver y actualizar los umbrales de la directiva. Los umbrales de la directiva se pueden controlar en el nivel de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , para un equipo, para los archivos de base de datos y los archivos de registro, y en el nivel de volúmenes de almacenamiento. También se pueden ver los detalles sobre las propiedades correspondientes a las instancias administradas individuales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="uielement-list"></a>Lista de UIElement  
 Vista de lista  
 La vista de lista del panel superior muestra los datos sobre las instancias individuales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se enumeran en las filas según mombreDeEquipo\nombreDeInstancia.  
  
 Los iconos de estado de mantenimiento proporcionan un resumen del estado de cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por categoría de utilización:  
  
-   Marca de verificación verde - ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") - Número de instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no están infringiendo las directivas de uso de recursos. Los recursos se utilizan apropiadamente.  
  
-   Flecha verde hacia abajo - ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") - Los recursos están infrautilizados.  
  
-   Flecha roja hacia arriba - ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_up_arrow") - Los recursos están sobreutilizados.  
  
 La secuencia de columnas en la vista de lista se puede cambiar, para ello arrastre las columnas hacia la izquierda o la derecha. En la vista de lista, se pueden agregar o eliminar columnas, para ello haga clic en los encabezados de columna y seleccione columnas o anule su selección. El menú contextual también proporciona opciones de ordenación. La capacidad de ordenación también se puede activar si hace clic en la parte superior del nombre de una columna.  
  
 Para tener acceso a las opciones de filtro de la vista de lista de la utilidad, haga clic con el botón derecho en el nodo **Instancias administradas** en el panel de navegación del Explorador de Utilidad y seleccione **Filtro**. Una vez se haya implementado la configuración del filtro, aparecerá la etiqueta **Instancias administradas (filtradas)** en el nodo **Instancias administradas** del Explorador de Utilidad. Para más información, consulte [Configuración del filtro &#40;Explorador de objetos y Explorador de Utilidad&#41;](http://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2).  
  
 De forma predeterminada, las siguientes columnas muestran información sobre el estado de mantenimiento con respecto a cada instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   CPU de instancia: muestra el estado de mantenimiento de la utilización del procesador asignado a esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El estado de mantenimiento para este parámetro se determina según la directiva de utilización de la CPU establecida para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la opción de configuración para la directiva de evaluación de recursos volátiles. Para obtener más información, vea [Reducir el ruido en las directivas de uso de la CPU &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para ver el historial de utilización del procesador para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o para ver o cambiar los límites de la directiva, haga clic en la pestaña **Uso de la CPU** .  
  
-   CPU del sistema informático: muestra el estado de mantenimiento de la utilización del procesador del sistema informático. El estado de mantenimiento para este parámetro se determina según la directiva de utilización de la CPU establecida para el sistema informático y la opción de configuración para la directiva de evaluación de recursos volátiles. Para obtener más información, vea [Reducir el ruido en las directivas de uso de la CPU &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para ver el historial de utilización del procesador para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o para ver o cambiar los límites de la directiva, haga clic en la pestaña **Uso de la CPU** .  
  
-   Espacio de archivo: muestra un resumen del estado de mantenimiento del uso de los archivos de todas las bases de datos que pertenecen a la instancia seleccionada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si el estado de mantenimiento de cualquier base de datos está sobreutilizado, el estado de mantenimiento del espacio de archivo se notificará como sobreutilizado en la vista de lista. Si el estado de mantenimiento de cualquier base de datos está infrautilizado y ninguna base de datos esta sobreutilizada, el estado del espacio de archivo se notificará como infrautilizado en la vista de lista. De lo contrario, el estado de mantenimiento del espacio de archivo se notificará como utilizado apropiadamente en la vista de lista. Para ver o cambiar los límites de la directiva, haga clic en la pestaña **Uso del almacenamiento** .  
  
-   Espacio de volumen: muestra un resumen de los estados de mantenimiento de la utilización del espacio de volumen para todos los volúmenes que contienen bases de datos que pertenecen a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]seleccionada. Si el estado de mantenimiento de cualquier volumen está sobreutilizado, el estado de mantenimiento del espacio de volumen se notificará como sobreutilizado en la vista de lista. Si el estado de mantenimiento de cualquier volumen está infrautilizado y no hay volúmenes que estén sobreutilizados, el estado de mantenimiento del espacio de volumen se notificará como infrautilizado en la vista de lista. De lo contrario, el estado de mantenimiento del espacio de volumen se notificará como utilizado apropiadamente en la vista de lista. Para ver o cambiar los límites de la directiva, haga clic en la pestaña **Uso del almacenamiento** .  
  
-   Tipo de directiva: indica si las opciones de directiva predeterminada global y directiva personalizada invalidada están habilitadas para la instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Otras de las columnas que se pueden mostrar con el menú contextual en la zona del encabezado de la columna de vista de lista:  
  
-   Nombre del procesador:  
  
-   Velocidad del procesador (MHz):  
  
-   Recuento del procesador:  
  
-   Memoria física (MB):  
  
-   Versión del sistema operativo:  
  
-   Versión de SQL Server:  
  
-   Edición de SQL Server:  
  
-   Agrupado: (True o False)  
  
-   Directorio de copia de seguridad:  
  
-   Intercalación:  
  
-   Distinción de mayúsculas y minúsculas: (True o False)  
  
-   Idioma:  
  
-   Último momento notificado: esta columna muestra la fecha y hora local del UCP mediante el tipo de datos datetime. Para más información, consulte el tema [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) . Al utilizar el modelo de objetos de la utilidad, observe que SSMS utiliza el tipo de datos datetimeoffset. Para más información, consulte el tema [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Pestaña Uso de la CPU  
 La pestaña Uso de CPU muestra gráficos en paralelo de datos históricos para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el uso de la CPU del sistema informático.  
  
 El gráfico muestra el historial de utilización del procesador para el intervalo especificado en los botones de radio a la derecha de la zona de visualización. Para cambiar el intervalo de presentación y actualizar el conjunto de datos, seleccione un botón de radio en la lista.  
  
 Las opciones de intervalo son las siguientes:  
  
-   1 día; se muestra en intervalos de 15 minutos.  
  
-   1 semana; se muestra en intervalos de 1 día.  
  
-   1 mes; se muestra en intervalos de 1 semana.  
  
-   1 año; se muestra en intervalos de 1 mes.  
  
 Pestaña Uso del almacenamiento  
 La pestaña Uso del almacenamiento tiene una vista de árbol que muestra los detalles de la utilización del almacenamiento. Observe que los datos sobre el momento muestran la fecha y hora locales del UCP mediante el tipo de datos datetime. Para más información, consulte el tema [datetime (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=164071) . Al utilizar el modelo de objetos de la utilidad, observe que SSMS utiliza el tipo de datos datetimeoffset. Para más información, consulte el tema [datetimeoffset (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 La presentación se puede agrupar según la base de datos o según el volumen. Para utilizar la vista de árbol de la base de datos, seleccione el botón de opción **Base de datos** en **Agrupar archivos por:** selección. Para ver el estado de la utilización del almacenamiento para los archivos de base de datos individuales, haga clic en el signo más junto a un nombre de base de datos en la vista de árbol. Los archivos de base de datos incluyen todas las bases de datos del usuario y del sistema que pertenecen a la instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ha seleccionado en la vista de lista.  
  
 La estructura de árbol corresponde a la jerarquía de almacenamiento. El nodo raíz en la vista de árbol es la base de datos. El nivel siguiente de la vista de árbol contiene un nodo de grupo de archivos, o bien nodos que pertenecen a la base de datos y un nodo de archivo de registro para los registros que pertenecen a la base de datos. El nivel siguiente contiene los archivos de datos que pertenecen al grupo de archivos.  
  
 Los datos que se muestran en el gráfico del historial de la utilización del almacenamiento cambian en función del nodo seleccionado en la vista de árbol:  
  
-   Seleccione el nodo de grupo de archivos para mostrar un gráfico del espacio de archivo que utilizan todos los archivos de datos que pertenecen al grupo de archivos seleccionado.  
  
-   Seleccione el nodo de archivo de registro para mostrar un gráfico del espacio de archivo que utilizan todos los archivos de registro que pertenecen a la base de datos seleccionada.  
  
-   Seleccione el nodo de base de datos para mostrar un gráfico que contenga el espacio que utilizan todos los archivos de datos y archivos de registro que pertenecen a la base de datos seleccionada.  
  
 Los iconos de estado de mantenimiento ofrecen un estado resumido de los archivos de base de datos, grupos de archivos y archivos de registro:  
  
 Para las bases de datos:  
  
-   Marca de verificación verde: los estados de mantenimiento de todos los grupos de archivos y archivos de registro son sobreutilizado o infrautilizado.  
  
-   Flecha verde hacia abajo: los estados de mantenimiento de al menos un grupo de archivos o del archivo de registro son infrautilizado y no hay estados de mantenimiento que sean sobreutilizado.  
  
-   Flecha roja hacia arriba: el estado de mantenimiento de al menos un grupo de archivos o del archivo de registro es sobreutilizado.  
  
 Para grupos de archivo y archivos de registro:  
  
-   Marca de verificación verde: la utilización del espacio de archivo para todos los archivos en el grupo de archivos no está ni sobreutilizada ni infrautilizada.  
  
-   Flecha verde hacia abajo: la utilización del espacio de archivo para al menos un archivo en el grupo de archivos está infrautilizada y no hay archivos sobreutilizados en el grupo de archivos.  
  
-   Flecha roja hacia arriba: el uso del espacio de archivo para todos los archivos de datos en el grupo de archivos está sobreutilizado.  
  
 Para ver los archivos según el volumen, seleccione el botón de radio **Volumen** en **Agrupar archivos por:** selección. El gráfico del historial de la utilización de almacenamiento muestra el espacio de archivo que utilizan todos los archivos de datos y todos los archivos de registro en el volumen de almacenamiento. Expanda el árbol para ver los detalles de los archivos de datos de la base de datos y de los archivos de registro individuales.  
  
 Los iconos de estado se utilizan para proporcionar el estado para cada volumen:  
  
-   Marca de verificación verde: los recursos se utilizan apropiadamente.  
  
-   Flecha verde hacia abajo: los recursos están infrautilizados.  
  
-   Flecha roja hacia arriba: los recursos está sobreutilizados.  
  
 El medidor junto a cada nombre de archivo en la pestaña Uso del almacenamiento representa la cantidad de espacio que utiliza el archivo con respecto a la capacidad efectiva del archivo. El valor porcentual que aparece junto al medidor es la proporción de la cantidad de espacio utilizado por el archivo con respecto a la capacidad efectiva del archivo. La información sobre las herramientas ofrece datos que se utilizan para calcular los porcentajes para cada volumen y para cada archivo en comparación con la capacidad efectiva.  
  
 Si no se configura el archivo para que crezca de forma automática, la capacidad efectiva será la cantidad de espacio que se asigne al archivo. Si se configura el archivo para que crezca de forma automática, la capacidad efectiva es la suma de la cantidad de espacio que en esos momentos se asigna al archivo y la cantidad de espacio disponible actualmente en el volumen.  
  
 Las directivas de utilización de almacenamiento se pueden configurar para los archivos de datos y para los archivos de registro. Para ver o cambiar los umbrales de la directiva de utilización de almacenamiento para los archivos, haga clic en el vínculo a la **directiva de archivos** en la parte inferior del panel Uso del almacenamiento. Para ver o cambiar los umbrales de la directiva de utilización del almacenamiento para un volumen de almacenamiento, haga clic en el vínculo a la **directiva de volumen** en la parte inferior del panel Uso del almacenamiento.  
  
 Para invalidar los umbrales de la directiva predeterminada, haga clic en el botón de radio **Invalidar directiva predeterminada**, especifique los valores de los límites superior e inferior y, a continuación, haga clic en **Aceptar**.  
  
 Para más información sobre cómo cambiar la tolerancia correspondiente a las infracciones de directivas, consulte [Reducir el ruido en las directivas de uso de CPU &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 Pestaña Detalles de propiedades  
 Los detalles de las propiedades que se enumeran para las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluyen las siguientes categorías:  
  
-   Nombre del procesador:  
  
-   Velocidad del procesador (MHz):  
  
-   Recuento del procesador:  
  
-   Memoria física (MB):  
  
-   Versión del sistema operativo:  
  
-   Versión de SQL Server:  
  
-   Edición de SQL Server:  
  
-   Agrupado: (True o False)  
  
-   Directorio de copia de seguridad:  
  
-   Intercalación:  
  
-   Distinción de mayúsculas y minúsculas: (True o False)  
  
-   Idioma:  

## <a name="utility-administration-sql-server-utility"></a>Administración de la utilidad (utilidad de SQL Server)
Utilice las pestañas Administración de la utilidad para administrar la configuración de directivas, la seguridad y el almacenamiento de datos de una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información sobre conceptos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
### <a name="uielement-list"></a>Lista de UIElement
 **Pestaña Directiva** : use la pestaña de directivas para ver o especificar las directivas globales de supervisión.  
  
 Establezca directivas globales de supervisión de aplicaciones de capas de datos. Para expandir la lista de valores correspondiente a esta opción, haga clic en la flecha junto al nombre de la directiva o haga clic en el título de la directiva.  
 ¿Cuándo se queda una aplicación sin capacidad de procesamiento? Para cambiar esta directiva, utilice el control a la derecha de la descripción de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El valor máximo predeterminado de utilización del procesador es 70%.  
  
-   El valor mínimo predeterminado de utilización del procesador es 0%.  
  
 ¿Cuándo se queda una aplicación sin espacio para archivos? Para cambiar la directiva correspondiente a la utilización del espacio de un archivo de datos o un archivo de registro, utilice el control a la derecha de la descripción de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El valor máximo predeterminado de utilización de espacio de archivos es 70%.  
  
-   El valor mínimo predeterminado de utilización de espacio de archivos es 0%.  
  
 Establezca las directivas globales de supervisión de aplicaciones de instancias administradas de SQL Server. Para expandir la lista de valores correspondiente a esta opción, haga clic en la flecha junto al nombre de la directiva o haga clic en el título de la directiva.  
 ¿Cuándo se queda una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin capacidad de procesamiento? Para cambiar esta directiva, utilice el control a la derecha de la descripción de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El valor máximo predeterminado de utilización del procesador de instancias es 70%.  
  
-   El valor mínimo predeterminado de utilización del procesador de instancias es 0%.  
  
 ¿Cuándo se queda una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin capacidad de procesamiento en el sistema informático? Para cambiar esta directiva, utilice el control a la derecha de la descripción de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El valor máximo predeterminado de utilización del procesador del sistema informático es 70%.  
  
-   El valor mínimo predeterminado de utilización del procesador del sistema informático es 0%.  
  
 ¿Cuándo se queda una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin espacio para archivos? Para cambiar la directiva correspondiente a la utilización del espacio de un archivo de datos o un archivo de registro, utilice el control a la derecha de la descripción de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El valor máximo predeterminado de utilización de espacio de archivos es 70%.  
  
-   El valor mínimo predeterminado de utilización de espacio de archivos es 0%.  
  
 ¿Cuándo se queda una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin espacio de volumen de almacenamiento en el equipo? Para cambiar esta directiva, utilice el control a la derecha de la descripción de la directiva y, a continuación, haga clic en **Aplicar**. También puede restaurar los valores predeterminados o descartar los cambios con los botones en la parte inferior de la pantalla.  
  
-   El valor máximo predeterminado de utilización de espacio de volumen en el sistema informático es 70%.  
  
-   El valor mínimo predeterminado de utilización de espacio de volumen en el sistema informático es 0%.  
  
 Reducción del ruido que provoca la infracción de directivas en recursos muy volátiles. Para expandir los controles correspondientes a esta característica, haga clic en la flecha hacia abajo a la derecha de la pantalla.  
 Para obtener más información, vea [Reducir el ruido en las directivas de uso de la CPU &#40;utilidad de SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 
**Pestaña Seguridad**: muestra los nombres de inicio de sesión con permisos para administrar el UCP o poder leer desde él.  
  
 Seleccione los inicios de sesión del UCP que se agregarán al rol Lector de utilidad.  
 Los privilegios del rol Lector de utilidad hacen posible que la cuenta de usuario:  
  
-   Se conecte a la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Vea todos los puntos de vista en el explorador de la utilidad en SSMS.  
  
-   Vea los valores de configuración en el nodo Administración de la utilidad en el explorador de la utilidad en SSMS.  
  
 Los administradores de la utilidad pueden inscribir instancias de SQL Server y quitar instancias de SQL Server de una Utilidad de SQL Server, así como modificar directivas en instancias administradas y valores de administración en el UCP.  
  
 Para ser administrador de la utilidad, debe disponer de privilegios sysadmin en la instancia de SQL Server. Para agregar o cambiar las cuentas de usuario para el UCP de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilice Explorador de objetos en SSMS con el fin de agregar al usuario a los inicios de sesión del servidor de la instancia de UCP de SQL Server. Para obtener más información, vea [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md).  
  
 
Pestaña **Almacenamiento de datos**: muestra los detalles de configuración para el almacén de administración de datos de la utilidad.  
  
 Retención de datos  
 Especifique el período de retención de datos para obtener la información de utilización que se haya recopilado para las instancias administradas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El período predeterminado es 1 año. El valor mínimo es de 1 mes. El valor máximo admitido es 2 años.  
  
 Información de configuración de almacenamiento de datos de utilidad  
 Los siguientes valores de configuración no se pueden establecer en esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Nombre de UMDW: Sysutility_mdw_\<GUID>_DATA.  
  
-   Frecuencia de la carga del conjunto de recopilación: cada 15 minutos.  
  
 El directorio de UMDW se puede configurar: \<Unidad del sistema:>:Archivos de programa\Microsoft SQL Server\MSSQL10_50.<Nombre_UCP\MSSQL\Data\\,donde \<Unidad del sistema> normalmente es la unidad C:\. El archivo de registro, UMDW_\<GUID>_LOG, se encuentra en el mismo directorio.  
  
> **NOTA:** La ubicación del archivo UMDW (sysutility_mdw) se puede cambiar mediante detach/attach o ALTER DATABASE. Recomendamos el uso de ALTER DATABASE. Para obtener más información, vea [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 Restablecer los valores originales  
 Para restablecer los valores de esta pestaña a los valores predeterminados, haga clic en el botón **Restaurar valores predeterminados** y, luego, en **Aplicar**.  
 
  
## <a name="reference"></a>Referencia  
 [Crear un punto de control de la Utilidad de SQL Server &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)  
  
 [Conectarse a una utilidad de SQL Server](../../relational-databases/manage/connect-to-a-sql-server-utility.md)  
  
 [Inscribir una instancia de SQL Server &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)  
  
 [Configurar las directivas de mantenimiento &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)  
  
 [Supervisar instancias de SQL Server en la utilidad de SQL Server](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
## <a name="see-also"></a>Ver también  
 [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Solucionar problemas de la Utilidad de SQL Server](http://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
