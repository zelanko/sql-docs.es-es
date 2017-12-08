---
title: El Comprobador de coherencia (DBCC) para Analysis Services de la base de datos | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 28714c32-718f-4f31-a597-b3289b04b864
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9dee0f68a2d9b4dd1bdae90435de3c02eddfeba2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="database-consistency-checker-dbcc-for-analysis-services"></a>Comprobador de coherencia de base de datos (DBCC) para Analysis Services
  DBCC proporciona validación de base de datos a petición para bases de datos multidimensionales y tabulares en una instancia de Analysis Services. Puede ejecutar DBCC en una ventana de consulta XMLA o MDX en SQL Server Management Studio (SSMS) y realizar el seguimiento de la salida de DBCC en SQL Server Profiler o sesiones xEvent en SSMS.  
El comando toma una definición de objeto y devuelve un conjunto de resultados vacío o la información detallada del error si el objeto está dañado.   En este artículo, aprenderá a ejecutar el comando, interpretar los resultados y solucionar los problemas que surjan.  
  
 En el caso de las bases de datos tabulares, las comprobaciones de coherencia realizadas por DBCC equivalen a la validación integrada que se produce automáticamente cada vez que se vuelve a cargar, se sincroniza o se restaura una base de datos.  En cambio, las comprobaciones de coherencia de bases de datos multidimensionales se producen solo al ejecutar DBCC a petición.  
  
 El intervalo de comprobaciones de validación varía según el modo, ya que las bases de datos tabulares están sujetas a una gama más amplia de comprobaciones.  
 Las características de una carga de trabajo de DBCC también varían según el modo de servidor. Las operaciones de comprobación en bases de datos multidimensionales incluyen la lectura de datos desde el disco, la creación de índices temporales para comparar con los índices reales, etc. En todo caso, son procesos que tardan mucho en completarse.  
  
 La sintaxis de comando para DBCC utiliza los metadatos de objetos específicos del tipo de base de datos que se va a comprobar:  
  
-   Las bases de datos multidimensionales y tabulares anteriores a SQL Server 2016 de nivel de compatibilidad 1100 o 1103 se describen en estructuras de modelado multidimensional como **cubeID**, **measuregroupID**y **partitionID**.  
  
-   Metadatos de las nuevas bases de datos de modelo Tabular en el nivel de compatibilidad 1200 y superior constan de descriptores como **TableName** y **PartitionName**.  
  
 DBCC para Analysis Services se ejecutará en cualquier base de datos de Analysis Services en cualquier nivel de compatibilidad, siempre que la base de datos se ejecute en una instancia de SQL Server 2016. Asegúrese de que está utilizando la sintaxis de comando correcta para cada tipo de base de datos.  
  
> [!NOTE]  
>  Si está familiarizado con [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md), pronto se dará cuenta de que DBCC en Analysis Services tiene un ámbito mucho más restringido. DBCC en Analysis Services es un comando único que notifica exclusivamente los datos dañados en la base de datos o en objetos individuales. Si tiene otras tareas en mente, como la recopilación de información, pruebe a usar los scripts de PowerShell de AMO o XMLA en su lugar. Consulte [Monitor an Analysis Services Instance](../../analysis-services/instances/monitor-an-analysis-services-instance.md) para obtener vínculos que amplíen la información.  
  
## <a name="permission-requirements"></a>Requisitos de permisos  
 Debe ser administrador de servidor o base de datos de Analysis Services (un miembro del rol de servidor) para ejecutar el comando. Para tener instrucciones, vea [Otorgar permisos de base de datos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) o [Conceder permisos de administrador de servidor (Analysis Services)](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
## <a name="command-syntax"></a>Sintaxis del comando 
 Bases de datos tabulares 1200 y niveles de compatibilidad más altos utilizan metadatos tabulares para definiciones de objeto. En el ejemplo siguiente, se muestra la sintaxis completa de DBCC para una base de datos tabular creada en un nivel funcional de SQL Server 2016.  
  
 Las principales diferencias entre las dos sintaxis incluyen un espacio de nombres más reciente de XMLA, ya no \<objeto > elemento y no \<modelo > elemento (hay solo un modelo por base de datos).  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2014/engine">  
     <DatabaseID>MyTabular1200DB_7811b5d8-c407-4203-8793-12e16c3d1b9b</DatabaseID>  
     <TableName>FactSales</TableName>  
     <PartitionName>FactSales 4</PartitionName>  
</DBCC>  
```  
  
 Puede omitir los objetos de nivel inferior, como los nombres de tabla o partición, para comprobar todo el esquema.  
  
 Puede obtener los nombres de objeto y los identificadores DatabaseID desde Management Studio, a través de la página de propiedades de cada objeto.  
  
## <a name="command-syntax-for-multidimensional-and-tabular-110x-databases"></a>Sintaxis del comando para bases de datos multidimensionales y tabulares 110x  
 DBCC utiliza una sintaxis idéntica para las bases de datos multidimensionales y tabulares 1100 y 1103. Puede ejecutar DBCC en objetos de base de datos específicos, incluida la base de datos completa. Para más información sobre la definición de objetos, vea [Elemento de objeto &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md).  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2006</PartitionID>  
     </Object>  
</DBCC>  
  
```  
  
 Para ejecutar DBCC en objetos en posiciones superiores de la cadena de objetos, elimine los elementos de identificador de objeto de nivel inferior que no sean necesarios:  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
     </Object>  
</DBCC>  
  
```  
  
 En el caso de las bases de datos tabulares 110x, la sintaxis de definición de objeto se modela después de la sintaxis del comando de proceso (específicamente, en el modo en que las tablas se asignan a las dimensiones y los grupos de medida).  
  
-   **CubeID** se asigna al identificador de modelo, que es **Model**.  
  
-   **MeasureGroupID** se asigna a un identificador de tabla.  
  
-   **PartitionID** se asigna a un identificador de partición.  
  
## <a name="usage"></a>Uso  
 En SQL Server Management Studio, puede invocar DBCC mediante la ventana de consulta MDX o XMLA. Además, puede utilizar tanto [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Profiler como xEvents de Analysis Services para ver el resultado de DBCC. Tenga en cuenta que los mensajes de DBCC de SSAS no se notifican al registro de eventos de la aplicación Windows o al archivo msmdsrv.log.  
  
 DBCC comprueba si hay daños en los datos físicos, así como los daños en los datos lógicos que se producen cuando hay miembros huérfanos en un segmento. Para poder ejecutar DBCC es necesario procesar antes una base de datos. Este proceso omite las particiones remotas, vacías o sin procesar.  
  
 El comando se ejecuta en una transacción de lectura y, por tanto, puede ser expulsado por el tiempo de espera para forzar confirmación. Las comprobaciones de la partición se ejecutan en paralelo.  
  
 Es posible que se requiera un reinicio del servicio para reflejar los errores por daños que se hayan producido desde el último reinicio del servicio. La reconexión del servidor no es suficiente para recoger los cambios.  
  
### <a name="run-dbcc-commands-in-management-studio"></a>Ejecución de los comandos DBCC en Management Studio  
 Para consultas ad hoc, abra una ventana de consulta XMLA o MDX en SQL Server Management Studio. Para hacerlo, haga clic con el botón derecho en la base de datos | **Nueva consulta** | **XMLA**para ejecutar el comando y leer la salida.  
  
 ![Comando DBCC XML en Management Studio](../../analysis-services/instances/media/ssas-dbcc-ssms.gif "comando DBCC XML en Management Studio")  
  
 La pestaña Resultados mostrará un conjunto de resultados vacío (como se muestra en la captura de pantalla) si no se detectó ningún problema.  
  
 La pestaña Mensajes proporciona información detallada, pero no siempre es confiable para las bases de datos más pequeñas. Los mensajes de estado a veces se recortan, indicando que el comando se completó, pero sin los mensajes de comprobación de estado de cada objeto. Un informe de mensaje típico puede ser similar al que se muestra a continuación.  
  
 **Mensajes notificados desde DBCC para la comprobación de validación de cubo**  
  
```  
Executing the query ...  
READS, 0  
READ_KB, 0  
WRITES, 0  
WRITE_KB, 0  
CPU_TIME_MS, 0  
ROWS_SCANNED, 0  
ROWS_RETURNED, 0  
  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
<Object>  
<DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
<CubeID>Adventure Works</CubeID>  
</Object>  
</DBCC>  
Started checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2012' partition.  
Finished checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2013' partition.  
Finished checking segment indexes for the 'Internet_Sales_2012' partition.  
Started checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2011' partition.  
Finished checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2012' partition.  
Started checking segment indexes for the 'Internet_Orders_2013' partition.  
Finished checking segment indexes for the 'Internet_Orders_2012' partition.  
...   
Run complete  
  
```  
  
 **Resultado al ejecutar DBCC en una versión anterior de Analysis Services**  
  
 DBCC solo se admite en bases de datos que se ejecutan en una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Si ejecuta el comando en sistemas más antiguos, se devolverá este error.  
  
```  
Executing the query ...  
The DBCC element at line 7, column 87 (namespace http://schemas.microsoft.com/analysisservices/2003/engine) cannot appear under Envelope/Body/Execute/Command.  
Execution complete  
  
```  
  
### <a name="trace-dbcc-output-in-sql-server-profiler-2016"></a>Seguimiento del resultado de DBCC en SQL Server Profiler 2016  
 Puede ver el resultado de DBCC en un seguimiento de Profiler que incluye los eventos de Progress Reports (Progress Report Begin, Progress Report Current, Progress Report End y Progress Report Error).  
  
1.  Inicie un seguimiento Consulte [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md) para obtener ayuda acerca de cómo usar SQL Server Profiler con Analysis Services.  
  
2.  Elija **Command Begin** y **Command End** y alguno de los eventos de **Progress Report** , o todos ellos.  
  
3.  Ejecute el comando DBCC en Management Studio en una ventana de consulta XMLA o MDX, utilizando la sintaxis proporcionada en una sección anterior.  
  
4.  En SQL Server Profiler, la actividad de DBCC se indica mediante eventos **Command** con una subclase de eventos de DBCC:  
  
     ![SSAS-dbcc-generador de perfiles-eventsubclass](../../analysis-services/instances/media/ssas-dbcc-profiler-eventsubclass.PNG "eventsubclass-ssas-dbcc-generador de perfiles")  
  
     El código de evento 32 es la ejecución de DBCC.  
  
     El código de evento 64 es un informe de progreso de DBCC sobre objetos individuales.  
  
     El código de evento 63 es una comprobación de segmento para objetos multidimensionales.  
  
     Para ambas subclases de evento, revise los valores **TextData** para los mensajes devueltos por DBCC.  
  
     Mensajes de estado empiezan con "Comprobando la coherencia de \<objeto >", "ha iniciado la comprobación \<objeto >", o "ha finalizado la comprobación \<objeto >".  
  
    > [!NOTE]  
    >  En CTP 3.0, los objetos se identifican por nombres internos. Por ejemplo, una jerarquía de categorías se articula como H$ Categories -\<objectID >. Los nombres internos deben reemplazarse por nombres descriptivos en una próxima versión de CTP.  
  
     Los mensajes de error se enumeran más adelante.  
  
### <a name="trace-dbcc-output-in-an-xevent-session-in-ssms"></a>Seguimiento de resultados de DBCC en una sesión de xEvent en SSMS  
 Las sesiones de eventos extendidos pueden usar eventos del generador de perfiles o xEvents. Consulte la sección anterior para obtener instrucciones sobre cómo agregar eventos **Command** y **Progress Report** .  
  
1.  Para iniciar sesión, haga clic con el botón derecho en una base de datos > **Administración** >**Eventos extendidos** >  **Sesiones** > **Nueva sesión**. Consulte  [Monitor Analysis Services with SQL Server Extended Events](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) para obtener más información.  
  
2.  Elija alguno o todos los eventos de **Progress Report** para la categoría de eventos Profiler o los eventos de **RequestProgress** para la categoría PureXevent.  
  
3.  Ejecute el comando DBCC en Management Studio en una ventana de consulta XMLA o MDX, utilizando la sintaxis proporcionada en una sección anterior.  
  
4.  En SSMS, actualice la carpeta de sesiones. Haga clic con el botón derecho en el nombre de sesión > **Observar datos en directo**.  
  
5.  Revise los valores de TextData para los mensajes devueltos por DBCC.  TextData es una propiedad de un campo de evento y muestra los mensajes de estado y de error devueltos por el evento.  
  
     Mensajes de estado empiezan con "Comprobando la coherencia de \<objeto >", "ha iniciado la comprobación \<objeto >", o "ha finalizado la comprobación \<objeto >".  
  
     Los mensajes de error se enumeran más adelante.  
  
## <a name="reference-consistency-checks-and-errors-for-multidimensional-databases"></a>Referencia: comprobaciones de coherencia y errores para bases de datos multidimensionales  
 En el caso de las bases de datos multidimensionales, se validan solo los índices de partición.  Durante la ejecución, DBCC crea un índice temporal para cada partición y lo compara con el índice almacenado en disco.  La creación de un índice temporal requiere la lectura de todos los datos de la partición del disco y, a continuación, su mantenimiento en el índice temporal de la memoria con fines de comparación. Dada la carga de trabajo adicional, el servidor puede experimentar un importante consumo de memoria y E/S del disco durante una ejecución de DBCC.  
  
 La detección de daños del índice multidimensional incluye las siguientes comprobaciones. Los errores en esta tabla aparecen en seguimientos de errores de xEvent o Profiler a nivel de objeto.  
  
||||  
|-|-|-|  
|**Objeto**|**Descripción de la comprobación de DBCC**|**Motivo del error**|  
|Índice de partición|Comprueba los índices y estadísticas del segmento.<br /><br /> Compara el identificador de cada miembro del índice de la partición temporal con las estadísticas de partición almacenadas en disco.  Si un miembro se encuentra en el índice temporal con un valor de identificador de datos fuera del intervalo almacenado para las estadísticas del índice de partición en el disco, se considera que las estadísticas para el índice están dañadas.|Las estadísticas del segmento de partición están dañadas.|  
|Índice de partición|Valida los metadatos.<br /><br /> Comprueba que cada miembro del índice temporal puede encontrarse en el archivo de encabezado de índice para el segmento en el disco.|El segmento de partición está dañado.|  
|Índice de partición|Analiza segmentos para buscar daños físicos.<br /><br /> Lee el archivo de índice en el disco para cada miembro del índice temporal y comprueba que el tamaño del los registros del índice coinciden, y que se marcan las mismas páginas de datos como contenedoras de registros para el miembro actual.|El segmento de partición está dañado.|  
  
## <a name="reference-consistency-checks-and-errors-for-tabular-databases"></a>Referencia: comprobaciones de coherencia y errores para bases de datos tabulares  
 La tabla siguiente enumera todas las comprobaciones de coherencia realizadas en objetos tabulares, junto con los errores que se producen si la comprobación indica daños. Los errores en esta tabla aparecen en seguimientos de errores de xEvent o Profiler a nivel de objeto.  
  
||||  
|-|-|-|  
|**Objeto**|**Descripción de la comprobación de DBCC**|**Motivo del error**|  
|Base de datos|Comprueba la cantidad de tablas de la base de datos.  Un valor inferior a cero indica daños.|Hay daños en la capa de almacenamiento. La colección de tablas de la base de datos '%{parent/}' está dañada.|  
|Base de datos|Comprueba la estructura interna que se utiliza para realizar un seguimiento de la integridad referencial y genera un error si el tamaño es incorrecto.|Los archivos de base de datos no superaron las comprobaciones de coherencia.|  
|Table|Comprueba el valor interno que se usa para determinar si la tabla es una tabla de dimensiones o hechos.  Un valor que quede fuera del intervalo conocido indica daños.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar las estadísticas de la tabla.|  
|Table|Comprueba si el número de particiones en la asignación de segmentos de la tabla coincide con el número de particiones definidas para la tabla.|Hay daños en la capa de almacenamiento. La colección de particiones de la tabla '%{parent/}' está dañada.|  
|Table|Si se creó o se importó una base de datos tabular se creó o importados desde PowerPivot para Excel 2010 y tiene un número de particiones superior a uno, se generará un error, ya que la compatibilidad con las particiones se agregó en una etapa posterior y esto indicaría daños.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar la asignación de segmentos.|  
|Partición|Comprueba en cada partición que el número de segmentos de datos y la cantidad de registros de cada segmento de datos en el segmento coincide con los valores almacenados en el índice para el segmento.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar la asignación de segmentos.|  
|Partición|Genera un error si el número total de registros, segmentos o registros por segmento no es válido (inferior a cero), o si el número de segmentos no coincide con el número calculado de segmentos requeridos en función del número total de registros.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar la asignación de segmentos.|  
|Relación|Genera un error si la estructura que se utiliza para almacenar datos acerca de la relación no contiene registros o si el nombre de la tabla utilizada en la relación está vacío.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar las relaciones.|  
|Relación|Comprueba que el nombre de la tabla principal, la columna principal, la tabla externa y la columna externa están configurados y que es posible acceder a las columnas y las tablas que participan en la relación.<br /><br /> Comprueba que los tipos de columna implicados son válidos y que el índice de valores de Clave principal-Clave externa resulta en una estructura de consulta válida.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar las relaciones.|  
|Jerarquía|Genera un error si el criterio de ordenación para la jerarquía no es un valor reconocido.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar la jerarquía '%{hier/}'.|  
|Jerarquía|Las comprobaciones realizadas en la jerarquía dependen del tipo interno de asignación de jerarquía utilizado.<br /><br /> Todas las jerarquías se comprueban para verificar el estado de procesado correcto, que el almacén de jerarquía existe y que, cuando sea aplicable, existen las estructuras de datos utilizadas para una conversión de identificador de datos a posición de jerarquía.<br /><br /> Suponiendo que todas las comprobaciones sean correctas, se recorre la estructura de la jerarquía para comprobar que cada posición en la jerarquía señala al miembro correcto.<br />Si se produce un error en cualquiera de estas pruebas, se genera un error.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar la jerarquía '%{hier/}'.|  
|Jerarquía definida por el usuario|Comprueba que están configurados los nombres de nivel de jerarquía.<br /><br /> Si se ha procesado la jerarquía, comprueba que el almacén de datos de jerarquía interna tiene el formato correcto.  Comprueba que el almacén interno de jerarquía no contiene valores de datos no válidos.<br /><br /> Si la jerarquía está marcada como sin procesar, confirma que este estado se aplica a las estructuras de datos anteriores y que todos los niveles de la jerarquía se marcan como vacíos.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar la jerarquía '%{hier/}'.|  
|Columna|Genera un error si no se establece la codificación utilizada para la columna en un valor conocido.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar las estadísticas de la columna.|  
|Columna|Comprueba si la columna se comprimió por el motor incorporado en la memoria o no.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar las estadísticas de la columna.|  
|Columna|Comprueba el tipo de compresión de la columna para valores conocidos.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar las estadísticas de la columna.|  
|Columna|Cuando la columna "tokenization" no se establece en un valor conocido, se genera un error.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar las estadísticas de la columna.|  
|Columna|Si el intervalo de identificadores almacenados para un diccionario de datos de columnas no coincide con el número de valores en el diccionario de datos o está fuera del intervalo permitido, se producirá un error.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar el diccionario de datos.|  
|Columna|Comprueba que el número de segmentos de datos para una columna coincide con el número de segmentos de datos para la tabla a la que pertenece.|Hay daños en la capa de almacenamiento. La colección de segmentos en la columna '%{parent/}' está dañada.|  
|Columna|Comprueba que el número de particiones de una columna de datos coincide con el número de particiones para la asignación de segmentos de datos para la columna.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar la asignación de segmentos.|  
|Columna|Comprueba que el número de registros en un segmento de columna coincide con el número de registros almacenados en el índice para ese segmento de columna.|Hay daños en la capa de almacenamiento. La colección de segmentos en la columna '%{parent/}' está dañada.|  
|Columna|Si una columna no tiene estadísticas del segmento, se producirá un error.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar las estadísticas del segmento.|  
|Columna|Si una columna no tiene información de compresión o almacenamiento de segmento, se producirá un error.|Los archivos de base de datos no superaron las comprobaciones de coherencia.|  
|Columna|Notifica un error si las estadísticas de segmento para una columna no coinciden con los valores de columna reales para el identificador de datos mínimo, el identificador de datos máximo, el número de valores distintos, el número de filas o la presencia de valores NULL.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar las estadísticas del segmento.|  
|ColumnSegment|Si el identificador de datos mínimo o el identificador de datos máximo es inferior al valor reservado del sistema para NULL, marque la información de segmento de la columna como dañado.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar las estadísticas del segmento.|  
|ColumnSegment|Si no hay ninguna fila para este segmento, los valores de datos mínimo y máximo para la columna deben establecerse en el valor reservado del sistema para NULL.  Si el valor no es NULL, se producirá un error.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar las estadísticas del segmento.|  
|ColumnSegment|Si la columna tiene filas y al menos un valor distinto de NULL, comprueba que el identificador de datos mínimo y máximo para la columna es mayor que el valor reservado para el sistema para NULL.|Error en las comprobaciones de coherencia de la base de datos (DBCC) al comprobar las estadísticas del segmento.|  
|Interno|Comprueba que está configurada la sugerencia de tokenización de almacén y que, si el almacén se procesa, hay punteros válidos para las tablas internas.  Si el almacén no se procesa, comprueba que todos los punteros son nulos.<br />De lo contrario, devuelve un error genérico de DBCC.|Los archivos de base de datos no superaron las comprobaciones de coherencia.|  
|Base de datos DBCC|Genera un error si el esquema de base de datos no tiene tablas o no se puede tener acceso a una o varias tablas.|Hay daños en la capa de almacenamiento. La colección de tablas de la base de datos '%{parent/}' está dañada.|  
|Base de datos DBCC|Genera un error si una tabla está marcada como temporal o tiene un tipo desconocido.|Se ha encontrado un tipo de tabla incorrecto.|  
|Base de datos DBCC|Genera un error si el número de relaciones de una tabla tiene un valor negativo, o si una tabla tiene definida una relación y no se encuentra una estructura de relación correspondiente.|Hay daños en la capa de almacenamiento. La colección de relaciones en la tabla '%{parent/}' está dañada.|  
|Base de datos DBCC|Si el nivel de compatibilidad para la base de datos es 1050 (SQL Server 2008 R2/PowerPivot v1.0) y el número de relaciones supera el número de tablas en el modelo, marca la base de datos como dañada.|Los archivos de base de datos no superaron las comprobaciones de coherencia.|  
|Tabla DBCC|Para la tabla en la validación, comprueba si el número de columnas es inferior a cero y genera un error si es así.  También se produce un error si el almacén de columnas para una columna de la tabla es NULL.|Hay daños en la capa de almacenamiento. La colección de columnas de la tabla '%{parent/}' está dañada.|  
|Partición DBCC|Comprueba la tabla a la que pertenece la partición que se valida, y si el número de columnas de la tabla es inferior a cero, indica que la colección de columnas se ha dañado para la tabla. También se producirá un error si el almacén de columnas para una columna de la tabla es NULL.|Hay daños en la capa de almacenamiento. La colección de columnas de la tabla '%{parent/}' está dañada.|  
|Partición DBCC|Itera por cada columna de la partición seleccionada y comprueba que cada segmento de la partición tiene un vínculo válido a una estructura de segmento de columna.  Si algún segmento tiene un vínculo NULL, la partición se considera dañada.|Hay daños en la capa de almacenamiento. La colección de segmentos en la columna '%{parent/}' está dañada.|  
|Columna|Devuelve un error si el tipo de columna no es válido.|Se ha encontrado un tipo de segmento incorrecto.|  
|Columna|Devuelve un error si alguna columna tiene una cantidad negativa para el número de segmentos de una columna, o si el puntero a la estructura de segmentos de las columnas para un segmento tiene un vínculo NULL.|Hay daños en la capa de almacenamiento. La colección de segmentos en la columna '%{parent/}' está dañada.|  
|Comando DBCC|El comando DBCC notificará varios mensajes de estado mientras pasa a través de la operación de DBCC.  Emitirá un mensaje de estado antes de iniciar que incluye el nombre de la base de datos, la tabla o la columna del objeto, y otro después de finalizar cada comprobación de los objetos.|Comprobando la coherencia de la \<objectname > \<objecttype >. Fase: comprobación previa.<br /><br /> Comprobando la coherencia de la \<objectname > \<objecttype >. Fase: comprobación posterior.|  
  
## <a name="common-resolutions-for-error-conditions"></a>Soluciones habituales de las condiciones de error  
 Los errores siguientes aparecerán en SQL Server Management Studio o en archivos de msmdsrv.log. Estos errores aparecen cuando una o varias comprobaciones no se completan correctamente. Dependiendo del error, la solución recomendada es volver a procesar un objeto, eliminar y volver a implementar una solución o restaurar la base de datos.  
  
|Error|Problema|Solución|  
|-----------|-----------|----------------|  
|**Errores del administrador de metadatos.**<br /><br /> La referencia al objeto '\<objectID >' no es válido. No coincide con la estructura de la jerarquía de clases de metadatos.|comando incorrecto|Compruebe la sintaxis del comando. Lo más probable es que haya incluido un objeto de nivel inferior sin especificar uno o varios de sus objetos primarios.|  
|**Errores del administrador de metadatos.**<br /><br /> Ya sea la \<objeto > con el Id. de '\<objectID >' no existe en el \<parentobject > con el Id. de '\<parentobjectID >', o el usuario no tiene permisos para tener acceso al objeto.|Daños en el índice (multidimensional)|Vuelva a procesar el objeto y los objetos dependientes.|  
|**Error durante la comprobación de coherencia de la partición**<br /><br /> Se produjo un error al comprobar la coherencia de la \<nombre de partición > partición de la \<nombre del grupo de medida > grupo de medida para el \<nombre del cubo > cubo desde el \<nombre de base de datos > base de datos. Vuelva a procesar la partición o los índices para corregir los daños.|Daños en el índice (multidimensional)|Vuelva a procesar el objeto y los objetos dependientes.|  
|**Daños en las estadísticas del segmento de la partición**|Daños en el índice (multidimensional)|Vuelva a procesar el objeto y los objetos dependientes.|  
|**El segmento de partición está dañado.**|Daños en los metadatos (tipo multidimensional o tabular)|Elimine y vuelva a implementar el proyecto, o restaure una copia de seguridad y procese de nuevo.<br /><br /> Para obtener instrucciones, vea la entrada de blog [How to handle corruption in Analysis Services databases (blog)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Reparar bases de datos dañadas de Analysis Services).|  
|**Daños en los metadatos de una tabla**<br /><br /> Tabla \<nombre de tabla > archivo de metadatos está dañado. La tabla principal no se encuentra en el nodo DataFileList.|Daños en los metadatos (solo en tipo tabular)|Elimine y vuelva a implementar el proyecto, o restaure una copia de seguridad y procese de nuevo.<br /><br /> Para obtener instrucciones, vea la entrada de blog [How to handle corruption in Analysis Services databases (blog)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Reparar bases de datos dañadas de Analysis Services).|  
|**Daños en la capa de almacenamiento**<br /><br /> Daños en la capa de almacenamiento: colección de \<nombre de tipo > en \<primario-name > \<tipo-primario > está dañado.|Daños en los metadatos (solo en tipo tabular)|Elimine y vuelva a implementar el proyecto, o restaure una copia de seguridad y procese de nuevo.<br /><br /> Para obtener instrucciones, vea la entrada de blog [How to handle corruption in Analysis Services databases (blog)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Reparar bases de datos dañadas de Analysis Services).|  
|**Falta tabla del sistema**<br /><br /> Tabla del sistema \<nombre de tabla > falta.|Daños en objeto (solo en tipo tabular)|Vuelva a procesar el objeto y los objetos dependientes.|  
|**Daños en las estadísticas de la tabla**<br /><br /> Las estadísticas de la tabla de sistema \<nombre de tabla > falta.|Daños en los metadatos (solo en tipo tabular)|Elimine y vuelva a implementar el proyecto, o restaure una copia de seguridad y procese de nuevo.<br /><br /> Para obtener instrucciones, vea la entrada de blog [How to handle corruption in Analysis Services databases (blog)](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Reparar bases de datos dañadas de Analysis Services).|  
  
## <a name="disable-automatic-consistency-checks-on-database-load-operations-through--the-msmdsrvini-configuration-file"></a>Deshabilite las comprobaciones de coherencia automáticas en las operaciones de carga de base de datos a través del archivo de configuración msmdsrv.ini.  
 Aunque no es recomendable, puede deshabilitar las comprobaciones de coherencia de la base de datos integradas que se producen automáticamente en los eventos de carga de la base de datos (solo en bases de datos tabulares). Para ello, tiene que modificar una opción de configuración en el archivo msmdsrv.ini:  
  
```  
<ConfigurationSettings>  
     <Vertipaq />  
          <DisableConsistencyChecks />  
```  
  
 Esta configuración no está presente en el archivo de configuración y debe agregarse manualmente.  
  
 Los valores válidos son los siguientes:  
  
-   **-2** (predeterminado) DBCC está habilitado. Si el servidor puede resolver de forma lógica el error con un alto grado de certeza, se aplicará automáticamente una corrección. De lo contrario, se registrará un error.  
  
-   **-1** DBCC está habilitado parcialmente. Está habilitado para RESTORE y en las validaciones previas a la confirmación que comprueban el estado de la base de datos al final de una transacción.  
  
-   **0** DBCC está habilitado parcialmente. Se realizan comprobaciones de coherencia de la base de datos durante las operaciones RESTORE, IMAGELOAD, LOCALCUBELOAD y ATTACH  
         .  
  
-   **1** DBCC está deshabilitado. Las comprobaciones de integridad de los datos están deshabilitadas; sin embargo, se llevarán a cabo comprobaciones de deserialización.  
  
> [!NOTE]  
>  Este valor no influye en DBCC cuando ejecute el comando a petición.  
  
## <a name="see-also"></a>Vea también  
 [Procesar base de datos, tabla o partición &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)   
 [Procesar un modelo multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Supervisar una instancia de Analysis Services](../../analysis-services/instances/monitor-an-analysis-services-instance.md)   
 [Nivel de compatibilidad para modelos tabulares de Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Propiedades del servidor de Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)  
  
  
