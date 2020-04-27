---
title: Determinar si una tabla o un procedimiento almacenado se debe pasar a OLTP en memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- Analyze, Migrate, Report
- AMR
ms.assetid: c1ef96f1-290d-4952-8369-2f49f27afee2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de6a778f9cdbfb7ab916f40a5250ca4f9e20c811
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63072394"
---
# <a name="determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp"></a>Determinar si una tabla o un procedimiento almacenado se debe pasar a OLTP en memoria
  El recopilador de rendimiento [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] de las transacciones de le ayuda a evaluar si OLTP en memoria mejorará el rendimiento de la aplicación de base de datos. El informe de análisis del rendimiento de las transacciones indica también la cantidad de trabajo que debe realizar para habilitar OLTP en memoria en la aplicación. Después de identificar una tabla basada en disco para convertirla a OLTP en memoria, puede usar el [Asistente de optimización de memoria](memory-optimization-advisor.md)para que le ayude a migrar la tabla. De manera similar, el [Native Compilation Advisor](native-compilation-advisor.md) le permitirá convertir un procedimiento almacenado en un procedimiento almacenado compilado de forma nativa.  
  
 En este tema se explicará cómo:  
  
-   Configurar el almacén de datos de administración.  
  
-   Configurar la recopilación de datos.  
  
-   Generar informes de análisis del rendimiento de las transacciones para identificar las tablas y los procedimientos almacenados críticos para el rendimiento.  
  
 Para obtener más información sobre las metodologías de migración, vea [OLTP en memoria: patrones de carga de trabajo comunes y consideraciones sobre la migración](https://msdn.microsoft.com/library/dn673538.aspx).  
  
 El recopilador de rendimiento de las transacciones y los informes de análisis del rendimiento de las transacciones la ayudan a lograr las tareas siguientes:  
  
-   Analizar la carga de trabajo para determinar si OLTP en memoria mejorará el rendimiento. El recopilador de rendimiento de las transacciones recopila y evalúa las características de rendimiento de la carga de trabajo. . El informe de análisis del rendimiento de las transacciones recomienda entonces las tablas y los procedimientos almacenados que se beneficiarían de la conversión a OLTP en memoria.  
  
-   Le ayuda a planear y ejecutar la migración a OLTP en memoria. La migración de una tabla basada en disco a una tabla optimizada para memoria puede llevar mucho tiempo. El Asesor de optimización para memoria permite identificar las incompatibilidades que debe quitar de la tabla antes de migrar la tabla a OLTP en memoria. El Asesor de optimización para memoria permite también comprender el impacto que la migración de una tabla a una tabla optimizada para memoria tendrá sobre su aplicación.  
  
     Puede ver si la aplicación se beneficiaría de OLTP en memoria, si desea planear la migración a OLTP en memoria y siempre que migre algunas de sus tablas y procedimientos almacenados a OLTP en memoria.  
  
    > [!IMPORTANT]  
    >  El rendimiento de un sistema de base de datos depende de diversos de factores, no todos los cuales puede observar y medir el recopilador de rendimiento de las transacciones. Por consiguiente, el informe de análisis del rendimiento de las transacciones no garantiza que las mejoras reales en el rendimiento coincidirán con las predicciones, en el caso de que las haya.  
  
 El recopilador de rendimiento de las transacciones y la capacidad de generar un informe de análisis de rendimiento de las transacciones se instalan cuando se selecciona **herramientas de administración-básica** o **herramientas de administración-avanzadas** al instalar [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
## <a name="best-practices"></a>Procedimientos recomendados  
 El flujo de trabajo recomendado se muestra en el diagrama de flujo siguiente. Los nodos amarillos representan procedimientos opcionales:  
  
 ![Flujo de trabajo de AMR](../../database-engine/media/amr-1.gif "Flujo de trabajo de AMR")  
  
 Puede utilizar cualquier método para establecer una línea base de rendimiento, incluyendo pero sin limitarse al uso de registros de contador de rendimiento o del Monitor de actividad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La información que se utiliza en la línea base de rendimiento y las comparaciones son:  
  
-   Uso de CPU de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Consumo de memoria de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Actividad de E/S de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Rendimiento de la transacción de la instancia durante el procesamiento de transacciones.  
  
 El recopilador de rendimiento de las transacciones captura los datos cada 15 minutos. Para obtener resultados útiles, ejecute el recopilador de rendimiento de las transacciones al menos durante una hora. Para obtener los mejores resultados, ejecute el recopilador de rendimiento de las transacciones durante el tiempo necesario para capturar los datos para los escenarios principales. Genere un informe de análisis del rendimiento de las transacciones solo después de que termine de recopilar los datos.  
  
 Configure el recopilador de rendimiento de las transacciones para ejecutarlo en la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en producción y recopilar los datos en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el entorno de desarrollo (pruebas) para asegurar una sobrecarga mínima. Para obtener información sobre cómo guardar datos en una base de datos de almacén de administración [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de datos en una instancia remota, vea [configurar la recopilación de datos en una instancia de SQL Server remota](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md#xxx).  
  
## <a name="performance-impacts"></a>Impactos de rendimiento  
 El recopilador del rendimiento de las transacciones consta de dos conjuntos de recopilación de datos:  
  
-   Análisis de uso de tablas  
  
-   Análisis de procedimientos almacenados  
  
 Los conjuntos de recopilación recopilan los datos de tres vistas de administración dinámicas (DMV) cada quince minutos y cargan los datos en la base de datos configurada para actuar como almacén de administración de datos. La carga de los datos recopilados conlleva un impacto mínimo en el rendimiento.  
  
## <a name="use-the-transaction-performance-collector"></a>Usar el recopilador de rendimiento de las transacciones  
 Los pasos siguientes requieren [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
> [!IMPORTANT]  
>  No cambie el esquema (por ejemplo, no agregue ni quite bases de datos ni cree ni quite tablas) durante la generación de perfiles. Si cambia el esquema de una base de datos mientras está recopilando datos, la base de datos puede no incluirse de forma precisa en el informe.  
  
### <a name="configure-management-data-warehouse"></a>Configurar el almacén de administración de datos  
 El almacén de administración de datos se debe configurar para utilizar el recopilador de rendimiento de las transacciones.  
  
 La versión de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la que recopilará los datos (perfil) debe ser la misma o una más antigua que la de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] donde se ha configurado el almacén de administración de datos.  
  
1.  En el Explorador de objetos, expanda **Administración**.  
  
2.  Haga clic con el botón secundario en **recopilación de datos** y seleccione **tareas** y, después, **configurar almacén de administración de datos**. Se inicia el **Asistente para configurar el almacén de administración de datos** .  
  
3.  Haga clic en **siguiente** para seleccionar la base de datos que actuará como almacén de administración de datos.  
  
4.  Haga clic en **nuevo** para crear una nueva base de datos que contenga los datos del perfil. Cuando termine de crear la base de datos, haga clic en **siguiente** en el asistente.  
  
5.  En el paso siguiente del asistente podrá agregar usuarios e inicios de sesión. Puede asignar inicios de sesión a las pertenencias a roles para la instancia de MDW. No es necesario recopilar los datos de la instancia local. Si no va a recopilar datos de la instancia local, puede conceder la pertenencia al rol de base de datos `mdw_admin` a la cuenta que ejecutará las transacciones que se incluirán en el perfil. Cuando haya terminado, haga clic en **siguiente**.  
  
6.  Asegúrese de que el Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se esté ejecutando.  
  
7.  En la siguiente pantalla, haga clic en **Finalizar** para salir del asistente.  
  
### <a name="configure-data-collection-on-a-local-ssnoversion-instance"></a>Configurar la recopilación de datos en una instancia local de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 La recopilación de datos requiere que el Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esté iniciado. Solo es necesario configurar un recopilador de datos en un servidor.  
  
 Un recopilador de datos se puede configurar en un SQL Server 2012 o una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]versión posterior de.  
  
 Para configurar la recopilación de datos para cargar una base de datos del almacén de administración de datos en la misma instancia,  
  
1.  En **Explorador de objetos**, expanda **Administración**.  
  
2.  Haga clic con el botón derecho en **recopilación de datos**, seleccione **tareas**y, después, **Configure la recopilación de datos**. Se iniciará el **Asistente para configurar la recopilación de datos** .  
  
3.  Haga clic en **siguiente** para seleccionar la base de datos que recopilará los datos del perfil.  
  
4.  Seleccione la instancia actual de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y una base de datos del almacén de administración de datos en esa instancia.  
  
5.  En el cuadro con la etiqueta **seleccionar conjuntos de recopiladores de datos que desea habilitar**, seleccione **conjuntos de recopilación de rendimiento de transacciones**. Haga clic en **Siguiente** cuando termine.  
  
6.  Compruebe las selecciones. Haga clic en **atrás** para modificar la configuración. Haga clic **Finalizar** cuando haya terminado.  
  
###  <a name="configure-data-collection-on-a-remote-ssnoversion-instance"></a><a name="xxx"></a>Configurar la recopilación de datos en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] una instancia remota  
 La recopilación de datos requiere que se inicie el Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la instancia que recopilará los datos.  
  
 Un recopilador de datos se puede configurar en un SQL Server 2012 o una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]versión posterior de.  
  
 Necesita un proxy del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] establecido con la credencial correcta para que un recopilador de datos cargue los datos en una base de datos del almacén de administración de datos en una instancia distinta de aquella en la que se van a generar perfiles de las transacciones. Para habilitar un proxy del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], primero debe establecer una credencial con un inicio de sesión habilitado para dominio. El inicio de sesión habilitado para el dominio debe ser miembro del grupo `mdw_admin` para la base de datos del almacén de administración de datos. Consulte [Cómo: crear una credencial (SQL Server Management Studio)](../security/authentication-access/create-a-credential.md) para obtener información sobre cómo crear una credencial.  
  
 Para configurar la recopilación de datos para cargar una base de datos del almacén de administración de datos en otra instancia,  
  
1.  En la instancia que contiene los objetos basados en disco que desea migrar a OLTP en memoria, expanda el nodo **Administración** en explorador de objetos.  
  
2.  Haga clic con el botón derecho en **recopilación de datos** y seleccione **tareas** y, después, **configurar recopilación de datos**. Se iniciará el **Asistente para configurar la recopilación de datos** .  
  
3.  Haga clic en **siguiente** para seleccionar la base de datos que recopilará los datos del perfil.  
  
4.  Asegúrese de que existe una base de datos del almacén de administración de datos en la otra instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
5.  Seleccione otra instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y una base de datos del almacén de administración de datos en dicha instancia.  
  
     La versión de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la que recopilará los datos (perfil) debe ser la misma o una más antigua que la de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] donde se ha configurado el almacén de administración de datos.  
  
6.  En el cuadro con la etiqueta **seleccionar conjuntos de recopiladores de datos que desea habilitar**, seleccione **conjuntos de recopilación de rendimiento de transacciones**.  
  
7.  Seleccione **usar un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proxy del agente para cargas remotas**.  
  
8.  Haga clic en **Siguiente** cuando termine.  
  
9. Seleccione el proxy.  
  
     Si desea crear un nuevo proxy del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)],  
  
    1.  Haga clic en **nuevo** para abrir el cuadro de diálogo **nueva cuenta de proxy** .  
  
    2.  En el cuadro de diálogo **nueva cuenta de proxy** , escriba el nombre del proxy, seleccione la credencial y, si lo desea, escriba una descripción. A continuación, haga clic en **entidades**de seguridad.  
  
    3.  Haga clic en **Agregar** y seleccione rol **msdb** .  
  
    4.  Seleccione `dc_proxy` y haga clic en **Aceptar**. Haga clic en **Aceptar** de nuevo.  
  
     Una vez seleccionado el proxy correcto, haga clic en **siguiente**.  
  
10. Para configurar los conjuntos de recopilación del sistema, compruebe los **conjuntos de recopilación del sistema** y haga clic en **siguiente**.  
  
11. Compruebe las selecciones. Haga clic en **atrás** para modificar la configuración. Clicck **Finalizar** cuando haya terminado.  
  
 Los conjuntos de recopilación de datos deben estar configurados ahora y ejecutándose en la instancia.  
  
### <a name="generate-reports"></a>Generar informes  
 Puede generar informes de análisis de rendimiento de transacciones haciendo clic con el botón secundario en la base de datos del almacén de administración de datos y seleccionando **informes**, **almacén de administración de datos**y, a continuación, **información general de análisis de rendimiento de transacciones**.  
  
 El informe recopila información sobre todas las bases de datos de usuario en el servidor de la carga de trabajo. Si la base de datos del almacén de administración de datos (MDW) se encuentra en el equipo local, verá las bases de datos MDW en el informe.  
  
 Un procedimiento almacenado con un proporción alta de tiempo de CPU/tiempo transcurrido es un candidato a la migración. El informe muestra todas las referencias de tabla, ya que los procedimientos almacenados compilados de forma nativa solo pueden hacer referencia a tablas optimizadas para memoria, que pueden incrementar el costo de la migración.  
  
 El informe de detalles de una tabla consta de tres secciones:  
  
-   Sección de estadísticas de recorrido  
  
     Esta sección incluye una única tabla que muestra las estadísticas recopiladas acerca de los recorridos en la tabla de base de datos. Las columnas son:  
  
    -   Porcentaje de accesos en total. El porcentaje de recorridos y de búsquedas en esta tabla con respecto a la actividad de toda la base de datos. Cuanto mayor sea el porcentaje, más se usa la tabla en comparación con otras de la base de datos.  
  
    -   Estadísticas de búsqueda y de recorrido de intervalos. Esta columna registra el número de búsquedas de puntos y de recorridos de intervalo (recorridos de índice y recorridos de tabla) realizados en la tabla durante la generación de perfiles. El promedio por transacción es una estimación.  
  
    -   Mejora de la interoperabilidad y mejora nativa. Estas columnas estiman el grado de mejora en el rendimiento que tendrían una búsqueda o un recorrido de intervalo si la tabla se convirtiera en una tabla optimizada para memoria.  
  
-   Sección de estadísticas de contención  
  
     Esta sección incluye una tabla que muestra la contención en la tabla de base de datos. Para obtener más información sobre bloqueos y bloqueos temporales de base de datos, consulte [arquitectura de bloqueo](https://msdn.microsoft.com/library/aa224738\(v=sql.80\).aspx). Estas son sus columnas:  
  
    -   Porcentaje de esperas en total. El porcentaje de esperas por bloqueos y bloqueos temporales en esta tabla de base de datos en comparación con la actividad de la base de datos. Cuanto mayor sea el porcentaje, más se usa la tabla en comparación con otras de la base de datos.  
  
    -   Estadísticas de bloqueos temporales. Estas columnas registran el número de esperas por bloqueos temporales para las consultas que implican a esta tabla. Para obtener información acerca de los bloqueos temporales, consulte [bloqueo temporal](https://msdn.microsoft.com/library/aa224727\(v=SQL.80\).aspx). Cuanto mayor sea este número, más contención por bloqueos temporales hay en la tabla.  
  
    -   Estadísticas de bloqueos. Este grupo de columnas registra el número de esperas y de adquisiciones de bloqueos de página para las consultas de esta tabla. Para obtener más información sobre los bloqueos, vea [Descripción del bloqueo en SQL Server](https://msdn.microsoft.com/library/aa213039\(v=SQL.80\).aspx). Cuantas más esperas hay, más contención por bloqueos se producen en la tabla.  
  
-   Sección de dificultades de migración  
  
     Esta sección incluye una tabla que muestra las dificultades de convertir esta tabla de base de datos en una tabla optimizada para memoria. Una clasificación de mayor dificultad indica que convertir la tabla es más difícil. Para ver los detalles para convertir esta tabla de base de datos, use el [Asesor de optimización de memoria](memory-optimization-advisor.md).  
  
 Las estadísticas de análisis y contención en el informe de detalles de la tabla se recopilan y se agregan desde [Sys. dm_db_index_operational_stats &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql).  
  
 El informe de detalles de un procedimiento almacenado consta de dos secciones:  
  
-   Sección de estadísticas de ejecución  
  
     Esta sección incluye una tabla en la que se muestran las estadísticas recopiladas sobre las ejecuciones del procedimiento almacenado. Estas son sus columnas:  
  
    -   Tiempo en caché. El tiempo que se almacena en caché este plan de ejecución. Si el procedimiento almacenado se sale de la memoria caché de planes y vuelve a entrar, habrá datos para cada caché.  
  
    -   Tiempo total de CPU. El tiempo total de CPU que el procedimiento almacenado usó durante la generación de perfiles. Cuanto mayor es este número, más CPU usó el procedimiento almacenado.  
  
    -   Tiempo total de ejecución. El tiempo total de ejecución que el procedimiento almacenado usó durante la generación de perfiles. Cuanto más alta es la diferencia entre este número y el tiempo de CPU, menos eficiente es el procedimiento almacenado en el uso de la CPU.  
  
    -   Total de errores de caché. El número de errores de caché (lecturas del almacenamiento físico) que se debe a las ejecuciones del procedimiento almacenado durante la generación de perfiles.  
  
    -   Recuento de ejecución. El número de veces que este procedimiento almacenado se ha ejecutado durante la generación de perfiles.  
  
-   Sección de referencias de tabla  
  
     Esta sección incluye una tabla que muestra las tablas a las que este procedimiento almacenado hace referencia. Antes de convertir el procedimiento almacenado en un procedimiento almacenado compilado de forma nativa, todas estas tablas deben convertirse en tablas optimizadas para memoria y deben permanecer en el mismo servidor y base de datos.  
  
 Las estadísticas de ejecución del informe de detalles del procedimiento almacenado se recopilan y se agregan desde [Sys. dm_exec_procedure_stats &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql). Las referencias se obtienen de [Sys. sql_expression_dependencies &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql).  
  
 Para ver detalles sobre cómo convertir un procedimiento almacenado en un procedimiento almacenado compilado de forma nativa, use el [Asistente de compilación nativa](native-compilation-advisor.md).  
  
## <a name="see-also"></a>Consulte también  
 [Migrar a OLTP en memoria](migrating-to-in-memory-oltp.md)  
  
  
