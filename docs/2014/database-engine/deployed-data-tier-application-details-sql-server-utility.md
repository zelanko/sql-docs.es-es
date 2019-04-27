---
title: Implementa los detalles de la aplicación de capa de datos (utilidad de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.UE.dac.details.F1
helpviewer_keywords:
- utility, management
- Utility
- SQL Server Utility [SQL Server]
- data-tier application [SQL Server], utility details
- Multi-server management [SQL Server]
ms.assetid: 79c41dd9-abcb-434e-9326-00a341d5c867
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0ca9186b93e96c60e1c5128e385b5b77d5f2b94e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62754112"
---
# <a name="deployed-data-tier-application-details-sql-server-utility"></a>Detalles de la aplicación de capa de datos implementada (Utilidad de SQL Server)
  La información en la vista de aplicaciones de capa de datos implementadas del explorador de Utilidad facilita datos de utilización para las aplicaciones de capa de datos individuales, el historial de la utilización de la CPU, los detalles de la utilización del almacenamiento de nivel de archivo, y la capacidad para ver y actualizar los umbrales de directivas. Los umbrales de directivas se pueden supervisar en el nivel de la aplicación de capa de datos para la utilización de la CPU y para los archivos de datos y de registro de la base de datos. También puede ver los detalles de propiedades para las aplicaciones de capa de datos individuales.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 Vista de lista  
 La vista de lista en el panel superior muestra los datos sobre las aplicaciones de capa de datos individuales. Los iconos de estado de mantenimiento proporcionan un resumen del estado para cada aplicación de capa de datos por categoría de utilización:  
  
-   Marca de verificación verde - ![](../../2014/database-engine/media/well-utilized.gif "Well_utilized") - Número de aplicaciones de capa de datos que no están infringiendo las directivas de uso de recursos. Los recursos se utilizan apropiadamente.  
  
-   Flecha verde hacia abajo - ![](../../2014/database-engine/media/utility-down-arrow.gif "Utility_down_arrow") - Los recursos están infrautilizados.  
  
-   Flecha roja hacia arriba - ![](../../2014/database-engine/media/utility-up-arrow.gif "Utility_up_arrow") - Los recursos están sobreutilizados.  
  
 La secuencia de columnas en la vista de lista se puede cambiar, para ello arrastre las columnas hacia la izquierda o la derecha. En la vista de lista, se pueden agregar o eliminar columnas, para ello haga clic en los encabezados de columna y seleccione columnas o anule su selección. El menú contextual también proporciona opciones de ordenación. La capacidad de ordenación también se puede activar si hace clic en la parte superior del nombre de una columna.  
  
 Para tener acceso a las opciones de filtro para la vista de lista de la utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , haga clic con el botón derecho en el nodo **Aplicaciones de capa de datos implementadas** en el panel de navegación del Explorador de Utilidad y seleccione **Filtro**. Una vez implementada la configuración del filtro, el nodo **Aplicaciones de capa de datos implementadas** en el Explorador de Utilidad se etiquetará con **Aplicaciones de capa de datos implementadas (filtradas)**. Para más información, consulte [Configuración del filtro &#40;Explorador de objetos y Explorador de Utilidad&#41;](../ssms/object/filter-settings-object-explorer-and-utility-explorer.md).  
  
 De forma predeterminada, las siguientes columnas muestran información sobre el estado de mantenimiento de cada aplicación de capa de datos.  
  
-   Nombre: el nombre de la aplicación de capa de datos.  
  
-   CPU de la aplicación: muestra el estado de mantenimiento de la utilización del procesador para esta aplicación de capa de datos. El estado de mantenimiento para este parámetro se determina según la directiva de utilización de CPU establecida para la aplicación de capa de datos y la opción de configuración para la directiva de evaluación de recursos volátiles. Para obtener más información, vea [Reducir el ruido en las directivas de uso de la CPU &#40;Utilidad de SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para ver el historial de utilización del procesador para esta aplicación de capa de datos o para ver o cambiar los límites de la directiva, haga clic en la pestaña **Uso de CPU**.  
  
-   CPU del sistema informático: muestra el estado de mantenimiento de la utilización del procesador del sistema informático. El estado de mantenimiento para este parámetro se determina según la directiva de utilización de la CPU establecida para el sistema informático y la opción de configuración para la directiva de evaluación de recursos volátiles. Para obtener más información, vea [Reducir el ruido en las directivas de uso de la CPU &#40;Utilidad de SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Para ver el historial de utilización del procesador para esta aplicación de capa de datos o para ver o cambiar los límites de la directiva, haga clic en la pestaña **Uso de CPU**.  
  
-   Espacio de archivo: muestra un resumen de los estados de mantenimiento de la utilización del espacio de archivo para cada aplicación de capa de datos.  
  
    -   Marca de comprobación verde: los estados de mantenimiento para todos los grupos de archivos y el grupo de archivos de registro son sobreutilizado o infrautilizado.  
  
    -   Flecha verde hacia abajo: el estado de mantenimiento para al menos un grupo de archivos o para el grupo de archivos de registro es infrautilizado, no hay grupos de archivos ni un grupo de archivos de registro que estén sobreutilizados.  
  
    -   Flecha roja hacia arriba: el estado de mantenimiento para al menos un grupo de archivos o el grupo de archivos de registro es sobreutilizado. Tenga en cuenta que si una base de datos se encuentra en estado de "emergencia", el estado de mantenimiento mostrará el espacio de archivo de registro excesivo sobreutilizado.  
  
     Para ver o cambiar los límites de la directiva de espacio de archivo, haga clic en la pestaña **Uso del almacenamiento** .  
  
-   Espacio de volumen: muestra un resumen de los estados de mantenimiento de la utilización del espacio de volumen para todos los volúmenes que contienen bases de datos que pertenecen a la aplicación de capa de datos seleccionada. Si el estado de mantenimiento de cualquier volumen está sobreutilizado, el estado de mantenimiento del espacio de volumen se notificará como sobreutilizado en la vista de lista. Si el estado de mantenimiento de cualquier volumen está infrautilizado y no hay volúmenes que estén sobreutilizados, el estado de mantenimiento del espacio de volumen se notificará como infrautilizado en la vista de lista. De lo contrario, el estado de mantenimiento del espacio de volumen se notificará como utilizado apropiadamente en la vista de lista. Para ver o cambiar los límites de la directiva, haga clic en la pestaña **Uso del almacenamiento** .  
  
-   Tipo de directiva: indica si las directivas predeterminadas globales y directivas personalizadas invalidadas están habilitadas para la aplicación de capa de datos.  
  
-   Nombre de instancia: muestra el nombre de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que hospeda las aplicaciones de capa de datos.  
  
 Otras de las columnas que se pueden mostrar con el menú contextual en la zona del encabezado de la columna de vista de lista:  
  
-   Nombre de la base de datos  
  
-   Fecha de implementación  
  
-   Confianza: (True o False)  
  
-   Intercalación  
  
-   Nivel de compatibilidad: (por ejemplo, Versión100)  
  
-   Cifrado habilitado: (True o False)  
  
-   Modelo de recuperación: (Simple, completa o Bulk-Logged.)  
  
-   Última hora notificada: Esta columna muestra el UCP fecha y hora local mediante el tipo de datos de fecha y hora. Para obtener más información, vea el tema [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) de los Libros en pantalla de SQL Server. Al utilizar el modelo de objetos de la utilidad, observe que SSMS utiliza el tipo de datos datetimeoffset. Para obtener más información, vea el tema [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) de los Libros en pantalla de SQL Server.  
  
 Pestaña Uso de la CPU  
 La pestaña Uso de la CPU muestra gráficos en paralelo de datos históricos para la aplicación de capa de datos y la utilización de la CPU del sistema informático.  
  
 El gráfico muestra el historial de utilización del procesador para el intervalo especificado en los botones de radio a la derecha de la zona de visualización. Para cambiar el intervalo de presentación y actualizar el conjunto de datos, seleccione un botón de radio en la lista.  
  
 Las opciones de intervalo son las siguientes:  
  
-   1 día; se muestra en intervalos de 15 minutos.  
  
-   1 semana; se muestra en intervalos de 1 día.  
  
-   1 mes; se muestra en intervalos de 1 semana.  
  
-   1 año; se muestra en intervalos de 1 mes.  
  
 Pestaña Uso del almacenamiento  
 La pestaña Uso del almacenamiento tiene una vista de árbol que muestra los detalles de utilización del almacenamiento para los archivos de base de datos y archivos de registro que pertenecen a la aplicación de capa de datos seleccionada en la vista de lista. Observe que los datos sobre el momento muestran la fecha y hora locales del UCP mediante el tipo de datos datetime. Para obtener más información, vea el tema [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) de los Libros en pantalla de SQL Server. Al utilizar el modelo de objetos de la utilidad, observe que SSMS utiliza el tipo de datos datetimeoffset. Para obtener más información, vea el tema [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) de los Libros en pantalla de SQL Server.  
  
 La presentación se puede agrupar según el grupo de archivos o según el volumen. Para utilizar la vista de árbol de grupo de archivos, seleccione el botón de radio **Grupo de archivos** en **Archivos agrupados por:** selección.  
  
 Los datos que se muestran en el gráfico del historial de la utilización del almacenamiento cambian en función del nodo seleccionado en la vista de árbol:  
  
-   Seleccione el nodo de grupo de archivos para mostrar un gráfico del espacio de archivo que utilizan todos los archivos de datos que pertenecen al grupo de archivos seleccionado.  
  
-   Seleccione el nodo de archivo de registro para mostrar un gráfico del espacio de archivo que utilizan todos los archivos de registro que pertenecen a la base de datos seleccionada.  
  
-   Seleccione el nodo de base de datos para mostrar un gráfico que contenga el espacio que utilizan todos los archivos de datos y archivos de registro que pertenecen a la base de datos seleccionada.  
  
 Para ver el estado de utilización del almacenamiento de archivos individuales, haga clic en el signo más junto a un nombre de archivo en la vista de árbol.  
  
 Los iconos de estado de mantenimiento ofrecen el estado resumido para cada grupo de archivos con respecto a los umbrales de la directiva:  
  
-   Marca de comprobación verde: la utilización del espacio de archivo de al menos un archivo de datos en el grupo de archivos no está sobreutilizada ni infrautilizada.  
  
-   Flecha verde hacia abajo: la utilización del espacio de archivo de al menos un archivo de datos en el grupo de archivos está infrautilizada y no hay archivos sobreutilizados en el grupo de archivos.  
  
-   Flecha roja hacia arriba: el uso del espacio de archivo para todos los archivos de datos en el grupo de archivos está sobreutilizado. Tenga en cuenta que si una base de datos se encuentra en estado de "emergencia", el estado de mantenimiento mostrará el espacio de archivo de registro excesivo sobreutilizado.  
  
 Para ver los archivos según el volumen, seleccione el botón de radio **Volumen** en **Agrupar archivos por:** selección. El gráfico del historial de la utilización de almacenamiento muestra el espacio de archivo que utilizan todos los archivos de datos y todos los archivos de registro en el volumen de almacenamiento. Expanda el árbol para ver los detalles de los archivos de datos de la base de datos y de los archivos de registro individuales.  
  
 Los iconos de estado se utilizan para proporcionar el estado para cada volumen:  
  
-   Marca de verificación verde: los recursos se utilizan apropiadamente.  
  
-   Flecha verde hacia abajo: los recursos están infrautilizados.  
  
-   Flecha roja hacia arriba: los recursos está sobreutilizados.  
  
 El medidor junto a cada nombre de archivo en la pestaña Uso del almacenamiento representa la cantidad de espacio que utiliza el archivo con respecto a la capacidad efectiva del archivo. El valor porcentual que aparece junto al medidor es la proporción de la cantidad de espacio utilizado por el archivo con respecto a la capacidad efectiva del archivo. La información sobre las herramientas ofrece datos que se utilizan para calcular los porcentajes para cada volumen y para cada archivo en comparación con la capacidad efectiva.  
  
 Si no se configura el archivo para que crezca de forma automática, la capacidad efectiva será la cantidad de espacio que se asigne al archivo. Si se configura el archivo para que crezca de forma automática, la capacidad efectiva es la suma de la cantidad de espacio que en esos momentos se asigna al archivo y la cantidad de espacio disponible actualmente en el volumen.  
  
 Las directivas de utilización de almacenamiento se pueden configurar para los archivos de datos y para los archivos de registro. Para ver o cambiar los umbrales de la directiva de utilización de almacenamiento para los archivos, haga clic en el vínculo a la **directiva de archivos** en la parte inferior del panel Uso del almacenamiento. Para ver o cambiar los umbrales de la directiva de utilización del almacenamiento para un volumen de almacenamiento, haga clic en el vínculo a la **directiva de volumen** en la parte inferior del panel Uso del almacenamiento.  
  
 Para invalidar los umbrales de la directiva predeterminada, haga clic en el botón de radio **Invalidar directiva predeterminada**, especifique los valores de los límites superior e inferior y, a continuación, haga clic en **Aceptar**.  
  
 Para más información sobre cómo cambiar la tolerancia correspondiente a las infracciones de directivas, consulte [Reducir el ruido en las directivas de uso de CPU &#40;Utilidad de SQL Server&#41;](../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 Pestaña Detalles de propiedades  
 Los detalles de propiedades enumerados para las aplicaciones de capa de datos incluyen las siguientes categorías:  
  
-   Nombre de la base de datos  
  
-   Fecha de implementación  
  
-   Confianza: (True o False)  
  
-   Intercalación  
  
-   Nivel de compatibilidad: (por ejemplo, Versión100)  
  
-   Cifrado habilitado: (True o False)  
  
-   Modelo de recuperación: (Simple, completa o Bulk-Logged.)  
  
-   Última hora notificada: Esta columna muestra el UCP fecha y hora local mediante el tipo de datos de fecha y hora. Para obtener más información, vea el tema [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) de los Libros en pantalla de SQL Server. Al utilizar el modelo de objetos de la utilidad, observe que SSMS utiliza el tipo de datos datetimeoffset. Para obtener más información, vea el tema [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) de los Libros en pantalla de SQL Server.  
  
## <a name="see-also"></a>Vea también  
 [Detalles de las instancias administradas &#40;Utilidad de SQL Server&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md)   
 [Panel de la utilidad &#40;utilidad de SQL Server&#41;](../../2014/database-engine/utility-dashboard-sql-server-utility.md)   
 [Supervisar instancias de SQL Server en la utilidad de SQL Server](../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [Características y tareas de la utilidad de SQL Server](../relational-databases/manage/sql-server-utility-features-and-tasks.md)  
  
  
