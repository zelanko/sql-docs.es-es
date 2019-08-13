---
title: Notas de la versión de SQL Server Management Studio (SSMS) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.date: 07/31/2019
ms.openlocfilehash: e499f58eff6c09ac8d32d4cd630afc4c7855c299
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2019
ms.locfileid: "68809866"
---
# <a name="release-notes-for-sql-server-management-studio-ssms"></a>Notas de la versión de SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

En este artículo, se proporcionan detalles sobre las actualizaciones, mejoras y correcciones de errores de las versiones actuales y anteriores de SSMS.

<!--
The latest ## H2 section of this Release Notes article has been reformatted to match the new standard.
The new standard replaces the use of bullet lists with the 2-column markdown table format.
Please use the new 2-column table format going forward.
And please do include the final blank row of "| &nbsp;| &nbsp;|".

The ## H2 titles are also being shortened, by the removal of unnecessary repetitive strings.
In this case, "## SSMS 17.9" is being shortened to "## 17.9" (as one standard actual example).
Also, we are appending the 'Month yyyy.'

Also, this file has been renamed to the new standard, which calls for the file name to be with "release-notes-[techAreaName].md."
The old name for this file was 'sql-server-management-studio-changelog-ssms.md'.
But today the new file name is 'release-notes-ssms.md' (still in 'docs/ssms/').

Thank you.
GeneMi. 2019/04/02.
-->

## <a name="ssms-182"></a>SSMS 18.2

Descargar: [descargar SSMS 18.2](download-sql-server-management-studio-ssms.md)  
Número de compilación: 15.0.18142.0  
Fecha de publicación: 25 de julio de 2019

SSMS 18.2 es la versión de disponibilidad general (GA) más reciente de SSMS. Si necesita una versión anterior de SSMS, consulte [versiones de SSMS anteriores](release-notes-ssms.md#previous-ssms-releases).

18.2 es una actualización de 18.1 con los nuevos elementos y las correcciones de errores siguientes.

## <a name="whats-new-in-182"></a>Novedades de 18.2

|  Nuevo elemento  |  Detalles  |
|-------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Integration Services (SSIS) | Optimización del rendimiento del programador de paquetes SSIS en Azure. |
| Intellisense/Editor | Se ha agregado compatibilidad con la clasificación de datos. |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | Se ha agregado compatibilidad con IntelliSense. |
| OPTIMIZE_FOR_SEQUENTIAL_KEY | Activa una optimización en el motor de base de datos que ayuda a mejorar el rendimiento de las inserciones de alta simultaneidad en el índice. Esta opción está diseñada para los índices que son propensos a la contención de inserción de la última página, que suele darse con índices que tienen una clave secuencial, como una columna de identidad, de secuencia o de fecha y hora. Para obtener más detalles, vea [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys). |
| Ejecución o resultados de la consulta | Se ha agregado una *hora de finalización* en los mensajes en los que se realiza el seguimiento cuando una consulta determinada ha completado su ejecución. |
| Ejecución o resultados de la consulta | Permite que se muestren más datos (resultado a texto) y se almacenen en celdas (resultado a cuadrícula). SSMS ahora admite hasta 2 M de caracteres para ambos (hasta 256 K y 64 K, respectivamente). Esto también ha solucionado la incidencia por la que los usuarios no podían obtener más de 43 680 caracteres de las celdas de la cuadrícula. |
| ShowPlan | Se ha agregado un nuevo atributo en QueryPlan cuando la [característica escalar en línea UDF](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining) está habilitada (ContainsInlineScalarTsqludfs). |
| SMO | Se ha agregado compatibilidad con las *Restricciones de características*. Para obtener más información sobre la propia característica, vea [Restricciones de características](https://docs.microsoft.com/sql/relational-databases/security/feature-restrictions). |
| SMO | Se agregó soporte técnico para la *API de SQL Assessment*. Para obtener más información, consulte la [API de SQL Assessment](https://docs.microsoft.com/sql/sql-assessment-api/sql-assessment-api-overview). |
|  |  |

## <a name="bug-fixes-in-182"></a>Correcciones de errores en 18.2

|  Nuevo elemento  |  Detalles  |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Accesibilidad | Se ha actualizado la interfaz de usuario de XEvent (la cuadrícula) para que se pueda ordenar al presionar F3. |
| AlwaysOn | Se ha corregido un problema que hacía que SSMS produjera un error al intentar eliminar un grupo de disponibilidad (AG). |
| AlwaysOn | Se ha corregido un problema que hacía que SSMS presentase un asistente de conmutación por error incorrecto, cuando las réplicas se configuraban como sincrónicas, al usar las escalas de lectura AG (tipo de clúster = NONE). Ahora, SSMS presenta el asistente para la opción Force_Failover_Allow_Data_Loss, que es el único que se permite para la disponibilidad de tipo de clúster NONE. |
| AlwaysOn | Se ha corregido una incidencia por la que el asistente restringía el número de sincronizaciones permitidas a tres. |
| Clasificación de datos | Se ha corregido una incidencia que hacía que SSMS produjera un error *Índice (basado en cero) debe ser mayor o igual que cero* al intentar ver informes de clasificación de datos en bases de datos con un valor de CompatLevel inferior a 150. |
| SSMS general | Se ha corregido una incidencia por la que el usuario no podía desplazar horizontalmente el Panel de resultados a través de la rueda del mouse. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/34145641). |
| SSMS general | Se ha actualizado *Monitor de actividad* para omitir los tipos de espera benignos SQLTRACE_WAIT_ENTRIES. |
| SSMS general | Se ha corregido una incidencia por la que algunas opciones de color *(Editor de texto > Pestaña editor y barra de estado)* no se conservaban. Vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37924165).
| SSMS general | En el cuadro de diálogo de conexión, se ha reemplazado *Azure Active Directory: universal compatible con MFA* por *Azure Active Directory: universal con MFA* (la funcionalidad es la misma, pero probablemente sea menos confusa). |
| SSMS general | Se ha actualizado SSMS para usar los valores predeterminados correctos al crear una base de datos de Azure SQL Database. |
| SSMS general | Se ha corregido una incidencia que hacía que el usuario no pudiera *Iniciar PowerShell* desde un nodo de [Registrar servidores](register-servers/register-servers.md) cuando el servidor era un [contenedor de SQL Linux](../linux/quickstart-install-connect-docker.md). |
| Importar archivo plano | Se ha corregido una incidencia por la que *Importar un archivo plano* no funcionaba después de la actualización de SSMS 18.0 a 18.1. Vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37912636). |
| Importar archivo plano | Se ha corregido una incidencia por la que el *Asistente para la importación de archivos planos estaba notificando una columna duplicada o no válida* en un archivo .csv con encabezados con caracteres Unicode. |
| Explorador de objetos | Se ha corregido una incidencia que hacía que algunos elementos de menú (por ejemplo, el *Asistente para importación y exportación* de SQL Server) no estuvieran presentes o estuvieran deshabilitados cuando se conectaban a SQL Express. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37500016). |
| Explorador de objetos | Se ha corregido una incidencia que provocaba que SSMS se bloqueara cuando se arrastraba un objeto desde el Explorador de objetos al editor. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37887988). |
| Explorador de objetos | Se ha corregido una incidencia por la que el cambio de nombre de las bases de datos hacía que se mostraran nombres de la base de datos incorrectos en el Explorador de objetos. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37638472). |
| Explorador de objetos | Se ha corregido una incidencia pendiente durante mucho tiempo por la que, al intentar expandir el nodo *Tablas* en el Explorador de objetos de una base de datos que estuviera configurada para usar una intercalación que Windows ya no admitiera, se desencadenara un error (y el usuario no pudiera expandir las tablas). Un ejemplo de este tipo de intercalación sería Korean_Wansung_Unicode_CI_AS. |
| [Registrar servidores](register-servers/register-servers.md) | Se ha corregido una incidencia que hacía que, cuando el Servidor registrado usaba *Active Directory: integrado* o *Azure Active Directory: universal con MFA*, al intentar emitir una consulta en varios servidores (en un *Grupo* en Servidores registrados) no funcionara debido a que SSMS producía un error al conectarse. |
| [Registrar servidores](register-servers/register-servers.md) | Se ha corregido una incidencia que hacía que, cuando el Servidor registrado usaba *Active Directory: contraseña* o *SQL Auth* y el usuario no recordaba la contraseña y marcaba esta opción, al intentar emitir una consulta en varios servidores (en un *Grupo* en Servidores registrados) provocara el bloqueo de SSMS. |
| Informes | Se ha corregido una incidencia, en los informes de *Utilización de disco*, por la que se producía un error en el informe cuando los archivos de datos tenían un gran número de extensiones. |
| Herramientas de replicación | Se ha corregido una incidencia por la que el Monitor de replicación no funcionaba con la base de datos del publicador en AG ni con el distribuidor en AG (esto se corrigió anteriormente en SSMS 17.x). |
| Agente SQL | Se ha corregido una incidencia que hacía que, al agregar, insertar, editar o quitar pasos de trabajo, el foco se restableciese en la primera fila en lugar de en la fila activa. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/38070892). |
| SMO/Generación de Script | Se ha corregido una incidencia por la que la instrucción *CREATE o ALTER* no contenía objetos de scripting que tuvieran propiedades extendidas. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035-sql-server/suggestions/37236748). |
| SMO/Generación de Script | Se ha corregido una incidencia por la que SSMS no podía crear un script CREATE EXTERNAL LIBRARY correctamente. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37868089). |
| SMO/Generación de Script |  Se ha corregido una incidencia por la que, al intentar ejecutar *Generar scripts* en una base de datos con unas cuantas miles de tablas, provocara que el cuadro de diálogo de progreso pareciera bloquearse. |
| SMO/Generación de Script | Se ha corregido una incidencia por la que el scripting de *Tabla externa* en SQL 2019 no funcionaba. |
| SMO/Generación de Script | Se ha corregido una incidencia por la que el scripting de *Origen de datos externos* en SQL 2019 no funcionaba. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/34295080). |
| SMO/Generación de Script | Se ha corregido una incidencia por la que las *propiedades extendidas* de las columnas no se incluían en el script cuando el destino era una base de datos de Azure SQL Database. Vea [stackoverflow](https://stackoverflow.com/questions/56952337/how-can-i-script-the-descriptions-of-columns-in-ms-sql-server-management-studio) para obtener más detalles. |
| SMO/Generación de Script | Inserción de la última página: SMO: agregar propiedad *Index.IsOptimizedForSequentialKey* |
|**Programa de instalación de SSMS**| **Se ha mitigado una incidencia por la que el programa de instalación de SSMS bloqueaba de forma incorrecta la instalación de los idiomas que no coincidían con los informes de SSMS. Esto podría haber sido una incidencia en algunas situaciones anómalas, como una instalación anulada o una desinstalación incorrecta de una versión anterior de SSMS. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37483594/).** |
| Generador de perfiles XEvent | Se ha corregido un bloqueo que se producía cuando se cerraba el visor. |

### <a name="known-issues-182"></a>Incidencias conocidas (18.2)

- El Diagrama de base de datos creado a partir de un conjunto SSMS que se ejecuta en la máquina A no se puede modificar desde la máquina B (bloquearía SSMS). Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37992649).

- SSMS 18.0 rediseña las incidencias al cambiar entre varias ventanas de consulta. Consulte [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37474042). Una solución para esta incidencia es deshabilitar la aceleración de hardware en **Herramientas** > **Opciones**.

- Existe una limitación en el tamaño de los datos que ve en los resultados de SSMS que se muestran en la cuadrícula, el texto o el archivo.

Puede hacer referencia a [UserVoice](https://feedback.azure.com/forums/908035-sql-server) para otras incidencias conocidas y para proporcionar comentarios al equipo del producto. 

## <a name="previous-ssms-releases"></a>Versiones de SSMS anteriores

Para descargar las versiones anteriores de SSMS, haga clic en los vínculos de título de las secciones siguientes:

## <a name="downloadssdtmediadownloadpng-ssms-181httpsgomicrosoftcomfwlinklinkid2094583"></a>![descargar](../ssdt/media/download.png) [SSMS 18.1](https://go.microsoft.com/fwlink/?linkid=2094583)

- Número de versión: 18.1  
- Número de compilación: 15.0.18131.0  
- Fecha de publicación: 11 de junio de 2019  

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x804) | [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40a)

SSMS 18.1 es la versión de disponibilidad general (GA) más reciente de SSMS. Si necesita una versión anterior de SSMS, consulte [versiones de SSMS anteriores](release-notes-ssms.md#previous-ssms-releases).

18.1 es una pequeña actualización de 18.0 con los nuevos elementos y las correcciones de errores siguientes.

## <a name="whats-new-in-181"></a>Novedades de 18.1

| Nuevo elemento| Detalles|
| :-------| :------|
| Diagramas de base de datos | [Los diagramas de base de datos se han vuelto a agregar a SSMS](https://feedback.azure.com/forums/908035/suggestions/37507828).
| SSBDIAGNOSE.EXE |La herramienta Diagnose de SQL Server (herramienta de línea de comandos) se ha vuelto a agregar al paquete SSMS.|
| Integration Services (SSIS) | Compatibilidad para la programación del paquete SSIS, ubicado en el catálogo de SSIS en Azure o el sistema de archivos de Azure. Existen tres entradas para iniciar el cuadro de diálogo Nueva programación, el elemento de menú *Nueva programación…* que se muestra al hacer clic con el botón derecho en el paquete SSIS en el catálogo de SSIS en Azure, el elemento de menú *Programe el paquete SSIS en Azure* del elemento de menú *Migrar a Azure* en el elemento de menú *Herramientas* y "Programación de SSIS en Azure", que se muestra al hacer clic con el botón derecho en la carpeta Trabajos del Agente de SQL Server de la instancia administrada de Azure SQL Database.|

## <a name="bug-fixes-in-181"></a>Correcciones de errores en 18.1

| Nuevo elemento | Detalles |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Accesibilidad | Mejora de la accesibilidad de la interfaz de usuario de trabajo del agente. |
| Accesibilidad | Se ha mejorado la accesibilidad en la página de supervisión de Stretch al agregar un nombre accesible para el botón *Actualizar automáticamente*; además, se agregó un nombre accesible inteligente que va a ayudar a los usuarios a saber no solo en qué botón se encuentran, sino también el efecto que tendrá presionarlo. |
| Integración de ADS| Se ha corregido un posible bloqueo en SSMS al intentar usar los servidores registrados de ADS.|
| Diseñador de bases de datos | Se ha agregado compatibilidad con la intercalación Latin1_General_100_BIN2_UTF8 (disponible en SQL Server 2019 CTP 3.0) |
| Clasificación de datos | Se evita la adición de etiquetas de confidencialidad a las columnas de la tabla de historial, que no se admite. |
| Clasificación de datos | Se ha solucionado un problema relacionado con el tratamiento incorrecto del nivel de compatibilidad (servidor frente a base de datos). |
| Diseñador de bases de datos | Se ha agregado compatibilidad con la intercalación Latin1_General_100_BIN2_UTF8 (disponible en SQL2019 CTP 3.0). |
| SSMS general | Se ha corregido un problema consistente en que el scripting de pseudocolumnas de un índice era incorrecto. |
| SSMS general | Se ha corregido un problema en la página Propiedades de inicio de sesión consistente en que al hacer clic en el botón *Agregar credencial* se podía producir una excepción de referencia nula. |
| SSMS general | Se ha corregido la visualización del tamaño de la columna "money" en la página de propiedades del índice. |
| SSMS general | Se ha corregido un problema consistente en que SSMS no respetaba la configuración de Intellisense de *Herramientas/Opciones* en la ventana del editor SQL. |
| SSMS general | Se ha corregido una incidencia en la que SSMS no respetaba la configuración de la ayuda ("en línea" frente a "sin conexión"). |
| Configuración elevada de ppp | Se ha corregido el diseño de los controles de los cuadros de diálogo de error de las opciones de consulta no admitidas. |
| Configuración elevada de ppp | Se ha corregido el diseño de los controles de la página *Nuevo grupo de disponibilidad* en alguna versión localizada de SSMS. |
| Configuración elevada de ppp | Se ha corregido el diseño de la página *Nueva programación de trabajo*. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37632094). |
| Importación de archivo plano | Se ha corregido una incidencia en la que las filas pueden perderse silenciosamente durante la importación.|
| Intellisense/editor | Se ha reducido el tráfico de las consultas basadas en SMO a las bases de datos de Azure SQL para IntelliSense. |
| Intellisense/editor | Se ha corregido un error gramatical en la información sobre herramientas mostrada al escribir T-SQL para crear un usuario. Además, se ha corregido el mensaje de error para eliminar la ambigüedad entre usuarios e inicios de sesión. |
| Visor de registros | Se ha corregido una incidencia en la que SSMS siempre abre el registro del servidor (o agente) actual, incluso si se hace doble clic en un inicio de sesión de archivo anterior en el Explorador de objetos. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37633648). |
| Programa de instalación de SSMS | Se ha corregido una incidencia que hacía que el programa de instalación SSMS generara un error cuando la ruta de acceso del registro de instalación contenía espacios. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37496110). |
| Programa de instalación de SSMS | Se ha corregido un problema consistente en que SSMS salía inmediatamente después de mostrar la pantalla de presentación. </br> Para obtener más detalles, vea estos sitios: [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37502512), [SSMS se niega a iniciar](https://dba.stackexchange.com/questions/238609/ssms-refuses-to-start) y [Administradores de base de datos](https://dba.stackexchange.com/questions/237086/sql-server-management-studio-18-wont-open-only-splash-screen-pops-up). |
| Explorador de objetos | Se ha eliminado la restricción sobre la habilitación de *iniciar PowerShell* al conectarse a SQL en Linux. |
| Explorador de objetos | Se ha corregido un problema que hacía que SSMS se bloquease al intentar expandir el nodo Polybase/Grupo de escalado horizontal (al conectarse a un nodo de proceso). |
| Explorador de objetos | Se ha corregido un problema consistente en que el elemento de menú *Deshabilitado* todavía estaba habilitado incluso después de deshabilitar un índice determinado. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37735375). |
| Informes | Se ha corregido un informe para mostrar realmente GrantedQueryMemory en KB (informe del panel de rendimiento de SQL). Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37167289). |
| Informes | Se ha mejorado el seguimiento del bloque de registro en escenarios de Always-On. |
| ShowPlan | Se ha agregado un nuevo elemento de plan de presentación *SpillOccurred* al esquema de plan de presentación. |
| ShowPlan | Se han agregado lecturas remotas (*ActualPageServerReads*, *ActualPageServerReadAheads*, *ActualLobPageServerReads*, *ActualLobPageServerReadAheads* ) al esquema del plan de presentación. |
| SMO/scripting | Se evita la consulta de restricciones perimetrales durante el scripting de tablas que no son de grafos. |
| SMO/scripting | Se ha eliminado la restricción sobre la clasificación de confidencialidad al generar scripts de columnas con *Clasificación de datos*. |
| SMO/scripting | Se ha corregido una incidencia en la que la opción "Generar script" de una tabla de grafos producía un error al generar datos. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898466). |
| SMO/scripting | Se ha corregido una incidencia en la que el método EnumObjects() no capturaba el nombre de esquema de un sinónimo. |
| SMO/scripting | Se ha corregido un problema en UIConnectionInfo.LoadFromStream() consistente en que la sección *AdvancedOptions* no se leía (cuando no se especificaba una contraseña). |
| Agente SQL | Se ha corregido un problema que hacía que SSMS se bloqueara al trabajar con una ventana Propiedades del trabajo. Para obtener más detalles, vea [UserVoice](https://feedback.azure.com/forums/908035/suggestions/37164244). |
| Agente SQL | Se ha corregido un problema consistente en que el botón "Ver" de *Propiedades de paso de trabajo* no siempre estaba habilitado, lo que evitaba la visualización de la salida de un paso de trabajo determinado. |
| Interfaz de usuario de XEvent | Se ha agregado una columna "Package" a la lista de XEvents para eliminar la ambigüedad de los eventos con nombres idénticos. |
| Interfaz de usuario de XEvent | Se ha agregado una asignación de tipo de clase "EXTERNAL LIBRARY" que faltaba a XEventUI. |

### <a name="known-issues-181"></a>Problemas conocidos (18.1)

- Es posible que se muestre un error a los usuarios al arrastrar un objeto de tabla del Explorador de objetos al Editor de consultas. Somos conscientes del problema y la corrección está prevista para la próxima versión.

- Las opciones de color *Conexiones de grupo* y *Conexiones de servidor único* en Opciones -> Editor de texto -> Pestaña del editor y barra de estado -> Diseño y colores de la barra de estado, no se conservan después de cerrar SSMS 18.1. Al volver a abrir SSMS, la opción Diseño y colores de la barra de estado vuelve al valor predeterminado (blanco).

- Existe una limitación en el tamaño de los datos que ve en los resultados de SSMS que se muestran en la cuadrícula, el texto o el archivo.

## <a name="downloadssdtmediadownloadpng-ssms-180httpsgomicrosoftcomfwlinklinkid2088649"></a>![descargar](../ssdt/media/download.png) [SSMS 18.0](https://go.microsoft.com/fwlink/?linkid=2088649)

- Número de versión: 18.0  
- Número de compilación: 15.0.18118.0  
- Fecha de publicación: 24 de abril de 2019

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x40a)

### <a name="whats-new-in-180"></a>Novedades de 18.0

| Nuevo elemento| Detalles|
| :-------| :------|
|Compatibilidad con SQL Server 2019|SSMS 18.0 es la primera versión de este producto que es totalmente *compatible* con SQL Server 2019 (compatLevel 150).|
|Compatibilidad con SQL Server 2019|Es compatible con "BATCH_STARTED_GROUP" y "BATCH_COMPLETED_GROUP" en SQL Server 2019 y la instancia administrada de SQL Database.|
|Compatibilidad con SQL Server 2019|SMO: se añade compatibilidad para la Inserción de UDF.|
|Compatibilidad con SQL Server 2019|GraphDB: se agrega una marca en el plan de presentación para Graph TC Sequence.|
|Compatibilidad con SQL Server 2019|Always Encrypted: se ha agregado compatibilidad para AEv2 / Enclave.|
|Compatibilidad con SQL Server 2019|Always Encrypted: el cuadro de diálogo de conexión presenta una nueva pestaña "Always Encrypted" cuando el usuario hace clic en el botón "Opciones" para habilitar o configurar la compatibilidad de enclave.|
|Tamaño de descarga SSMS más pequeño| El tamaño actual es de unos 500 MB, aproximadamente la mitad del conjunto de SSMS 17.x.
|SSMS Se basa en el shell aislado de Visual Studio 2017|El nuevo shell (SSMS se basa en Visual Studio 2017 15.9.11) desbloquea todas las correcciones de accesibilidad que se han incluido en SSMS y Visual Studio e incluye las correcciones de seguridad más recientes.|
|Mejoras de accesibilidad de SSMS| Se ha realizado un gran esfuerzo para resolver las incidencias de accesibilidad en todas las herramientas (SSMS, DTA y Profiler).|
|Ahora puede instalarse SSMS en una carpeta personalizada.| Esta opción está disponible desde la línea de comandos (útil para la instalación desatendida) y la configuración de la interfaz de usuario. Desde la línea de comandos, pase este argumento adicional a SSMS-Setup-ENU.exe:   SSMSInstallRoot=C:\MySSMS18 De forma predeterminada, la nueva ubicación de instalación para SSMS es la siguiente: %ProgramFiles(x86)%\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe.  Esto no significa que SSMS sea de instancias múltiples.|
|SSMS permite instalar en un idioma distinto del sistema operativo.|Se ha suprimido el bloque en la configuración de idiomas mixtos. Por ejemplo, puede instalar SSMS en alemán en un Windows en francés. Si el idioma del sistema operativo no coincide con el idioma de SSMS, el usuario debe cambiar el idioma en **Herramientas** > **Opciones** > **Configuración internacional**. En caso contrario, SSMS mostrará la interfaz de usuario en inglés.|
|SSMS ya no comparte componentes con el motor SQL.|Se ha realizado un gran esfuerzo para evitar compartir componentes con el motor SQL, lo que a menudo daba lugar a incidencias de servicio (uno sobrescribía los archivos instalados por el otro).|
|SSMS requiere NetFx 4.7.2 o posterior|Hemos actualizado nuestros requisitos mínimos de NetFx4.6.1 a NetFx4.7.2: esto nos permite aprovechar las ventajas de la nueva funcionalidad expuesta en el nuevo marco.|
|Capacidad de migrar la configuración de SSMS| Cuando SSMS 18 se inicia por primera vez, se le pide al usuario que migre la configuración de la versión 17.x. Los archivos de configuración de usuario ahora se almacenan como un archivo XML sin formato, de este modo mejora la portabilidad y, posiblemente, permite la edición.|
|Compatibilidad con la configuración elevada de PPP| La configuración elevada de PPP está habilitada de manera predeterminada.|
|SSMS se entrega con el controlador OLE DB de Microsoft.| Para obtener más detalles, consulte [Descarga del controlador Microsoft OLE DB para SQL Server](https://docs.microsoft.com/sql/connect/oledb/download-oledb-driver-for-sql-server).|
|SSMS no se admite en Windows 8. Windows 10 y Windows Server 2016 requieren la versión 1607 (10.0.14393) o posterior.|Debido a la nueva dependencia de NetFx 4.7.2, SSMS 18.0 no se instala en Windows 8 ni en las versiones antiguas de Windows 10 y Windows Server 2016. La configuración de SSMS bloquea esos sistemas. Windows 8.1 sigue siendo compatible.|
|SSMS ya no se agrega a la variable de entorno PATH.|La ruta de acceso a SSMS.EXE (y las herramientas en general) ya no se agrega más a la ruta de acceso. Los usuarios pueden agregarla de forma manual o, si se encuentran en un equipo moderno de Windows, usar el menú Inicio.|
|Los identificadores de paquete ya no tienen que desarrollar extensiones de SSMS.| En el pasado, SSMS cargaba selectivamente solo los paquetes conocidos, lo que requería que los desarrolladores registrasen sus propios paquetes. Este ya no es el caso.|
|SSMS general|Se expone la opción de configuración AUTOGROW_ALL_FILES para grupos de archivos en SSMS.|
|SSMS general|Se han eliminado las opciones con riesgo "agrupación ligera" y "aumento de prioridad" de la interfaz gráfica de usuario de SSMS. Para obtener más información, consulte [Detalles de aumento de prioridad y por qué no se recomienda](https://blogs.msdn.microsoft.com/arvindsh/2010/01/26/priority-boost-details-and-why-its-not-recommended/).
|SSMS general|Nuevos enlaces de teclado y menú para crear archivos **CTRL+ALT+N**. Se mantiene **CTRL+N** para crear una consulta.|
|SSMS general|Ahora el cuadro de diálogo **Nueva regla de firewall** permite al usuario especificar un nombre de regla, en lugar de generar uno de forma automática en nombre del usuario.|
|SSMS general|Mejora de IntelliSense en el editor, especialmente para la versión v140 de T-SQL y versiones posteriores.|
|SSMS general|Se ha agregado compatibilidad de la interfaz de usuario de SSMS con UTF-8 en el diálogo de intercalación.|
|SSMS general|Se ha cambiado al "Administrador de credenciales de Windows" para las contraseñas utilizadas recientemente en el cuadro de diálogo de conexión. Esto soluciona un problema pendiente desde hace mucho tiempo consistente en que la persistencia de las contraseñas no siempre era fiable.|
|SSMS general|Compatibilidad mejorada con sistemas de varios monitores al asegurarnos de que aparezcan cada vez más diálogos y ventanas en el monitor esperado.|
|SSMS general|Se ha expuesto la configuración de servidor "valor predeterminado de la suma de comprobación de copia de seguridad" en la nueva página de configuración de la base de datos del diálogo de propiedades del servidor. Para obtener detalles, vea [https://feedback.azure.com/forums/08035-sql-server/suggestions/34634974](https://feedback.azure.com/forums/08035-sql-server/suggestions/34634974).|
|SSMS general|Se expone el "tamaño máximo de los archivos de registro de errores" en "Configurar registros de errores de SQL Server". Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/33624115](https://feedback.azure.com/forums/908035/suggestions/33624115).|
|SSMS general|Se ha agregado "Migrar a Azure" al menú Herramientas: se ha integrado Database Migration Assistant y Azure Database Migration Service con el fin de proporcionar acceso rápido y sencillo para ayudar a acelerar las migraciones a Azure.|
|SSMS general|Se ha agregado lógica para pedirle al usuario que confirme las transacciones abiertas cuando se usa "Cambiar la conexión".|
|Integración de Azure Data Studio|Se ha agregado un elemento de menú para iniciar o descargar Azure Data Studio.|
|Integración de Azure Data Studio|Se ha agregado el elemento de menú "Iniciar Azure Data Studio" al Explorador de objetos.|
|Integración de Azure Data Studio|Cuando se hace clic con el botón secundario en un nodo de base de datos en OE, al usuario se le presentan menús contextuales para ejecutar una consulta o crear un nuevo cuaderno en Azure Data Studio.|
|Compatibilidad con Azure SQL| Las propiedades de base de datos SLO/edición/MaxSize ahora aceptan nombres personalizados, lo que facilita la compatibilidad con ediciones futuras de bases de datos de Azure SQL.|
|Compatibilidad con Azure SQL| Se ha agregado compatibilidad con las SKU de los núcleos virtuales (De uso general y Crítico para la empresa): Gen4_24 y la serie Gen5 completa.|
|Instancia administrada de Azure SQL|Se han agregado "Inicios de sesión de AAD" como nuevo tipo de inicio de sesión de SMO y SSMS cuando se conecta a una instancia administrada de Azure SQL.|
|AlwaysOn|Se recombinan RTO (tiempo de recuperación estimado) y RPO (pérdida de datos estimada) en el panel Always On de SSMS. Vea la documentación actualizada en [https://docs.microsoft.com/sql/database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups](../database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups.md).|
|Always Encrypted| La casilla Habilitar Always Encrypted de la pestaña Always Encrypted del cuadro de diálogo Conectar con el servidor ofrece ahora una manera fácil de habilitar y deshabilitar Always Encrypted para una conexión de base de datos.|
|Always Encrypted con enclaves seguros| Se han realizado varias mejoras para admitir Always Encrypted con enclaves seguros en la versión preliminar de SQL Server 2019:  Un campo de texto para especificar la dirección URL de atestación de enclave en el cuadro de diálogo Conectar con el servidor (nueva pestaña Always Encrypted).  La nueva casilla del cuadro de diálogo Nueva clave maestra de columna para controlar si una nueva clave maestra de columna permite cálculos de enclave.  Otros cuadros de diálogo de administración de claves de Always Encrypted exponen ahora la información sobre qué claves maestras de columna permiten cálculos de enclave.|
|Archivos de auditoría|Se ha cambiado el método de autenticación basada en Clave de cuenta de almacenamiento a autenticación basada en AD Azure.|
|Archivos de auditoría|Se ha actualizado la lista de las acciones de auditoría conocidas para incluir FEATURE RESTRICTION ADD/CHANGE GROUP/DROP.|
|Clasificación de datos| Se ha reorganizado el menú de tareas de clasificación de datos: se ha agregado un submenú al menú de tareas de base de datos y una opción para abrir el informe desde el menú sin tener que abrir primero la ventana de clasificación de datos.|
|Clasificación de datos|Se ha agregado la nueva característica "Clasificación de datos" a SMO. El objeto de columna expone propiedades nuevas: SensitivityLabelName, SensitivityLabelId, SensitivityInformationTypeName, SensitivityInformationTypeId e IsClassified (de solo lectura). Para obtener más información, consulte [ADD SENSITIVITY CLASSIFICATION (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/add-sensitivity-classification-transact-sql)|
|Clasificación de datos|Se ha agregado el elemento de menú "Informe de clasificación" al control flotante "Clasificación de datos".|
|Clasificación de datos| Recomendaciones actualizadas.|
|Actualización del nivel de compatibilidad de la base de datos|Se ha agregado una opción nueva en ***Nombre de base de datos*** > ***Tareas*** > ***Actualizar base de datos***. Esta opción iniciará el nuevo **Asistente para la optimización de consultas (QTA)** que guía a los usuarios a través de los procesos siguientes: Recopilación de una línea de base de rendimiento antes de actualizar el nivel de compatibilidad de la base de datos. Actualización al nivel de compatibilidad de la base de datos deseado.  Recopilación de un segundo paso de datos de rendimiento a través de la misma carga de trabajo. Detección de regresiones de carga de trabajo y proporcionar recomendaciones comprobadas para mejorar el rendimiento de la carga de trabajo.  Esto es similar al proceso de actualización de base de datos documentado en [escenarios de uso del almacén de consultas](https://docs.microsoft.com/sql/relational-databases/performance/query-store-usage-scenarios#CEUpgrade), excepto el último paso donde QTA no se basa en un estado correcto conocido previamente para generar las recomendaciones.|
|Asistente para aplicaciones de capa de datos|Se ha agregado compatibilidad para importar o exportar la aplicación de capa de datos con tablas de grafos.|
|Asistente para la importación de archivos planos|Se ha agregado lógica para notificar al usuario que una importación puede haber producido un cambio de nombre de las columnas.|
|Integration Services (SSIS)|Se ha agregado compatibilidad para permitir que los clientes programen paquetes SSIS en los Azure-SSIS IR que están en la nube de Azure Government.|
|Integration Services (SSIS)|Cuando se usa el Agente SQL de la instancia administrada de Azure SQL mediante SSMS, se puede configurar el administrador de conexiones y parámetros en el paso de trabajo del agente SSIS.|
|Integration Services (SSIS)|Al conectarse a Azure SQL DB o a la instancia administrada, se puede conectar con la opción *predeterminada* como base de datos inicial.|
|Integration Services (SSIS)|Se ha agregado un nuevo elemento de entrada **Probar SSIS en Azure Data Factory** en el nodo "Catálogos de Integration Services", que se puede usar para iniciar el "Asistente para la creación de un entorno de ejecución de integración" y crear de forma rápida "Azure-SSIS Integration Runtime".
|Integration Services (SSIS)|Se ha agregado un botón **Create SSIS IR** (Crear entorno de ejecución de integración de SSI) a "Catalog Creation Wizard" (Asistente para crear catálogos), que se puede usar para iniciar el "Asistente para la creación de un entorno de ejecución de integración" y crear de forma rápida "Azure-SSIS Integration Runtime".|
|Integration Services (SSIS)|ISDeploymentWizard ahora admite autenticación SQL, autenticación integrada de Azure Active Directory y autenticación de contraseña de Azure Active Directory en el modo de línea de comandos.|
|Integration Services (SSIS)|El Asistente para la implementación ahora admite la creación y la implementación en SSIS Integration Runtime en Azure Data Factory.|
|Scripting de objetos|Se han agregado elementos de menú nuevos para "CREATE OR ALTER" al generar scripts de objetos.|
|Almacén de consultas|Se ha mejorado la facilidad de uso de algunos informes (Consumos de recursos globales) mediante la adición del separador de miles a los números que aparecen en el eje Y de los gráficos.|
|Almacén de consultas|Se ha agregado un nuevo informe de estadísticas de espera de consulta.|
|Almacén de consultas|Se ha agregado la métrica "Recuento de ejecuciones" a la vista "Consulta con seguimiento".|
|Herramientas de replicación|Se ha agregado compatibilidad para la característica de especificación de puerto no predeterminado en el Monitor de replicación y SSMS.|
|ShowPlan|Se han agregado filas estimadas frente a reales en el tiempo real transcurrido en el nodo de operadores de plan de presentación, si están disponibles. Esta opción hace que el plan real tenga una apariencia coherente con el plan de estadísticas de consulta activa.|
|ShowPlan|Se ha modificado la información sobre herramientas y se ha agregado un comentario al hacer clic en el botón Editar consulta para un plan de presentación, que indica al usuario que puede que el motor SQL trunque el plan de presentación si la consulta es más de 4000 caracteres.|
|ShowPlan|Se ha agregado lógica para mostrar el "operador Materializer (instrucción Select externa)".|
|ShowPlan|Se ha agregado el nuevo atributo de plan de presentación BatchModeOnRowStoreUsed para identificar fácilmente las consultas en las que se usa la característica de "examen de modo por lotes en almacenes de filas". Cada vez que una consulta realiza el examen de modo por lotes en almacenes de filas, se agrega un nuevo atributo (BatchModeOnRowStoreUsed = "true") al elemento StmtSimple.|
|ShowPlan|Se ha agregado compatibilidad de plan de presentación al elemento RelOp LocalCube para DW ROLLUP y CUBE.|
|ShowPlan|Nuevo operador LocalCube para la nueva característica de agregación ROLLUP y CUBE en Azure SQL Data Warehouse.|
|SMO| Se amplía la compatibilidad SMO con la creación de índices reanudables.|
|SMO| Se agregó un nuevo evento en los objetos SMO ("PropertyMissing") para que los creadores de aplicaciones detecten antes los problemas de rendimiento SMO.|
|SMO| Se ha expuesto la nueva propiedad DefaultBackupChecksum en el objeto de configuración que se asigna a la configuración de servidor "Valor predeterminado de la suma de comprobación de copia de seguridad".|
|SMO| Se expone la nueva propiedad ProductUpdateLevel en el objeto de servidor, que se asigna al nivel de servicio para la versión de SQL en uso (por ejemplo, CU12, RTM).|
|SMO| Se expone la propiedad nueva LastGoodCheckDbTime en el objeto de base de datos, que se asigna a la propiedad de base de datos "lastgoodcheckdbtime". Si esta propiedad no está disponible, se devuelve un valor predeterminado de 1/1/1900 12:00:00 AM.|
|SMO|Se ha movido la ubicación del archivo RegSrvr.xml (archivo de configuración de servidor registrado) a "%AppData%\Microsoft\SQL Server Management Studio" (sin versión, para que se pueda compartir entre las versiones de SSMS).|
|SMO|Se ha agregado "Testigo de la nube" como un tipo de cuórum nuevo y como un tipo de recurso nuevo.|
|SMO|Se ha agregado compatibilidad con las "restricciones perimetrales" en SMO y SSMS.|
|SMO|Se ha agregado compatibilidad con la eliminación en cascada a las "restricciones perimetrales" en SMO y SSMS.|
|SMO|Se ha agregado compatibilidad para los permisos de "lectura-escritura" de la clasificación de datos.|
|Evaluación de vulnerabilidad| Se ha habilitado el menú de tareas Evaluación de vulnerabilidad en Azure SQL Data Warehouse.|
|Evaluación de vulnerabilidad|Se ha cambiado el conjunto de reglas de evaluación de vulnerabilidades que se ejecuta en servidores de Instancia administrada de Azure SQL para que los resultados del examen de "evaluación de vulnerabilidades" sean coherentes con los de Azure SQL DB.|
|Evaluación de vulnerabilidad| "Evaluación de vulnerabilidades de SQL" ahora es compatible con Azure SQL Data Warehouse.|
|Evaluación de vulnerabilidad|Se ha agregado una nueva característica de exportación para exportar los resultados del examen de evaluación de vulnerabilidades a Excel.|
|Visor de XEvent|En el Visor de XEvent se ha habilitado la ventana de plan de presentación para más elementos XEvent.|

### <a name="bug-fixes-in-180"></a>Correcciones de errores en 18.0

| Nuevo elemento| Detalles|
| :-------| :------|
|Bloqueos|Se ha corregido una fuente frecuente de bloqueos de SSMS relacionados con objetos GDI.|
|Bloqueos|Se ha corregido una fuente frecuente de errores y rendimiento deficiente cuando se selecciona "Script como Crear/Actualizar/Colocar" (se han eliminado capturas innecesarias de objetos SMO).|
|Bloqueos|Se ha corregido un error cuando se conecta a una Azure SQL DB con MFA mientras se habilitan los seguimientos de ADAL.|
|Bloqueos|Se ha corregido un bloqueo (o bloqueo percibido) en Estadísticas de consultas dinámicas cuando se invoca desde el Monitor de actividad (el problema se manifiesta cuando se utiliza la autenticación de SQL Server sin haber establecido "información de seguridad persistente").|
|Bloqueos|Se ha corregido un bloqueo al seleccionar "Informes" en el Explorador de objetos que se podía manifestar en conexiones de alta latencia o en la opción de no accesibilidad temporal de los recursos.|
|Bloqueos|Se ha corregido un bloqueo en SSMS cuando se intenta usar el Servidor de administración central y los servidores de Azure SQL. Para obtener más información, consulte [Error y bloqueo de la aplicación SSMS 17.5 cuando se usa el Servidor de administración central](https://feedback.azure.com/forums/908035/suggestions/33374884).|
|Bloqueos|Se ha corregido un bloqueo en el Explorador de objetos mediante la optimización de la manera de recuperar la propiedad IsFullTextEnabled.|
|Bloqueos|Se ha corregido un error en el "Asistente para copiar bases de datos" al evitar la compilación de consultas innecesarias para recuperar propiedades de la base de datos.|
|Bloqueos|Se ha corregido una incidencia que provocaba que SSMS diera error o se bloqueara al editar T-SQL.|
|Bloqueos|Se ha mitigado una incidencia que hacía que SSMS dejara de responder al editar scripts de T-SQL grandes.|
|Bloqueos|Se ha corregido una incidencia que provocaba que SSMS se quedara sin memoria cuando se administraban los grandes conjuntos de datos que devolvían las consultas.|
|SSMS general|Se ha corregido un problema consistente en que "ApplicationIntent" no se pasaba en las conexiones en "Servidores registrados".|
|SSMS general|Se ha corregido una incidencia en la que el formulario "Nueva interfaz de usuario del asistente de sesión de XEvent" no se representaba correctamente en monitores con una configuración elevada de ppp.|
|SSMS general|Se ha corregido una incidencia que hacía que se intentara importar un archivo bacpac.|
|SSMS general|Se ha corregido una incidencia que provocaba que al intentar mostrar las propiedades de una base de datos (con FILEGROWTH > 2048 GB) se produjera un error de desbordamiento aritmético.|
|SSMS general|Se ha corregido un problema por el cual el informe del panel de rendimiento notificaba unas esperas PAGELATCH y PAGEIOLATCH que no se podían encontrar en los subinformes.|
|SSMS general|Se han realizado otra serie de correcciones para hacer que SSMS sea más compatible con varios monitores al tener un diálogo abierto en el monitor correcto.|
|Analysis Services (AS)|Se ha corregido una incidencia por la que se recortaba la opción "Configuración avanzada" en la interfaz de usuario de XEvent de sistema autónomo (AS).|
|Analysis Services (AS)|Se ha corregido un problema en el que el análisis de DAX inicia una excepción "No se encontró el archivo".|
|Base de datos SQL de Azure|Se ha corregido un problema consistente en que la lista de bases de datos no se rellenaba correctamente en la ventana de consulta de Azure SQL Database cuando se estaba conectado a una base de datos de usuario de Azure SQL DB en lugar de a una base de datos maestra.|
|Base de datos SQL de Azure|Se ha corregido un problema consistente en que no era posible agregar una "tabla temporal" a una base de datos de Azure SQL.|
|Base de datos SQL de Azure|Se ha habilitado la opción de submenú de propiedades de Estadísticas en el menú Estadísticas de Azure, porque desde hace bastante tiempo se admite de forma completa.|
|Azure SQL: compatibilidad general|Se han corregido problemas en el control común de la interfaz de usuario de Azure que impedían al usuario mostrar suscripciones de Azure (si había más de 50). Además, se ha cambiado la ordenación para que sea por nombre en lugar de por identificador de suscripción. Por ejemplo, el usuario podría encontrarse este error al intentar restaurar una copia de seguridad desde una dirección URL.|
|Azure SQL: compatibilidad general|Se ha corregido una incidencia en el control común de la interfaz de usuario de Azure al enumerar suscripciones que podían generar un error de tipo "El índice estaba fuera del intervalo. Debe ser un valor no negativo e inferior al tamaño de la colección." cuando el usuario no tenía suscripciones en algunos inquilinos. Por ejemplo, el usuario podría encontrarse este error al intentar restaurar una copia de seguridad desde una dirección URL.|
|Azure SQL: compatibilidad general|Se ha corregido una incidencia por la que los objetivos de nivel de servicio estaban codificados, lo que dificultaba la compatibilidad de SSMS con nuevos SLO de Azure SQL. Ahora el usuario puede iniciar sesión en Azure y permitir a SSMS recuperar todos los datos de SLO aplicables (edición y tamaño máximo).|
|Compatibilidad con la instancia administrada de Azure SQL DB|Se ha mejorado y perfeccionado la compatibilidad con instancias administradas: se han deshabilitado opciones no admitidas en la interfaz de usuario y se proporciona una corrección para la opción Ver registros de auditoría para controlar la dirección URL de destino de auditoría.|
|Compatibilidad con la instancia administrada de Azure SQL DB|El asistente para "generar y publicar scripts" crea scripts de cláusulas CREATE DATABASE no admitidas.|
|Compatibilidad con la instancia administrada de Azure SQL DB|Habilite las estadísticas de consultas activas para instancias administradas.|
|Compatibilidad con la instancia administrada de Azure SQL DB|Propiedades de la base de datos -> Archivos incluía un scripting ALTER DB ADD FILE incorrecto.|
|Compatibilidad con la instancia administrada de Azure SQL DB|Se ha corregido la regresión con el programador del servicio Agente SQL por la que se elegía la programación ONIDLE aunque se hubiera elegido algún otro tipo de programación.|
|Compatibilidad con la instancia administrada de Azure SQL DB|Se han ajustado MAXTRANSFERRATE y MAXBLOCKSIZE para realizar copias de seguridad en Azure Storage.|
|Compatibilidad con la instancia administrada de Azure SQL DB|Se ha solucionado el problema por el que el script de la copia de seguridad de registros final se creaba antes de la operación RESTORE (esto no se admite en CL).|
|Compatibilidad con la instancia administrada de Azure SQL DB|El asistente para crear bases de datos no creaba correctamente el scripting de la instrucción CREATE DATABASE.|
|Compatibilidad con la instancia administrada de Azure SQL DB|Tratamiento especial de paquetes SSIS en SSMS cuando se conecta a instancias administradas.|
|Compatibilidad con la instancia administrada de Azure SQL DB|Se ha corregido una incidencia en la que se mostraba un error al intentar usar el "Monitor de actividades" cuando estaba conectado a instancias administradas.|
|Compatibilidad con la instancia administrada de Azure SQL DB|Compatibilidad mejorada para los inicios de sesión de AAD (en el Explorador de SSMS).|
|Compatibilidad con la instancia administrada de Azure SQL DB|Se ha mejorado el scripting de los objetos de grupos de archivos de SMO.|
|Compatibilidad con la instancia administrada de Azure SQL DB|Se ha mejorado la interfaz de usuario para las credenciales.|
|Compatibilidad con la instancia administrada de Azure SQL DB|Se ha agregado compatibilidad para la replicación lógica.|
|Compatibilidad con la instancia administrada de Azure SQL DB|Se ha corregido una incidencia que provocaba un error al hacer clic con el botón derecho en una base de datos y al seleccionar "Importar la aplicación de capa de datos".|
|Compatibilidad con la instancia administrada de Azure SQL DB|Se ha corregido una incidencia que provocaba que se mostraran errores al hacer clic con el botón derecho en un valor "TempDB".|
|Compatibilidad con la instancia administrada de Azure SQL DB|Se ha corregido una incidencia que provocaba que al intentar el scripting de la instrucción ALTER DB ADD FILE de SMO, se generara un script T-SQL vacío.|
|Compatibilidad con la instancia administrada de Azure SQL DB|Se ha mejorado la visualización de las propiedades específicas del servidor de Instancia administrada (generación de hardware, nivel de servicio, almacenamiento usado y reservado).|
|Compatibilidad con la instancia administrada de Azure SQL DB|Se ha corregido un problema que provocaba que el scripting de una base de datos ("Crear script como CREATE...") no generara scripts de grupos de archivos y archivos adicionales. Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/37326799](https://feedback.azure.com/forums/908035/suggestions/37326799). |
|Realizar copia de seguridad/restaurar/adjuntar/desasociar una base de datos|Se ha corregido un problema por el que el usuario no podía adjuntar una base de datos cuando el nombre de archivo físico del archivo .mdf no coincide con el nombre de archivo original.|
|Realizar copia de seguridad/restaurar/adjuntar/desasociar una base de datos|Se ha corregido una incidencia debido a la cual era posible que SSMS no encontrase un plan de restauración válido o encontrase uno que fuera poco óptimo. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752). |
|Realizar copia de seguridad/restaurar/adjuntar/desasociar una base de datos|Se ha corregido un problema que provocaba que el asistente "Adjuntar base de datos" no mostrara los archivos secundarios cuyo nombre se hubiera cambiado. En este momento, se muestra el archivo y se agrega un comentario sobre él (por ejemplo "No se ha encontrado"). Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/32897434](https://feedback.azure.com/forums/908035/suggestions/32897434). |
|Asistente para copiar bases de datos|No se fuerza la activación de ansi_padding cuando los asistentes para copiar bases de datos, generar scripts y realizar transferencias intentan crear una tabla con una tabla en memoria.|
|Asistente para copiar bases de datos|Los asistentes para copiar bases de datos y para la tarea Transferir bases de datos se han interrumpido en SQL Server 2017 y SQL Server 2019.|
|Asistente para copiar bases de datos|Los asistentes para copiar bases de datos, para generar scripts y para transferencias incluyen en un script la creación de la tabla antes de crear el origen de datos externo asociado.|
|Cuadro de diálogo de conexión|Se ha habilitado la eliminación de nombres de usuario de la lista anterior de nombres de usuario al presionar la tecla SUPR. Para obtener más información, consulte [Permitir la eliminación de usuarios de la ventana de inicio de sesión de SSMS](https://feedback.azure.com/forums/908035/suggestions/32897632).|
|Asistente para importación de DAC|Se ha corregido un problema que provocaba que el Asistente para importación de DAC no funcionara cuando se conectaba con AAD.|
|Clasificación de datos|Se ha corregido un problema que se producía al guardar clasificaciones en el panel de clasificación de datos mientras hay otros paneles de clasificación de datos abiertos en otras bases de datos.|
|Asistente para aplicaciones de capa de datos|Se ha corregido una incidencia debido a la cual el usuario no podía importar una aplicación de capa de datos (.dacpac) debido al acceso limitado al servidor (por ejemplo, falta de acceso a todas las bases de datos del mismo servidor).|
|Asistente para aplicaciones de capa de datos|Se ha corregido una incidencia que hacía que la importación fuera muy lenta si muchas bases de datos estaban hospedadas en el mismo servidor SQL Azure.|
|Tablas externas|Se ha agregado compatibilidad con Rejected_Row_Location de plantilla, SMO, IntelliSense y cuadrícula de propiedades.|
|Asistente para la importación de archivos planos|Se ha corregido un problema por el que el "Asistente para la importación de archivos planos" no trataba correctamente las comillas dobles (escape). Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/32897998](https://feedback.azure.com/forums/908035/suggestions/32897998). |
|Asistente para la importación de archivos planos|Se ha corregido una incidencia relacionada con el tratamiento incorrecto de tipos de número de punto flotante (en configuraciones regionales que usan un delimitador distinto en números de punto flotante).|
|Asistente para la importación de archivos planos|Se ha corregido un problema relacionado con la importación de bits cuando los valores son 0 o 1. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535). |
|Asistente para la importación de archivos planos|Se ha corregido una incidencia debido a la cual se especificaban elementos *float* como valores *NULL*.|
|Asistente para la importación de archivos planos|Se ha corregido un problema que evitaba que el Asistente para importación procesara valores decimales negativos.|
|Asistente para la importación de archivos planos|Se ha corregido un problema que evitaba que el asistente importara desde archivos CSV de una sola columna.|
|Asistente para la importación de archivos planos|estará en SSMS 17.9] Se ha corregido un incidencia por la que la importación de archivos planos no permitía cambiar la tabla de destino cuando la tabla ya existe. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186](https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186). |
|Visor de Ayuda|Lógica mejorada en torno al respeto de los modos en línea o sin conexión (aún puede haber algunas incidencias que deban solucionarse).|
|Visor de Ayuda|Se ha corregido la opción "Ver Ayuda" para que se respete la configuración de en línea/sin conexión. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791). |
|Alta disponibilidad y recuperación ante desastres<BR> Grupos de disponibilidad|Se ha corregido una incidencia que provocaba que los roles del "Asistente de Grupos de disponibilidad de conmutación por error" siempre se mostraran como "Resolviendo".|
|Alta disponibilidad y recuperación ante desastres<BR> Grupos de disponibilidad|Se ha corregido un problema que provocaba que SSMS mostrara advertencias truncadas en el "Panel de grupos de disponibilidad".|
|Integration Services (IS)|Se ha corregido una incidencia en paralelo por la que el Asistente para la implementación no se puede conectar a SQL Server si SQL Server 2019 y SSMS 18.0 están instalados en el mismo equipo.|
|Integration Services (IS)|Se ha corregido un problema que impedía editar una tarea de plan de mantenimiento al diseñar el plan de mantenimiento.|
|Integration Services (IS)|Se ha corregido una incidencia que provocaba el bloqueo del asistente para la implementación al cambiar el nombre del proyecto en la implementación.|
|Integration Services (IS)|Se ha habilitado la configuración del entorno en la característica de programación de Azure-SSIS IR.|
|Integration Services (IS)|Se ha corregido un problema que provocaba que el Asistente para la creación de un entorno de ejecución de integración de SSIS dejara de responder cuando la cuenta del cliente pertenecía a más de un inquilino.|
|Monitor de actividad de trabajo|Se ha corregido un bloqueo al usar el Monitor de actividad (con filtros).|
|Explorador de objetos|Se ha corregido una incidencia por la que SSMS generaba una excepción "No se puede convertir el objeto del tipo DBNull a otros tipos" al intentar expandir el nodo "Administración" del Explorador de objetos (configuración errónea de DataCollector).|
|Explorador de objetos|Se ha corregido un problema por el que el Explorador de objetos no incluía comillas de escape antes de invocar a "Editar las primeras...", lo que provocaba confusión en el diseñador.|
|Explorador de objetos|Se ha corregido un problema donde el asistente "Importar la aplicación de capa de datos" no se iniciaba desde el árbol de Azure Storage.|
|Explorador de objetos|Se ha corregido un problema en "Configuración de Correo electrónico de base de datos" que provocaba que no se conservara el estado de la casilla SSL. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541](https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541). |
|Explorador de objetos|Se ha corregido una incidencia por la que la opción de SSMS para cerrar las conexiones existentes se atenuaba al intentar restaurar la base de datos con is_auto_update_stats_async_on.|
|Explorador de objetos|Se ha corregido una incidencia en la que al hacer clic con el botón derecho en los nodos del Explorador de objetos (por ejemplo "Tablas") y querer realizar una acción como filtrar tablas mediante Filtro > Configuración de filtro, el formulario de configuración de filtro puede aparecer en la otra pantalla y no en la que SSMS está activo actualmente. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106](https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106). |
|Explorador de objetos|Se ha corregido un problema pendiente desde hace mucho tiempo por el que la tecla SUPR no funcionaba en el Explorador de objetos al intentar cambiar el nombre de un objeto. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/33073510](https://feedback.azure.com/forums/908035-sql-server/suggestions/33073510), [https://feedback.azure.com/forums/908035/suggestions/32910247](https://feedback.azure.com/forums/908035/suggestions/32910247) y otros elementos duplicados.|
|Explorador de objetos|Cuando se muestran las propiedades de los archivos de base de datos existentes, el tamaño aparece en una columna "Tamaño (MB)" en lugar de "Tamaño inicial (MB)", que es lo que se muestra al crear una base de datos. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32629024](https://feedback.azure.com/forums/908035-sql-server/suggestions/32629024). |
|Explorador de objetos|Se ha deshabilitado el elemento de menú contextual "Diseño" en "Tablas de Graph" ya que no existe ninguna compatibilidad con ese tipo de tablas en la versión actual de SSMS.|
|Explorador de objetos|Se ha corregido un problema que hacía que el cuadro de diálogo "Nueva programación de trabajo" no se representara correctamente en monitores con una configuración elevada de ppp. Para obtener detalles, vea [https://feedback.azure.com/admin/v3/suggestions/35541262](https://feedback.azure.com/admin/v3/suggestions/35541262). |
|Explorador de objetos|Se ha corregido y mejorado la forma de mostrar una incidencia de tamaño de base de datos ("Tamaño (MB)") en los detalles del Explorador de objetos: solo con dos dígitos decimales y formato con el separador de miles. Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/34379308](https://feedback.azure.com/forums/908035/suggestions/34379308).|
|Explorador de objetos|Se ha corregido una incidencia que hacía que la creación de un "índice espacial" produjera un error del tipo "Para realizar esta acción, establezca la propiedad PartitionScheme".|
|Explorador de objetos|Mejoras de rendimiento menores en el Explorador de objetos para evitar la emisión de consultas adicionales, siempre que sea posible.|
|Explorador de objetos|Se ha extendido la lógica para solicitar confirmación al cambiar el nombre de una base de datos a todos los objetos de esquema (se puede configurar el valor).|
|Explorador de objetos|Se han agregado secuencias de escape adecuadas en el filtrado del Explorador de objetos. Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/36678803](https://feedback.azure.com/forums/908035/suggestions/36678803). |
|Explorador de objetos|Se ha corregido y mejorado la vista de detalles del Explorador de objetos para mostrar los números con separadores adecuados. Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/32900944](https://feedback.azure.com/forums/908035/suggestions/32900944). |
|Explorador de objetos|Se ha corregido el menú contextual en el nodo de "Tablas" cuando se conecta a SQL Express, que provocaba que faltara el control flotante "Nuevo", las tablas de grafos se mostraran de forma incorrecta y faltara la tabla con versiones del sistema. Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/37245529](https://feedback.azure.com/forums/908035/suggestions/37245529). |
|Scripting de objetos|Mejoras de rendimiento general: se tarda la mitad de tiempo en generar scripts de WideWorldImporters en comparación con SSMS 17.7.|
|Scripting de objetos|Al crear objetos de scripting, se omite la configuración del ámbito de DB que tiene valores predeterminados.|
|Scripting de objetos|No se genera T-SQL dinámico al crear un scripting. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391). |
|Scripting de objetos|Se omite la sintaxis de gráfico "como borde" y "como nodo" en el scripting de una tabla en SQL Server 2016 y versiones anteriores.|
|Scripting de objetos|Se ha corregido una incidencia que provocaba un error de scripting de objetos de base de datos al conectarse a una Azure SQL DB mediante AAD con MFA.|
|Scripting de objetos|Se ha corregido un problema que producía un error al intentar incluir en un script un índice espacial con GEOMETRY_AUTO_GRID o GEOGRAPHY_AUTO_GRID en una instancia de Azure SQL DB.|
|Scripting de objetos|Se ha corregido una incidencia que provocaba que el scripting de una base de datos (esto es, una base de datos de Azure SQL) tuviera siempre como destino una instancia de SQL Server local, incluso si la configuración de scripting del "Explorador de objetos" se hubiera establecido para coincidir con el origen.|
|Scripting de objetos|Se ha corregido una incidencia que provocaba que, al intentar incluir en un script una tabla de una base de datos de SQL Data Warehouse con índices agrupados y no agrupados, se generaran instrucciones T-SQL incorrectas.|
|Scripting de objetos|Se ha corregido una incidencia que provocaba que, al intentar incluir en un script una tabla de una base de datos de SQL Data Warehouse con "Índices de almacén de columnas agrupados" e "Índices agrupados", se generaran instrucciones T-SQL incorrectas (duplicadas).|
|Scripting de objetos|Se ha corregido el scripting de tablas con particiones sin valores de rango (bases de datos de almacenamiento de datos de SQL).|
|Scripting de objetos|Se ha corregido una incidencia que provocaba que el usuario no pudiera incluir en un script una auditoría o una especificación de auditoría SERVER_PERMISSION_CHANGE_GROUP.|
|Scripting de objetos|Se corrige una incidencia que hacía que el usuario no pudiera incluir en un script estadísticas de SQL Data Warehouse. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897296](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897296). |
|Scripting de objetos|Se ha corregido una incidencia que provocaba que el "Asistente para generar scripts" mostrara la tabla incorrecta con un error de scripting cuando "Continuar scripting en caso de Error" se establece en false.|
|Scripting de objetos|Generación de scripts mejorada en SQL Server 2019.|
|Profiler|Se ha agregado el evento "Consulta de reescritura de tabla de agregado" a los eventos del generador de perfiles.|
|Almacén de datos de consultas|Se ha corregido un problema que producía que se pudiera iniciar una excepción "DocumentFrame (SQLEditors)".|
|Almacén de datos de consultas|Se ha corregido un problema por el que al intentar establecer un intervalo de tiempo personalizado en los informes de Almacén de consultas integrados, el usuario no podía seleccionar AM o PM en el intervalo de inicio o fin.|
|Cuadrícula de resultados|Se ha corregido un problema que se provocaba en el modo de contraste alto (números de línea seleccionados no visibles).|
|Cuadrícula de resultados|Se ha corregido una incidencia que provocaba una excepción de tipo "Índice fuera de rango" al hacer clic en la cuadrícula.|
|Cuadrícula de resultados|Se ha corregido un problema por el cual se omitía el color de fondo del resultado de la cuadrícula. Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/32895916](https://feedback.azure.com/forums/908035/suggestions/32895916). |
|ShowPlan|Las nuevas propiedades del operador de concesión de memoria no se muestran correctamente cuando hay más de un subproceso.|
|ShowPlan|Se han agregado los siguientes cuatro atributos en RunTimeCountersPerThread del plan XML de ejecución real: HpcRowCount (número de filas procesadas por dispositivo hpc), HpcKernelElapsedUs (espera de tiempo transcurrida para la ejecución del kernel en uso), HpcHostToDeviceBytes (bytes transferidos desde el host al dispositivo) y HpcDeviceToHostBytes (bytes transferidos desde el dispositivo al host).|
|ShowPlan|Se ha corregido una incidencia que provocaba que los nodos de plan parecidos se resaltaran en una posición incorrecta.|
|SMO|Se ha corregido un problema por el que SMO/ServerConnection no controlaba correctamente las conexiones basadas en SqlCredential. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941](https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941). |
|SMO|Se ha corregido un problema por el que una aplicación escrita con SMO podía encontrar un error si intentaba enumerar las bases de datos desde el mismo servidor en varios subprocesos, aunque usara instancias de SqlConnection independientes en cada uno.|
|SMO|Se ha corregido la regresión de rendimiento en la transferencia desde tablas externas.|
|SMO|Se ha corregido una incidencia en la seguridad para subprocesos de ServerConnection que hacía que SMO perdiera instancias de SqlConnection cuando tiene como destino Azure.|
|SMO|Se ha corregido una incidencia que provocaba un error StringBuilder.FormatError al intentar restaurar una base de datos que tenía llaves en su nombre.|
|SMO|Se ha corregido una incidencia por la cual las bases de datos de Azure en SMO aplicaban, de forma predeterminada, la intercalación sin distinguir entre mayúsculas y minúsculas para todas las comparaciones de cadenas en lugar de usar la intercalación especificada para la base de datos.|
|Editor de SSMS|Se ha corregido una incidencia en la que la "Tabla del sistema de SQL" al restaurar los colores predeterminados cambiaba el color a verde lima, y no al color verde predeterminado, lo que hacía difícil leerla sobre un fondo blanco. Para obtener más información, consulte [Restaurar el color predeterminado incorrecto para la Tabla del sistema de SQL](https://feedback.azure.com/forums/908035-sql-server/suggestions/32896906). La incidencia todavía persiste en versiones no inglesas de SSMS.|
|Editor de SSMS|Se ha corregido un problema por el que IntelliSense no funcionaba cuando se conectaba a Azure SQLDW con autenticación de AAD.|
|Editor de SSMS|Se ha corregido IntelliSense en Azure cuando el usuario carece de acceso a la base de datos **maestra**.|
|Editor de SSMS|Se han corregido fragmentos de código para crear "tablas temporales", que se interrumpieron cuando la intercalación de la base de datos de destino distinguía mayúsculas y minúsculas.|
|Editor de SSMS|Ahora IntelliSense reconoce la nueva función TRANSLATE. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898430](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898430). |
|Editor de SSMS|Se ha mejorado IntelliSense en la función integrada FORMAT. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898676](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898676). |
|Editor de SSMS|LAG y LEAD ahora se reconocen como funciones integradas. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898757](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898757). |
|Editor de SSMS|Se ha corregido una incidencia que hacía que IntelliSense generara una advertencia al usar "ALTER TABLE...ADD CONSTRAINT...WITH(ONLINE=ON)".|
|Editor de SSMS|Se corrigió una incidencia debido a la cual varias vistas del sistema y funciones de valores de tabla no se coloreaban correctamente.|
|Editor de SSMS|Se ha corregido una incidencia que podía causar que al hacer clic en las pestañas del editor la ficha se cerrara en lugar de obtener el foco. Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/37291114](https://feedback.azure.com/forums/908035/suggestions/37291114). |
|Opciones de SSMS|Se ha corregido un problema por el que la página **Herramientas** > **Opciones** > **Explorador de objetos de SQL Server** > **Comandos** no cambiaba de tamaño correctamente.|
|Opciones de SSMS|Ahora, SSMS deshabilitará de forma predeterminada la descarga automática de DTD en el editor de XMLA; el editor de scripts XMLA (que usa el servicio de lenguaje XML) evitará ahora de forma predeterminada que se descargue automáticamente la DTD para archivos xmla potencialmente malintencionados. Esto se controla mediante la desactivación del valor "Descargar automáticamente DTD y esquemas" en **Herramientas** > **Opciones** > **Entorno** > **Editor de texto** > **XML** > **Varios**.|
|Opciones de SSMS|Se ha restaurado **CTRL+D** para que sea el acceso directo como lo era en versiones anteriores de SSMS. Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/35544754](https://feedback.azure.com/forums/908035/suggestions/35544754). |
|Diseñador de tablas|Se ha corregido un bloqueo al "Editar 200 filas".|
|Diseñador de tablas|Se ha corregido un problema por el que se permitía al diseñador agregar una tabla cuando se estaba conectado a una instancia de Azure SQL Database.|
|Evaluación de vulnerabilidad|Se ha corregido una incidencia que provocaba que los resultados del análisis no se cargaran correctamente.|
|XEvent|Se han agregado dos columnas, "action_name" y "class_type_desc", que muestran los campos de identificador de acción y tipo de clase como cadenas legibles.|
|XEvent|Se ha quitado el límite de 1 000 000 eventos del Visor de XEvent.|
|Generador de perfiles XEvent|Se ha corregido un problema por el que el generador de perfiles XEvent no se podía iniciar cuando se estaba conectado a una instancia de SQL Server de 96 núcleos.|
|Visor de XEvent|Se ha corregido una incidencia que provocaba que el Visor de XEvent se bloqueara al intentar agrupar los eventos mediante las "Opciones de la barra de herramientas de eventos extendidos".|

### <a name="deprecated-and-removed-features-in-180"></a>Características en desuso y eliminadas en 18.0

Características de elementos en desuso y eliminados
- Depurador de T-SQL
- Diagramas de base de datos
- Las siguientes herramientas ya no se instalan con SSMS:
  - OSQL.EXE
  - DReplay.exe
  - SQLdiag.exe
  - SSBDiagnose.exe
  - bcp.exe
  - sqlcmd.exe
- Herramientas de Configuration Manager:
  - SQL Server Configuration Manager y Reporting Server Configuration Manager ya no forman parte del programa de instalación de SSMS.
- Directivas estándar de DMF
  - Las directivas ya no se instalan con SSMS. Se moverán a Git. Si quieren, los usuarios podrán colaborar y descargarlas/instalarlas.
- Se ha quitado la opción -P de la línea de comandos de SSMS
  - Por motivos de seguridad, se ha quitado la opción que permitía especificar contraseñas de texto no cifrado en la línea de comandos.
- Se ha eliminado Generar Scripts > Publicar en servicio web.
  - Esta característica en desuso se ha eliminado de la interfaz de usuario de SSMS.
- Se ha eliminado el nodo "Mantenimiento > Heredado" del Explorador de objetos.
  - Ya no se tendrá acceso a los nodos realmente antiguos "Plan de mantenimiento de bases de datos" y "SQL Mail". Los nodos modernos "Correo electrónico de base de datos" y "Planes de mantenimiento" seguirán funcionando con normalidad.

### <a name="known-issues-180"></a>Problemas conocidos (18.0)

- Podría detectar un problema al instalar la versión 18.0 consistente en la imposibilidad de ejecutar SQL Server Management Studio. Si detecta este problema, siga los pasos del artículo [SSMS2018 está instalado, pero no se ejecuta](https://feedback.azure.com/forums/908035-sql-server/suggestions/37502512-ssms2018-installed-but-will-not-run).

- Existe una limitación en el tamaño de los datos que ve en los resultados de SSMS que se muestran en la cuadrícula, el texto o el archivo.

## <a name="downloadssdtmediadownloadpng-ssms-1791httpsgomicrosoftcomfwlinklinkid2043154clcid0x409"></a>![descargar](../ssdt/media/download.png) [SSMS 17.9.1](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409)

- Número de versión: 17.9.1<br>
- Número de compilación: 14.0.17289.0<br>
- Fecha de publicación: 21 de noviembre de 2018

17.9.1 es una pequeña actualización de 17.9 con las correcciones de errores siguientes:

- Se ha corregido una incidencia que hace que la conexión de los usuarios se cierre y se vuelva a abrir con cada invocación de consulta cuando se usa la autenticación "Azure Active Directory: universal compatible con MFA" con el editor de consultas SQL. Entre los efectos secundarios del cierre de la conexión se incluyen tablas temporales globales que se quitan de forma inesperada y, a veces, la asignación de un SPID nuevo a la conexión.
- Se ha corregido un problema pendiente desde hace mucho tiempo por el que se producía un error al buscar un plan de restauración, o bien se generaba un plan de restauración ineficaz en determinadas condiciones.
- Se ha corregido una incidencia en el Asistente "para importar aplicaciones de capa de datos" que podía producir un error cuando se conectaba a una base de datos de Azure SQL.

> [!NOTE]
> Las versiones localizadas de SSMS 17.x en idiomas diferentes al inglés requieren el [paquete de actualización de seguridad KB 2862966](https://support.microsoft.com/kb/2862966) cuando se instalan en: Windows 8, Windows 7, Windows Server 2012 y Windows Server 2008 R2.

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40a)

## <a name="downloadssdtmediadownloadpng-ssms-1653httpsgomicrosoftcomfwlinklinkid840946"></a>![descargar](../ssdt/media/download.png) [SSMS 16.5.3](https://go.microsoft.com/fwlink/?LinkID=840946)
Disponible con carácter general | Número de compilación: 13.0.16106.4

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)

Se han corregido los problemas siguientes en esta versión:

* Se ha corregido una incidencia detectada en SSMS 16.5.2 que provocaba la expansión del nodo "Table" cuando la tabla tenía más de una columna dispersa.

* Los usuarios pueden implementar paquetes SSIS que contienen el Administrador de conexiones OData que se conectan a un recurso de Microsoft Dynamics AX/CRM Online en el catálogo de SSIS. Para más información, vea [Administrador de conexiones OData](../integration-services/connection-manager/odata-connection-manager.md).

* La configuración de Always Encrypted en una tabla existente produce errores en los objetos relacionados. [Id. de Connect 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* La Configuración de Always Encrypted para una base de datos existente con varios esquemas no funciona. [Id. de Connect 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* El Asistente para columnas cifradas de Always Encrypted produce un error debido a la base de datos que contiene vistas que hacen referencia a vistas del sistema. [Id. de Connect 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* Cuando se cifra mediante Always Encrypted, los errores al actualizar los módulos después del cifrado se tratan incorrectamente.

* El menú *Abrir recientes* no muestra los archivos guardados recientemente. [Id. de Connect 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* SSMS funciona con lentitud cuando se hace clic con el botón derecho en el índice de una tabla (a través de una conexión remota de Internet). [Id. de Connect 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)

* Se ha corregido un problema de la barra de desplazamiento del Diseñador de SQL. [Id. de Connect 3114856](https://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* El menú contextual de las tablas se bloquea momentáneamente. 
 
* En algunas ocasiones, SSMS produce excepciones en el Monitor de actividad y se bloquea. [Id. de Connect 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* SSMS 2016 se bloquea con error "El proceso terminó debido a un error interno en el runtime de .NET en la dirección IP 71AF8579 (71AE0000) con el código de salida 80131506".


## <a name="uninstall-and-reinstall-ssms-17x"></a>Desinstalación y reinstalación de SSMS 17.x

Si tiene algún problema con la instalación de SSMS que no se resuelve al instalarlo y volverlo a instalar, primero puede probar a [reparar](https://support.microsoft.com/help/4028054/windows-10-repair-or-remove-programs) Visual Studio 2015 IsoShell. Si el problema tampoco se resuelve al reparar Visual Studio 2015 IsoShell, pruebe los pasos que se indican a continuación, con los que se han podido resolver muchos problemas aleatorios:

1. Desinstale SSMS de la misma forma en que desinstalaría cualquier aplicación (con las opciones *Aplicaciones y características* o *Programas y características* en función de su versión de Windows).

2. Desinstale Visual Studio 2015 IsoShell **desde un símbolo del sistema con privilegios elevados**:

    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```

    ```vs_isoshell.exe /Uninstall /Force /PromptRestart```

3. Desinstale Microsoft Visual C++ 2015 Redistributable de la misma forma en que desinstalaría cualquier aplicación. Si están en el equipo, desinstale x86 y x64.

4. Vuelva a instalar Visual Studio 2015 IsoShell **desde un símbolo del sistema con privilegios elevados**:  

    ```PUSHD "C:\ProgramData\Package Cache\FE948F0DAB52EB8CB5A740A77D8934B9E1A8E301\redist"```  

    ```vs_isoshell.exe /PromptRestart```

5. Vuelva a instalar SSMS.

6. Actualice a la [versión más reciente de Visual C++ 2015 Redistributable](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads) si todavía no lo ha hecho.

## <a name="additional-downloads"></a>Descargas adicionales

Para obtener una lista de todas las descargas de SQL Server Management Studio, consulte el [Centro de descargas de Microsoft](https://www.microsoft.com/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending).  
  
Para obtener la versión más reciente de SQL Server Management Studio, vea [Descargar SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
