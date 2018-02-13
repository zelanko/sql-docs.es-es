---
title: "Notas de la versión de SQL Server 2014 | Microsoft Docs"
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.technology: server-general
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf4c4922-80b3-4be3-bf71-228247f97004
caps.latest.revision: 
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4bbb387c935dc07e467125921ef11986ea004c21
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2018
---
# <a name="sql-server-2014-release-notes"></a>SQL Server 2014 Release Notes
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]
Este documento de notas de la versión describe problemas conocidos que es conveniente que conozca antes de instalar o antes de solucionar problemas de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
## <a name="top"></a>Contenido  
[1.0 Antes de la instalación](#BeforeInstall)  
  
[2.0 Documentación del producto](#ProdDoc)  
  
[3.0 Motor de base de datos](#DBEngine)  
  
[4.0 Reporting Services](#SSRS)  
  
[5.0 SQL Server 2014 en máquinas virtuales de Windows Azure](#AzureVM)  
  
[6.0 Analysis Services](#SSAS)  
  
[7.0 Data Quality Services](#DQS)  
  
[8.0 Asesor de actualizaciones](#UA)  
  
## <a name="BeforeInstall"></a>1.0 Antes de la instalación  
  
### <a name="11-limitations-and-restrictions-in-sql-server-2014-rtm"></a>1.1 Limitaciones y restricciones de SQL Server 2014 RTM  
  
#### <a name="111-general-limitations-and-restrictions"></a>1.1.1 Limitaciones y restricciones generales  
  
1.  NO se admite la actualización de SQL Server 2014 CTP 1 a SQL Server 2014 RTM.  
  
2.  NO se admite la instalación de SQL Server 2014 CTP 1 en paralelo con SQL Server 2014 RTM.  
  
3.  NO se admite adjuntar o restaurar una base de datos de SQL Server 2014 CTP 1 a SQL Server 2014 RTM.  
  
**Solución alternativa** : ninguna.  
  
#### <a name="12-considerations-for-upgrading-sql-server-2014-ctp-2-to-sql-server-2014-rtm-and-downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>1.2 Consideraciones para actualizar SQL Server 2014 CTP 2 a SQL Server 2014 RTM y degradar SQL Server 2014 RTM a SQL Server 2014 CTP 2  
  
#### <a name="121-upgrading-from-sql-server-2014-ctp-2-to-sql-server-rtm-is-fully-supported"></a>1.2.1 Se admite totalmente la actualización de SQL Server 2014 CTP 2 a SQL Server RTM  
En concreto, puede:  
  
1.  Adjuntar una base de datos de SQL Server 2014 CTP 2 a una instancia de SQL Server 2014 RTM.  
  
2.  Restaurar una copia de seguridad de una base de datos realizada en SQL Server 2014 CTP 2 en una instancia de SQL Server 2014 RTM.  
  
3.  Actualizar en contexto a SQL Server 2014 RTM.  
  
4.  Realizar una actualización gradual a SQL Server 2014 RTM. Es necesario cambiar al modo de conmutación por error manual antes de iniciar la actualización gradual. Vea [Actualizar servidores de un grupo de disponibilidad con una pérdida de datos y un tiempo de inactividad mínimos](http://msdn.microsoft.com/library/dn178483.aspx) para obtener más detalles.  
  
5.  Los datos recopilados por los conjuntos de recopilación de rendimiento de transacción instalados en SQL Server 2014 CTP 2 no se pueden ver mediante SQL Server Management Studio en SQL Server 2014 RTM y viceversa. Use SQL Server Management Studio en SQL Server 2014 CTP 2 para ver los datos recopilados por el conjunto de recopilación instalado en SQL Server 2014 CTP 2 y use SQL Server Management Studio en SQL Server 2014 RTM para ver los datos recopilados por el conjunto de recopilación instalado en SQL Server 2014 RTM.  
  
### <a name="122-downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>1.2.2 Degradar SQL Server 2014 RTM a SQL Server 2014 CTP 2  
Esto no se admite.  
  
**Solución alternativa** : no hay ninguna solución alternativa para la degradación. Se recomienda hacer una copia de seguridad de la base de datos antes de actualizarse a SQL Server 2014 RTM.  
  
![Icono de flecha usado con el vínculo Volver al principio](../sql-server/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Arriba](#top)  
  
## <a name="13-incorrect-version-of-streaminsight-client-on-sql-server-2014-mediaisocab"></a>1.3 Versión incorrecta del cliente StreamInsight en SQL Server 2014 media/ISO/CAB  
En la ruta de acceso de SQL Server media /ISO/CAB se encuentra la versión incorrecta de StreamInsight.msi y StreamInsightClient.msi (StreamInsight\\\<Architecture\>\\\<Language ID\>).  
  
**Solución alternativa:** descargar e instalar la versión correcta de la [página de descarga de SQL Server 2014 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=306709).  
  
## <a name="ProdDoc"></a>2.0 Documentación del producto  
  
### <a name="21-report-builder-content-is-not-available-in-some-languages"></a>2.1 El contenido del Generador de informes no está disponible en algunos idiomas.  
**Problema** : el contenido del Generador de informes no está disponible en los idiomas siguientes.  
  
-   Griego (el-GR)  
  
-   Noruego (Bokmal) (nb-NO)  
  
-   Finés (fi-FI)  
  
-   Danés (DA-DK)  
  
En [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], este contenido estaba disponible en un archivo CHM que se incluía con el producto y estaba disponible en estos idiomas. Los archivos CHM ya no se incluyen con el producto y el contenido del Generador de informes solo está disponible en MSDN. MSDN no admite estos idiomas. El Generador de informes también se quitó de TechNet y ya no está disponible en esos idiomas admitidos.  
  
**Solución alternativa** : ninguna.  
  
### <a name="22-powerpivot-content-is-not-available-in-some-languages"></a>2.2 El contenido de PowerPivot no está disponible en algunos idiomas.  
**Problema** : el contenido de Power Pivot no está disponible en los idiomas siguientes.  
  
-   Griego (el-GR)  
  
-   Noruego (Bokmal) (nb-NO)  
  
-   Finés (fi-FI)  
  
-   Danés (DA-DK)  
  
-   Checo (cs-CZ)  
  
-   Húngaro (hu-HU)  
  
-   Holandés (Países Bajos) (nl-NL)  
  
-   Polaco (pl-PL)  
  
-   Sueco (sv-SE)  
  
-   Turco (tr-TR)  
  
-   Portugués (Portugal) (pt-PT)  
  
En [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], este contenido estaba disponible en TechNet y en estos idiomas. Este contenido se quitó de TechNet y ya no está disponible en estos idiomas admitidos.  
  
**Solución alternativa** : ninguna.  
  
![Icono de flecha usado con el vínculo Volver al principio](../sql-server/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Arriba](#top)  
  
## <a name="DBEngine"></a>3.0 Motor de base de datos  
  
### <a name="31-changes-made-for-standard-edition-in-sql-server-2014-rtm"></a>3.1 Cambios realizados en la edición Standard de SQL Server 2014 RTM  
SQL Server 2014 Standard incluye los cambios siguientes:  
  
-   La característica de extensión del grupo de búferes permite usar el tamaño máximo de hasta 4 veces la memoria configurada.  
  
-   La memoria máxima se ha ampliado de 64 a 128 GB.  
  
### <a name="32-in-memory-oltp-issues"></a>3.2 Problemas de OLTP en memoria  
  
#### <a name="321-memory-optimization-advisor-flags-default-constraints-as-incompatible"></a>3.2.1 El Asesor de optimización para memoria marca las restricciones DEFAULT como incompatibles  
**Problema** : el Asesor de optimización para memoria de SQL Server Management Studio marca todas las restricciones DEFAULT como incompatibles. En una tabla optimizada para memoria no se admiten todas las restricciones DEFAULT; el asesor no distingue entre los tipos admitidos y no admitidos de las restricciones DEFAULT. Entre las restricciones DEFAULT admitidas se incluyen todas las constantes, expresiones y funciones integradas que se admiten dentro de los procedimientos almacenados compilados de forma nativa. Para ver la lista de funciones admitidas en los procedimientos almacenados compilados de forma nativa, vea [Construcciones admitidas en procedimientos almacenados compilados de forma nativa](http://msdn.microsoft.com/library/dn452279(v=sql.120).aspx).  
  
**Solución alternativa** : si desea usar el asesor para identificar bloqueadores, omita las restricciones DEFAULT compatibles. Para usar el Asesor de optimización para memoria con el fin de migrar tablas que tienen restricciones DEFAULT compatibles, pero no otros bloqueadores, siga estos pasos:  
  
1.  Quite la restricción DEFAULT de la definición de tabla.  
  
2.  Use el asesor para generar un script de migración en la tabla.  
  
3.  Vuelva a agregar las restricciones DEFAULT al script de migración.  
  
4.  Ejecute el script de migración.  
  
#### <a name="322-informational-message-file-access-denied-incorrectly-reported-as-an-error-in-the-sql-server-2014-error-log"></a>3.2.2 El mensaje informativo “acceso a archivo denegado” se notifica incorrectamente como un error en el registro de errores de SQL Server 2014  

            **Problema** : al reiniciar un servidor que tiene bases de datos que contienen tablas optimizadas para memoria, puede ver el siguiente tipo de mensajes de error en el registro de errores de SQL Server 2014:  
  
```  
[ERROR]Unable to delete file C:\Program Files\Microsoft SQL   
Server\....old.dll. This error may be due to a previous failure to unload   
memory-optimized table DLLs.  
```  
  
De hecho, este mensaje es solo informativo y no se requiere ninguna acción por parte del usuario.  
  
**Solución alternativa** : ninguna. Este mensaje es meramente informativo.  
  
#### <a name="323-missing-index-details-incorrectly-report-included-columns-for-memory-optimized-table"></a>3.2.3 Los detalles de índices que faltan indican incorrectamente columnas incluidas para la tabla optimizada para memoria  

            **Problema** : si SQL Server 2014 detecta que falta un índice para una consulta en una tabla optimizada para memoria, notificará un índice ausente en SHOWPLAN_XML, así como en las DMV de índices que faltan, como sys.dm_db_missing_index_details. En algunos casos, los detalles de los índices que faltan contendrán columnas incluidas. Como todas las columnas se incluyen implícitamente con todos los índices de las tablas optimizadas para memoria, no se permite especificar explícitamente columnas incluidas con índices optimizados para memoria.  
  

            **Solución alternativa** : no especifique la cláusula INCLUDE con índices en tablas optimizadas para memoria.  
  
#### <a name="324-missing-index-details-omit-missing-indexes-if-a-hash-index-exists-but-is-not-suitable-for-the-query"></a>3.2.4 Los detalles de índices que faltan omiten índices que faltan si un índice hash existe pero no es adecuado para la consulta  

            **Problema** : si tiene un índice HASH en columnas de una tabla optimizada para memoria a la que se hace referencia en una consulta, pero el índice no se puede usar para la consulta, SQL Server 2014 no notificará siempre un índice que falta en SHOWPLAN_XML y en la DMV sys.dm_db_missing_index_details.  
  
En concreto, si una consulta contiene predicados de igualdad que implican un subconjunto de las columnas de clave de índice o si contiene predicados de desigualdad que implican las columnas de clave de índice, el índice HASH no se puede usar tal cual y se necesitaría otro índice para ejecutar la consulta de forma eficaz.  
  
**Solución alternativa** : en caso de que esté usando índices hash, inspeccione las consultas y los planes de consulta para determinar si las consultas pueden beneficiarse de operaciones Index Seek en un subconjunto de la clave de índice, o de operaciones Index Seek en predicados de desigualdad. Si necesita buscar en un subconjunto de la clave de índice, use un índice NO CLÚSTER, o use un índice HASH solamente en las columnas en las que necesita buscar. Si necesita buscar en un predicado de desigualdad, use un índice NO CLÚSTER en lugar de HASH.  
  
#### <a name="325-failure-when-using-a-memory-optimized-table-and-memory-optimized-table-variable-in-the-same-query-if-the-database-option-readcommittedsnapshot-is-set-to-on"></a>3.2.5 Error al usar una tabla optimizada para memoria y una variable de tabla optimizada para memoria en la misma consulta, si la opción de base de datos READ_COMMITTED_SNAPSHOT está establecida en ON  

            **Problema** : si la opción de base de datos READ_COMMITTED_SNAPSHOT está establecida en ON, y tiene acceso a una tabla optimizada para memoria y a una variable de tabla optimizada para memoria en la misma instrucción fuera del contexto de una transacción de usuario, puede aparecer este mensaje de error:  
  
```  
Msg 41359  
A query that accesses memory optimized tables using the READ COMMITTED  
isolation level, cannot access disk based tables when the database option  
READ_COMMITTED_SNAPSHOT is set to ON. Provide a supported isolation level  
for the memory optimized table using a table hint, such as WITH (SNAPSHOT).  
```  
  
**Solución alternativa** : use la sugerencia de tabla WITH (SNAPSHOT) con la variable de tabla, o establezca la opción de base de datos MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT en ON, con la siguiente instrucción:  
  
```  
ALTER DATABASE CURRENT   
SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
```  
  
#### <a name="326-procedure-and-query-execution-statistics-for-natively-compiled-stored-procedures-record-worker-time-in-multiples-of-1000"></a>3.2.6 Las estadísticas de ejecución de procedimientos y consultas para los procedimientos almacenados compilados de forma nativa registran el tiempo de trabajo en múltiplos de 1000  
**Problema:** después de habilitar la recopilación de estadísticas de ejecución de procedimientos o de consultas para los procedimientos almacenados compilados de forma nativa mediante sp_xtp_control_proc_exec_stats o sp_xtp_control_query_exec_stats, verá que *_worker_time se muestra en múltiplos de 1000 en las DMV sys.dm_exec_procedure_stats y sys.dm_exec_query_stats. Las ejecuciones de consultas que tienen un tiempo de trabajo inferior a 500 microsegundos se notificarán con un valor de worker_time de 0.  
  
**Solución alternativa** : ninguna. No se fie del valor de worker_time notificado en las DMV de estadísticas de ejecución para las consultas de ejecución breve en procedimientos almacenados compilados de forma nativa.  
  
#### <a name="327-error-with-showplanxml-for-natively-compiled-stored-procedures-that-contain-long-expressions"></a>3.2.7 Error con SHOWPLAN_XML para los procedimientos almacenados compilados de forma nativa que contienen expresiones largas  
**Problema:** : si un procedimiento almacenado compilado de forma nativa contiene una expresión larga, al obtener SHOWPLAN_XML para el procedimiento, ya sea con la opción T-SQL establecida en SHOWPLAN_XML ON o mediante la opción 'Mostrar plan de ejecución estimado' de Management Studio, puede aparecer el error siguiente:  
  
```  
Msg 41322. MAT/PIT export/import encountered a failure for memory  
optimized table or natively compiled stored procedure with object ID  
278292051 in database ID 6. The error code was  
0xc00cee81.  
```  
  
**Solución alternativa** : hay dos soluciones alternativas:  
  
1.  Agregar paréntesis a la expresión, de manera similar al ejemplo siguiente:  
  
    En lugar de:  
  
    ```  
    SELECT @v0 + @v1 + @v2 + ... + @v199  
    ```  
  
    Escribir:  
  
    ```  
    SELECT((@v0 + ... + @v49) + (@v50 + ... + @v99)) + ((@v100 + ... + @v149) + (@v150 + ... + @v199))  
    ```  
  
2.  Crear un segundo procedimiento con una expresión ligeramente simplificada, para el plan de presentación: la forma general del plan debe ser al misma. Por ejemplo, en lugar de:  
  
    ```  
    SELECT @v0 +@v1 +@v2 +...+@v199  
    ```  
  
    Escribir:  
  
    ```  
    SELECT @v0 +@v1  
    ```  
  
#### <a name="328-using-a-string-parameter-or-variable-with-datepart-and-related-functions-in-a-natively-compiled-stored-procedure-results-in-an-error"></a>3.2.8 El uso de un parámetro o una variable de cadena con DATEPART y funciones relacionadas en un procedimiento almacenado compilado de forma nativa produce un error  
**Problema:** cuando se usa un parámetro o una variable que tiene un tipo de datos de cadena como (var)char o n(var)char con las funciones integradas DATEPART, DAY, MONTH y YEAR dentro de un procedimiento almacenado compilado de forma nativa, verá un mensaje de error que indica que el tipo de datos datetimeoffset no se admite con los procedimientos almacenados compilados de forma nativa.  
  
**Solución alternativa** : asigne el parámetro o la variable de cadena a una nueva variable de tipo datetime2 y use esa variable en la función DATEPART, DAY, MONTH o YEAR. Por ejemplo:  
  
```  
DECLARE @d datetime2 = @string  
DATEPART(weekday, @d)  
```  
  
#### <a name="329-native-compilation-advisor-flags-delete-from-clauses-incorrectly"></a>3.2.9 El Asistente de compilación nativa marca incorrectamente las cláusulas DELETE FROM  
**Problema** : el Asistente de compilación nativa marca incorrectamente las cláusulas DELETE FROM dentro de un procedimiento almacenado como incompatibles.  
  
**Solución alternativa** : ninguna.  
  
### <a name="33-register-through-ssms-adds-dac-meta-data-with-mismatched-instance-ids"></a>3.3 El registro mediante SSMS agrega metadatos de DAC con identificadores de instancia no coincidentes  
**Problema:** al registrar o eliminar un paquete de aplicación de capa de datos (.dacpac) mediante SQL Server Management Studio, las tablas sysdac* no se actualizan correctamente para que un usuario pueda consultar el historial de dacpac de la base de datos.  Los valores de instance_id en sysdac_history_internal y sysdac_instances_internal no coinciden para permitir una combinación.  
  
**Solución alternativa:** este problema se corrige con la redistribución del Feature Pack de [Data-Tier Application Framework](https://www.microsoft.com/download/details.aspx?id=42295).  Una vez aplicada la actualización, todas las nuevas entradas del historial usarán el valor mostrado para instance_id en la tabla sysdac_instances_internal.  
  
Si ya tiene el problema con valores no coincidentes de instance_id, la única manera de corregir los valores no coincidentes es conectarse al servidor como un usuario con privilegios para escribir en la base de datos MSDB y actualizar los valores de instance_id para que coincidan.  Si hubo varios eventos de registro y anulación de registro en la misma base de datos, puede que necesite ver la fecha y hora para ver qué registros coinciden con los valores actuales de instance_id.  
  
1.  Conéctese al servidor en SQL Server Management Studio con un inicio de sesión que tenga permisos de actualización en MSDB.  
  
2.  Abra una consulta nueva usando la base de datos MSDB.  
  
3.  Ejecute esta consulta para ver todas las instancias dac activas.  Busque la instancia que quiere corregir y anote el valor de instance_id:  
  
    `select * from` sysdac_instances_internal  
  
4.  Ejecute esta consulta para ver todas las entradas del historial:  
  
    `select * from` sysdac_history_internal  
  
5.  Identifique las filas que deben corresponder a la instancia que está corrigiendo  
  
6.  Actualice el valor de sysdac_history_internal.instance_id al valor que anotó en el paso 3 (de la tabla sysdac_instances_internal):  
  
    `update` sysdac_history_internal `set` instance_id = '\<valor del paso 3\>' `where` \<expresión que coincide con las filas que desea actualizar\>  
  
![Icono de flecha usado con el vínculo Volver al principio](../sql-server/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Arriba](#top)  
  
## <a name="SSRS"></a>4.0 Reporting Services  
  
### <a name="41-the-sql-server-2012-reporting-services-native-mode-report-server-cannot-run-side-by-side-with-sql-server-2014-reporting-services-sharepoint-components"></a>4.1 El servidor de informes en modo nativo de SQL Server 2012 Reporting Services no puede ejecutarse en paralelo con los componentes de SharePoint de SQL Server 2014 Reporting Services  
**Problema** : El servicio de Windows 'SQL Server Reporting Services' (ReportingServicesService.exe) en modo nativo de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no se inicia si hay componentes de SharePoint de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] instalados en el mismo servidor.  
  
**Solución alternativa** : desinstale los componentes de SharePoint de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] y reinicie el servicio de Windows Microsoft SQL Server 2012 Reporting Services.  
  
**Más información:**  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] El modo nativo no se puede ejecutar en paralelo con ninguno de los elementos siguientes:  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Complemento para productos de SharePoint  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Servicio compartido de SharePoint  
  
La instalación en paralelo impide el inicio del servicio de Windows en modo nativo [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Aparecerán mensajes de error similares a los siguientes en el registro de eventos de Windows:  
  
```  
Log Name:   Application  
Source:          Report Server (<SQL instance ID>)  
Event ID:        117  
Task Category:   Startup/Shutdown  
Level:           Error  
Keywords:        Classic  
Description:     The report server database is an invalid version.  
  
Log Name:      Application  
Source:        Report Server (<SQL instance ID>)  
Event ID:      107  
Task Category: Management  
Level:         Error  
Keywords:      Classic  
Description:   Report Server (DENALI) cannot connect to the report server database.  
```  
  
Para obtener más información, vea [Sugerencias, trucos y solución de problemas de SQL Server 2014 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=391254).  
  
### <a name="42-required-upgrade-order-for-multi-node-sharepoint-farm-to-sql-server-2014-reporting-services"></a>4.2 Orden necesario para actualizar una granja de servidores de SharePoint de varios nodos a SQL Server 2014 Reporting Services  
**Problema** : se produce un error en la representación de informes en una granja de varios nodos si las instancias del servicio compartido de SharePoint de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se actualizan antes que todas las instancias del Complemento de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para productos de SharePoint.  
  
**Solución alternativa** : en una granja de SharePoint de varios nodos:  
  
1.  Actualice primero todas las instancias del Complemento de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para productos de SharePoint.  
  
2.  Actualice después todas las instancias del servicio compartido de SharePoint de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
Para obtener más información, vea [Sugerencias, trucos y solución de problemas de SQL Server 2014 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=391254).  
  
![Icono de flecha usado con el vínculo Volver al principio](../sql-server/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Arriba](#top)  
  
## <a name="AzureVM"></a>5.0 SQL Server 2014 RTM en máquinas virtuales de Windows Azure  
  
### <a name="51-the-add-azure-replica-wizard-returns-an-error-when-configuring-an-availability-group-listener-in-windows-azure"></a>5.1 El Asistente para agregar réplica de Azure devuelve un error al configurar un agente de escucha del grupo de disponibilidad en Windows Azure  
**Problema** : si un grupo de disponibilidad tiene un agente de escucha, el Asistente para agregar réplica de Azure devolverá un error al intentar configurar el agente de escucha en Windows Azure.  
  
Esto se debe a que los agentes de escucha de los grupos de disponibilidad necesitan que se asigne una dirección IP a cada subred que hospede réplicas de grupos de disponibilidad, incluida la subred de Azure.  
  
**Solución alternativa:**  
  
1.  En la página Agente de escucha, asigne una dirección IP estática disponible en la subred de Azure que hospedará la réplica del grupo de disponibilidad al Agente de escucha del grupo de disponibilidad.  
  
    Esto permitirá que el asistente agregue la réplica a Windows Azure.  
  
2.  Cuando se complete el asistente, necesitará finalizar la configuración del agente de escucha en Windows Azure como se describe en [Configuración del agente de escucha de los Grupos de disponibilidad de AlwaysOn en Windows Azure](http://msdn.microsoft.com/library/dn376546.aspx).  
  
![Icono de flecha usado con el vínculo Volver al principio](../sql-server/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Arriba](#top)  
  
## <a name="SSAS"></a>6.0 Analysis Services  
  
### <a name="61-msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2010-new-farm-configured-with-sql-server-2014"></a>6.1 Se debe descargar, instalar y registrar MSOLAP.5 para una nueva granja de SharePoint 2010 configurada con SQL Server 2014  
**Problema:**  
  
-   En una granja de SharePoint 2010 configurada con una implementación de SQL Server 2014 RTM, los libros PowerPivot no se pueden conectar a los modelos de datos porque el proveedor al que se hace referencia en la cadena de conexión no está instalado.  
  
**Solución alternativa:**  
  
1.  Descargue el proveedor MSOLAP.5 desde [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Pack. Instale el proveedor en los servidores de aplicaciones que ejecutan Excel Services. Para obtener más información, vea la sección "Proveedor OLE DB de Microsoft Analysis Services para Microsoft SQL Server 2012 SP1" de [Microsoft SQL Server 2012 SP1 Feature Pack](http://www.microsoft.com/download/details.aspx?id=35580).  
  
2.  Registre MSOLAP.5 como proveedor de confianza con Servicios de Excel de SharePoint. Para obtener más información, vea [Add MSOLAP.5 as a Trusted Data Provider in Excel Services](http://technet.microsoft.com/library/hh758436.aspx).  
  
**Más información:**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] incluye MSOLAP.6. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] y [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssGemini](../includes/ssgemini-md.md)] usan MSOLAP.5. Si MSOLAP.5 no está instalado en el equipo en el que se ejecuta Servicios de Excel, Servicios de Excel no puede cargar los modelos de datos.  
  
### <a name="62-msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2013-new-farm-configured-with-sql-server-2014"></a>6.2 Se debe descargar, instalar y registrar MSOLAP.5 para una nueva granja de SharePoint 2013 configurada con SQL Server 2014  
**Problema:**  
  
-   En una granja de SharePoint 2013 configurada con una implementación de [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] , libros de Excel que hacen referencia al proveedor MSOLAP.5 no se pueden conectar a los modelos de datos tabulares porque el proveedor al que se hace referencia en la cadena de conexión no está instalado.  
  
**Solución alternativa:**  
  
1.  Descargue el proveedor MSOLAP.5 desde [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Pack. Instale el proveedor en los servidores de aplicaciones que ejecutan Excel Services. Para obtener más información, vea la sección "Proveedor OLE DB de Microsoft Analysis Services para Microsoft SQL Server 2012 SP1" de [Microsoft SQL Server 2012 SP1 Feature Pack](http://www.microsoft.com/download/details.aspx?id=35580).  
  
2.  Registre MSOLAP.5 como proveedor de confianza con Servicios de Excel de SharePoint. Para obtener más información, vea [Add MSOLAP.5 as a Trusted Data Provider in Excel Services](http://technet.microsoft.com/library/hh758436.aspx).  
  
**Más información:**  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] incluye MSOLAP.6. Pero los libros PowerPivot de SQL Server 2014 usan MSOLAP.5. Si MSOLAP.5 no está instalado en el equipo en el que se ejecuta Servicios de Excel, Servicios de Excel no puede cargar los modelos de datos.  
  
### <a name="63-corrupt-data-refresh-schedules"></a>6.3 Programaciones de actualización de datos dañadas  
**Problema:**  
  
-   Actualiza una programación de actualización y la programación resulta dañada y no se puede usar.  
  
**Solución alternativa:**  
  
1.  En Microsoft Excel, desactive las propiedades avanzadas personalizadas. Vea la sección “Solución alternativa” del siguiente artículo [KB 2927748](http://support.microsoft.com/kb/2927748)de Knowledge Base.  
  
**Más información:**  
  
-   Al actualizar una programación de actualización de datos para un libro, si la longitud serializada de la programación de actualización es menor que la de la programación original, el tamaño de búfer no se actualiza correctamente y la nueva información de programación se combina con la información de programación anterior, dando lugar a una programación dañada.  
  
![Icono de flecha usado con el vínculo Volver al principio](../sql-server/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Arriba](#top)  
  
## <a name="DQS"></a>7.0 Data Quality Services  
  
### <a name="71-no-cross-version-support-for-data-quality-services-in-master-data-services"></a>7.1 No hay compatibilidad entre versiones con Data Quality Services de Master Data Services  
**Problema** : no se admiten los escenarios siguientes:  
  
-   Master Data Services 2012 hospedado en una base de datos de motor de base de datos de SQL Server en SQL Server 2012 con Data Quality Services 2012 instalado.  
  
-   Master Data Services 2012 hospedado en una base de datos de motor de base de datos de SQL Server en SQL Server 2014 con Data Quality Services 2014 instalado.  
  
**Solución alternativa** : use la misma versión de Master Data Services que la base de datos del motor de base de datos y Data Quality Services.  
  
![Icono de flecha usado con el vínculo Volver al principio](../sql-server/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Arriba](#top)  
  
## <a name="UA"></a>8.0 Problemas del Asesor de actualizaciones  
  
### <a name="81--sql-server-2014-upgrade-advisor-reports-irrelevant-upgrade-issues-for-sql-server-reporting-services"></a>8.1 El Asesor de actualizaciones de SQL Server 2014 notifica problemas irrelevantes de actualización de SQL Server Reporting Services  
**Problema** : el Asesor de actualizaciones de SQL Server (SSUA) incluido con SQL Server 2014 notifica incorrectamente varios errores al analizar el servidor de SQL Server Reporting Services.  
  
**Solución alternativa** : este problema se ha corregido en el Asesor de actualizaciones de SQL Server incluido en el [SQL Server 2014 Feature Pack para SSUA](http://go.microsoft.com/fwlink/?LinkID=306709).  
  
### <a name="82--sql-server-2014-upgrade-advisor-reports-an-error-when-analyzing-sql-server-integration-services-server"></a>8.2 El Asesor de actualizaciones de SQL Server 2014 notifica un error al analizar el servidor de SQL Server Integration Services  
**Problema** : el Asesor de actualizaciones de SQL Server (SSUA) incluido con SQL Server 2014 notifica un error al analizar el servidor de SQL Server Integration Services.  El error que se muestra al usuario es:  
  
```  
The installed version of Integration Services does not support Upgrade Advisor.   
The assembly information is "Microsoft.SqlServer.ManagedDTS, Version=11.0.0.0,   
Culture=neutral, PublicKeyToken=89845dcd8080cc91  
```  
  
**Solución alternativa** : este problema se ha corregido en el Asesor de actualizaciones de SQL Server incluido en el [SQL Server 2014 Feature Pack para SSUA](http://go.microsoft.com/fwlink/?LinkID=306709).  
  
![Icono de flecha usado con el vínculo Volver al principio](../sql-server/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio")[Arriba](#top)  
  
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
