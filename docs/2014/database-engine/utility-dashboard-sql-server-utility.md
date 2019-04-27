---
title: Panel de la utilidad (utilidad de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 999eb741-4a60-43f6-ab37-2df7dce845c1
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5f0eb497499eafe16756becfb9607b925add08e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62773817"
---
# <a name="utility-dashboard-sql-server-utility"></a>Panel de la utilidad (utilidad de SQL Server)
  Para ver los datos en el panel de la utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], seleccione el nodo superior en el árbol del explorador de la utilidad (identificado como "Utilidad<UCP_Name>\\(nombreDeEquipo\UCP)"). El panel incluye un resumen y datos detallados de todas las instancias administradas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y de todas las aplicaciones de capa de datos en la utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para actualizar los datos en el panel, haga clic con el botón derecho en el nodo superior del árbol del explorador de la utilidad y seleccione **Actualizar**.  
  
 Para obtener más información sobre cómo crear un punto de control de la utilidad, vea [Crear un punto de control de la Utilidad de SQL Server &#40;Utilidad de SQL Server&#41;](../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md). Para obtener más información sobre cómo agregar una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a la Utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , vea [Inscribir una instancia de SQL Server &#40;Utilidad de SQL Server&#41;](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md).  
  
## <a name="uielement-list"></a>Lista de UIElement  
 Estado de mantenimiento de la instancia administrada  
 El estado de mantenimiento de las instancias administrados de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se muestra en a la izquierda del panel de contenido del explorador de la utilidad.  
  
 Los parámetros del estado de la instancia administrada son como sigue:  
  
-   Utilización de la CPU para la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Utilización de archivos de base de datos.  
  
-   Utilización del espacio de volumen de almacenamiento.  
  
-   Utilización de la CPU para el sistema informático.  
  
-   El estado de cada parámetro se divide en tres categorías:  
  
-   Utilizado apropiadamente: número de instancias administradas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que no están infringiendo las directivas de utilización de recursos.  
  
-   Infrautilizado: número de recursos administrados que están infringiendo las directivas de infrautilización de recursos.  
  
-   Sobreutilizado: número de recursos administrados que están infringiendo las directivas de sobreutilización de recursos.  
  
-   No hay datos disponibles: no hay datos disponibles para las instancias administradas de SQL Server porque su instancia acaba de inscribirse y no se ha completado la primera operación de recopilación de datos, o bien porque hay un problema con la instancia administrada de SQL Server con respecto a la recopilación y carga de datos en el UCP.  
  
 El estado detallado de cada parámetro de estado se muestra en indicadores deslizantes. La zona a la derecha de los indicadores deslizantes muestra el número de instancias administradas que se encuentran en cada categoría de estado.  
  
 Para crear una vista filtrada de una instancia administrada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o una aplicación de nivel de datos, haga clic en el vínculo de una categoría de utilización al lado de su indicador deslizante en el panel de la utilidad. Por ejemplo, si hace clic en **CPU de instancia sobreutilizada** en el panel **Contenido del explorador de la utilidad** , SSMS crea una vista de lista filtrada de instancias administradas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cuya CPU está sobreutilizada en función de los valores de directiva actuales.  
  
 Observe que, al hacer clic en un vínculo de una categoría de utilización, se agrega **(filtrado)** al nodo correspondiente en el panel de navegación del explorador de la utilidad; es decir, **Instancias administradas** se etiqueta **Instancias administradas (filtrado)**. Para ver la configuración del filtro, haga clic con el botón derecho en el nodo en el panel de navegación y seleccione **Filtro**y, después, haga clic en **Configuración del filtro**. Para borrar la configuración del filtro, haga clic con el botón derecho en el nodo en el panel de navegación, seleccione **Filtro** y, después, haga clic en **Quitar filtro**.  
  
 Para obtener más información sobre cómo ver el estado de mantenimiento de instancias individuales de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o para ver o cambiar la configuración de la directiva, vea [Detalles de las instancias administradas &#40;Utilidad de SQL Server&#41;](../../2014/database-engine/managed-instance-details-sql-server-utility.md).  
  
 Resumen de la utilidad  
 Muestra el número de instancias administradas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y el número de aplicaciones de capa de datos que administra la utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Estado de las aplicaciones de capa de datos  
 El estado de mantenimiento de las aplicaciones de capa de datos se muestra en la parte derecha del panel de contenido del explorador de la utilidad.  
  
 Los parámetros de estado de las aplicaciones de capa de datos son como sigue:  
  
-   Utilización de la CPU para la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Utilización de archivos de base de datos.  
  
-   Utilización del espacio de volumen de almacenamiento.  
  
-   Utilización de la CPU para el sistema informático.  
  
 El estado de cada parámetro se divide en tres categorías:  
  
-   Utilizado apropiadamente: número de aplicaciones de capa de datos que no están infringiendo las directivas de utilización de recursos.  
  
-   Sobreutilizado: número de aplicaciones de capa de datos que están infringiendo las directivas de sobreutilización de recursos.  
  
-   Infrautilizado: número de aplicaciones de capa de datos que están infringiendo las directivas de infrautilización de recursos.  
  
-   No hay datos disponibles: no hay datos disponibles para las aplicaciones de capa de datos porque la instancia administrada de SQL Server que contiene la aplicación de capa de datos no está efectuando la notificación de datos.  
  
 El estado detallado de cada parámetro de estado se muestra en indicadores deslizantes. La zona a la derecha de los indicadores deslizantes muestra el número de aplicaciones de capa de datos que se encuentran en cada categoría de estado. Para obtener más información sobre cómo ver el estado de mantenimiento de aplicaciones de capa de datos individuales o para ver o cambiar la configuración de la directiva, vea [Detalles de la aplicación de capa de datos implementada &#40;Utilidad de SQL Server&#41;](../../2014/database-engine/deployed-data-tier-application-details-sql-server-utility.md).  
  
 Historial de la utilización del almacenamiento de la utilidad  
 El historial de utilización se muestra en un gráfico cronológico en la parte inferior del panel de la utilidad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Observe que los datos sobre el momento muestran la fecha y hora locales del UCP mediante el tipo de datos datetime. Para obtener más información, vea el tema [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) de los Libros en pantalla de SQL Server. Al utilizar el modelo de objetos de la utilidad, observe que SSMS utiliza el tipo de datos datetimeoffset. Para obtener más información, vea el tema [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) de los Libros en pantalla de SQL Server.  
  
 Utilice los botones de radio a la izquierda del área de presentación para cambiar los periodos de notificación del gráfico.  
  
 Las opciones de intervalo de notificación son:  
  
-   1 día; se muestra en intervalos de 15 minutos.  
  
-   1 semana; se muestra en intervalos de 1 día.  
  
-   1 mes; se muestra en intervalos de 1 semana.  
  
-   1 año; se muestra en intervalos de 1 mes.  
  
 Después de modificar el intervalo de notificación, los datos se actualizan automáticamente.  
  
 Utilización del almacenamiento de la utilidad  
 En la parte inferior derecha del panel, el gráfico circular sobre la utilización de almacenamiento muestra la proporción de espacio utilizado en comparación con el espacio disponible en los volúmenes de los equipos que contienen instancias administradas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Los datos de esta presentación se actualizan cada 15 minutos.  
  
## <a name="see-also"></a>Vea también  
 [Utilizar el explorador de Utilidad para administrar la utilidad de SQL Server](../relational-databases/manage/use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [Inscribir una instancia de SQL Server &#40;utilidad de SQL Server&#41;](../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)   
 [Modificar una definición de la directiva de mantenimiento de recursos &#40;Utilidad de SQL Server&#41;](../relational-databases/manage/modify-a-resource-health-policy-definition-sql-server-utility.md)  
  
  
