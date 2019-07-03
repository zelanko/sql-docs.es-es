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
manager: craigg
ms.custom: ''
ms.date: 06/12/2019
ms.openlocfilehash: 0be9bae60c46aa43c6f0acb5de5204d33a318450
ms.sourcegitcommit: 65ceea905030582f8d89e75e97758abf3b1f0bd6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2019
ms.locfileid: "67399671"
---
# <a name="release-notes-for-sql-server-management-studio-ssms"></a>Notas de la versión de SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

En este artículo, se proporcionan detalles sobre las actualizaciones, mejoras y correcciones de errores de las versiones actuales y anteriores de SSMS.

<!--
The latest ## H2 section of this Release Notes article has been reformatted to match the new standard.
The new standard replaces the use of bullet lists with the 2-column markdown table format.
Please use the new 2-column table format going forward.
And please do include the final blank row of "| &nbsp;| &nbsp;|".

The ## H2 titles are also being shortened, by the removal of unnecessary repetitive strings.
In this case, "## SSMS 17.9" is being shortened to "## 17.9" (as one standard actual example).
And we are appending the 'Month yyyy'.

Also, this file has been renamed to the new standard, which calls for the file name to be with "release-notes-[techAreaName].md".
The old name for this file was 'sql-server-management-studio-changelog-ssms.md'.
But today the new file name is 'release-notes-ssms.md' (still in 'docs/ssms/').

Thank you.
GeneMi. 2019/04/02.
-->

## <a name="ssms-181"></a>SSMS 18.1

Descargar: &nbsp; &nbsp; [Descargar SSMS 18.1](download-sql-server-management-studio-ssms.md)<br/>
Número de compilación: &nbsp; &nbsp; 15.0.18131.0<br/>
Fecha de publicación: &nbsp; &nbsp; 11 de junio de 2019

SSMS 18.1 es la versión de disponibilidad general (GA) más reciente de SSMS. Si necesita una versión anterior de SSMS, consulte [versiones de SSMS anteriores](release-notes-ssms.md#previous-ssms-releases).

18.1 es una pequeña actualización de 18.0 con los nuevos elementos y las correcciones de errores siguientes.

## <a name="whats-new-in-181"></a>Novedades de 18.1

| Nuevo elemento| Detalles|
| :-------| :------|
| Diagramas de base de datos | [Los diagramas de base de datos se han vuelto a agregar a SSMS](https://feedback.azure.com/forums/908035/suggestions/37507828).
| SSBDIAGNOSE.EXE |Diagnose de SQL Server (herramienta de línea de comandos) se ha vuelto a agregar al paquete SSMS.|
| Integration Services (SSIS) | Compatibilidad para la programación del paquete SSIS, ubicado en el catálogo de SSIS en Azure o el sistema de archivos de Azure. Existen tres entradas para iniciar el cuadro de diálogo Nueva programación, el elemento de menú *Nueva programación…* que se muestra al hacer clic con el botón derecho en el paquete SSIS en el catálogo de SSIS en Azure, el elemento de menú *Programe el paquete SSIS* del elemento de menú *Migrar a Azure* en el elemento de menú *Herramientas* y "Schedule SSIS in Azure" (Programación de SSIS en Azure), que se muestra al hacer clic con el botón derecho en la carpeta Trabajos en el Agente SQL Server de Instancia administrada de Azure SQL Database.|

## <a name="bug-fixes-in-181"></a>Correcciones de errores en 18.1

| Nuevo elemento | Detalle |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Accesibilidad | Mejora de la accesibilidad de la interfaz de usuario de trabajo del agente. |
| Accesibilidad | Se ha mejorado la accesibilidad en la página de supervisión de Stretch al agregar un nombre accesible para el botón *Actualizar automáticamente* y, además, un nombre accesible inteligente que va a ayudar a los usuarios a saber no solo en qué botón se encuentran, sino también el efecto de presionarlo. |
| Integración de ADS| Se ha corregido un posible bloqueo en SSMS al intentar usar los servidores registrados de ADS.|
| Diseñador de bases de datos | Se ha agregado compatibilidad con la intercalación Latin1_General_100_BIN2_UTF8 (disponible en SQL Server 2019 CTP 3.0) |
| Clasificación de datos | Se evita la adición de etiquetas de confidencialidad a las columnas de la tabla de historial, que no se admite. |
| Clasificación de datos | Se ha solucionado un problema relacionado con el tratamiento incorrecto del nivel de compatibilidad (servidor frente a base de datos). |
| Diseñador de bases de datos | Se ha agregado compatibilidad con la intercalación Latin1_General_100_BIN2_UTF8 (disponible en SQL2019 CTP 3.0). |
| SSMS general | Se ha corregido un problema consistente en que el scripting de pseudocolumnas de un índice era incorrecto. |
| SSMS general | Se ha corregido un problema en la página Propiedades de inicio de sesión consistente en que al hacer clic en el botón *Agregar credencial* se podía producir una excepción de referencia nula. |
| SSMS general | Se ha corregido la visualización del tamaño de la columna money en la página de propiedades del índice. |
| SSMS general | Se ha corregido un problema consistente en que SSMS no respetaba la configuración de Intellisense de *Herramientas/Opciones* en la ventana del editor SQL. |
| SSMS general | Se ha corregido un problema consistente en que SSMS no respetaba la configuración de la Ayuda (en línea frente a sin conexión). |
| Configuración elevada de ppp | Se ha corregido el diseño de los controles de los cuadros de diálogo de error de las opciones de consulta no admitidas. |
| Configuración elevada de ppp | Se ha corregido el diseño de los controles de la página *Nuevo grupo de disponibilidad* en alguna versión localizada de SSMS. |
| Configuración elevada de ppp | Se ha corregido el diseño de la página *Nueva programación de trabajo*. Vea el [foro de comentarios](https://feedback.azure.com/forums/908035/suggestions/37632094) para obtener más detalles. |
| Importación de archivo plano | Se ha corregido un problema consistente en que las filas podrían perderse silenciosamente durante la importación.|
| Intellisense/editor | Se ha reducido el tráfico de las consultas basadas en SMO a las bases de datos de Azure SQL para Intellisense. |
| Intellisense/editor | Se ha corregido un error gramatical en la información sobre herramientas mostrada al escribir T-SQL para crear un usuario. Además, se ha corregido el mensaje de error para eliminar la ambigüedad entre usuarios e inicios de sesión. |
| Visor de registros | Se ha corregido un problema consistente en que SSMS siempre abre el registro del servidor actual (o agente), incluso si se hace doble clic en un inicio de sesión de archivo anterior en el Explorador de objetos. Vea el [foro de comentarios](https://feedback.azure.com/forums/908035/suggestions/37633648) para obtener más detalles. |
| Programa de instalación de SSMS | Se ha corregido el problema que hacía que el programa de instalación SSMS generara un error cuando la ruta de acceso del registro de instalación contenía espacios. Vea el [foro de comentarios](https://feedback.azure.com/forums/908035/suggestions/37496110) para obtener más detalles. |
| Programa de instalación de SSMS | Se ha corregido un problema consistente en que SSMS salía inmediatamente después de mostrar la pantalla de presentación. </br> Vea estos sitios para obtener más detalles: [foro de comentarios](https://feedback.azure.com/forums/908035/suggestions/37502512), [SSMS no se inicia](https://dba.stackexchange.com/questions/238609/ssms-refuses-to-start) y [Administradores de base de datos](https://dba.stackexchange.com/questions/237086/sql-server-management-studio-18-wont-open-only-splash-screen-pops-up). |
| Explorador de objetos | Se ha eliminado la restricción sobre la habilitación de *iniciar PowerShell* al conectarse a SQL en Linux. |
| Explorador de objetos | Se ha corregido un problema que hacía que SSMS se bloquease al intentar expandir el nodo Polybase/Grupo de escalado horizontal (al conectarse a un nodo de proceso). |
| Explorador de objetos | Se ha corregido un problema consistente en que el elemento de menú *Deshabilitado* todavía estaba habilitado incluso después de deshabilitar un índice determinado. Vea el [foro de comentarios](https://feedback.azure.com/forums/908035/suggestions/37735375) para obtener más detalles. |
| Informes | Se ha corregido un informe para mostrar realmente GrantedQueryMemory en KB (informe del panel de rendimiento de SQL). Vea el [foro de comentarios](https://feedback.azure.com/forums/908035/suggestions/37167289) para obtener más detalles. |
| Informes | Se ha mejorado el seguimiento del bloque de registro en escenarios de Always-On. |
| ShowPlan | Se ha agregado un nuevo elemento de plan de presentación *SpillOccurred* al esquema de plan de presentación. |
| ShowPlan | Se han agregado lecturas remotas (*ActualPageServerReads*, *ActualPageServerReadAheads*, *ActualLobPageServerReads*, *ActualLobPageServerReadAheads* ) al esquema del plan de presentación. |
| SMO/scripting | Se evita la consulta de restricciones perimetrales durante el scripting de tablas que no son de grafos. |
| SMO/scripting | Se ha eliminado la restricción sobre la clasificación de confidencialidad al generar scripts de columnas con *Clasificación de datos*. |
| SMO/scripting | Se ha corregido un problema consistente en que "Generar script" en una tabla de grafos produce un error al generar datos. Vea el [foro de comentarios](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898466) para obtener más detalles. |
| SMO/scripting | Se ha corregido un problema consistente en que el método EnumObjects() no capturaba el nombre de esquema de un sinónimo. |
| SMO/scripting | Se ha corregido un problema en UIConnectionInfo.LoadFromStream() consistente en que la sección *AdvancedOptions* no se leía (cuando no se especificaba una contraseña). |
| Agente SQL | Se ha corregido un problema que hacía que SSMS se bloqueara al trabajar con una ventana Propiedades del trabajo. Vea el [foro de comentarios](https://feedback.azure.com/forums/908035/suggestions/37164244) para obtener más detalles. |
| Agente SQL | Se ha corregido un problema consistente en que el botón "Ver" de *Propiedades de paso de trabajo* no siempre estaba habilitado, lo que evitaba la visualización de la salida de un paso de trabajo determinado. |
| Interfaz de usuario de XEvent | Se ha agregado una columna "Paquete" a la lista de XEvents para eliminar la ambigüedad de los eventos con nombres idénticos. |
| Interfaz de usuario de XEvent | Se ha agregado una asignación de tipo de clase "EXTERNAL LIBRARY" que faltaba a XEventUI. |

### <a name="known-issues-181"></a>Problemas conocidos (18.1)

- Es posible que se muestre un error a los usuarios al arrastrar un objeto de tabla del Explorador de objetos al Editor de consultas. Somos conscientes del problema y la corrección está prevista para la próxima versión.

- Las opciones de color *Conexiones de grupo* y *Conexiones de servidor único* en Opciones -> Editor de texto -> Pestaña de editor y barra de estado -> Diseño y colores de la barra de estado no se conservan después de cerrar SSMS 18.1. Al volver a abrir SSMS, la opción Diseño y colores de la barra de estado vuelve al valor predeterminado (blanco).

## <a name="previous-ssms-releases"></a>Versiones de SSMS anteriores

Para descargar las versiones anteriores de SSMS, haga clic en los vínculos de título de las secciones siguientes:

## <a name="downloadssdtmediadownloadpng-ssms-180httpsgomicrosoftcomfwlinklinkid2088649"></a>![descargar](../ssdt/media/download.png) [SSMS 18.0](https://go.microsoft.com/fwlink/?linkid=2088649)

- Número de versión: 18.0<br>
- Número de compilación: 15.0.18118.0<br>
- Fecha de publicación: 24 de abril de 2019

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=2088649&clcid=0x40a)

### <a name="whats-new-in-180"></a>Novedades de 18.0

| Nuevo elemento| Detalles|
| :-------| :------|
|Compatibilidad con SQL Server 2019|SSMS 18.0 es la primera versión de este producto que es totalmente *compatible* con SQL Server 2019 (compatLevel 150).|
|Compatibilidad con SQL Server 2019|Es compatible con "BATCH_STARTED_GROUP" y "BATCH_COMPLETED_GROUP" en SQL Server 2019 e Instancia administrada de SQL Database.|
|Compatibilidad con SQL Server 2019|SMO: se añade compatibilidad para la Inserción de UDF.|
|Compatibilidad con SQL Server 2019|GraphDB: se agrega marca en el plan de presentación para Graph TC Sequence.|
|Compatibilidad con SQL Server 2019|Always Encrypted: se ha agregado compatibilidad para AEv2 / Enclave.|
|Compatibilidad con SQL Server 2019|Always Encrypted: el cuadro de diálogo de conexión presenta una nueva pestaña "Always Encrypted" cuando el usuario hace clic en el botón "Opciones" para habilitar o configurar la compatibilidad de enclave.|
|Tamaño de descarga SSMS más pequeño| El tamaño actual es de unos 500 MB, aproximadamente la mitad del conjunto de SSMS 17.x.
|SSMS Se basa en el shell aislado de Visual Studio 2017|El nuevo shell (SSMS se basa en Visual Studio 2017 15.9.11) desbloquea todas las correcciones de accesibilidad que se han incluido en SSMS y Visual Studio e incluye las correcciones de seguridad más recientes.|
|Mejoras de accesibilidad de SSMS| Se ha realizado un gran esfuerzo para resolver las incidencias de accesibilidad en todas las herramientas (SSMS, DTA y Profiler).|
|Ahora puede instalarse SSMS en una carpeta personalizada.| Esta opción está disponible desde la línea de comandos (útil para la instalación desatendida) y la configuración de la interfaz de usuario. Desde la línea de comandos, pase este argumento adicional a SSMS-Setup-ENU.exe:<br> SSMSInstallRoot=C:\MySSMS18<br> De forma predeterminada, la nueva ubicación de instalación para SSMS es la siguiente: %ProgramFiles(x86)%\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe.<br>Esto no significa que SSMS sea de instancias múltiples.|
|SSMS permite instalar en un idioma distinto del sistema operativo.|Se ha suprimido el bloque en la configuración de idiomas mixtos. Por ejemplo, puede instalar SSMS en alemán en un Windows en francés. Si el idioma del sistema operativo no coincide con el idioma de SSMS, el usuario debe cambiar el idioma en **Herramientas** > **Opciones** > **Configuración internacional**. En caso contrario, SSMS mostrará la interfaz de usuario en inglés.|
|SSMS ya no comparte componentes con el motor SQL.|Se ha realizado un gran esfuerzo para evitar compartir componentes con el motor SQL, lo que a menudo daba lugar a incidencias de servicio (uno sobrescribía los archivos instalados por el otro).|
|SSMS requiere NetFx 4.7.2 o posterior|Hemos actualizado nuestros requisitos mínimos de NetFx4.6.1 a NetFx4.7.2: esto nos permite aprovechar las ventajas de la nueva funcionalidad expuesta en el nuevo marco.|
|Capacidad de migrar la configuración de SSMS| Cuando SSMS 18 se inicia por primera vez, se le pide al usuario que migre la configuración de la versión 17.x. Los archivos de configuración de usuario ahora se almacenan como un archivo XML sin formato, de este modo mejora la portabilidad y, posiblemente, permite la edición.|
|Compatibilidad con la configuración elevada de PPP| La configuración elevada de PPP está habilitada de manera predeterminada.|
|SSMS se entrega con el controlador OLE DB de Microsoft.| Para obtener más detalles, consulte [Descarga del controlador Microsoft OLE DB para SQL Server](https://docs.microsoft.com/sql/connect/oledb/download-oledb-driver-for-sql-server).|
|SSMS no se admite en Windows 8. Windows 10 y Windows Server 2016 requieren la versión 1607 (10.0.14393) o posterior.|Debido a la nueva dependencia de NetFx 4.7.2, SSMS 18.0 no se instala en Windows 8 ni en las versiones antiguas de Windows 10 y Windows Server 2016. La configuración de SSMS se bloqueará en esos sistemas. Windows 8.1 sigue siendo compatible.|
|SSMS ya no se agrega a la variable de entorno PATH.|La ruta de acceso a SSMS.EXE (y las herramientas en general) ya no se agrega más a la ruta de acceso. Los usuarios pueden agregarla de forma manual o, si se encuentran en un equipo moderno de Windows, usar el menú Inicio.|
|Los identificadores de paquete ya no tienen que desarrollar extensiones de SSMS.| En el pasado, SSMS cargaba selectivamente solo los paquetes conocidos, lo que requería que los desarrolladores registrasen sus propios paquetes. Este ya no es el caso.|
|SSMS general|Se expone la opción de configuración AUTOGROW_ALL_FILES para grupos de archivos en SSMS.|
|SSMS general|Se han eliminado las opciones con riesgo "agrupación ligera" y "aumento de prioridad" de la interfaz gráfica de usuario de SSMS. Para obtener más información, consulte [Detalles de aumento de prioridad y por qué no se recomienda](https://blogs.msdn.microsoft.com/arvindsh/2010/01/26/priority-boost-details-and-why-its-not-recommended/).
|SSMS general|Nuevos enlaces de teclado y menú para crear archivos **CTRL+ALT+N**. Se mantiene **CTRL+N** para crear una consulta.|
|SSMS general|Ahora el cuadro de diálogo **Nueva regla de firewall** permite al usuario especificar un nombre de regla, en lugar de generar uno de forma automática en nombre del usuario.|
|SSMS general|Mejora de IntelliSense en el editor, especialmente para la v140 de T-SQL y versiones posteriores.|
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
|Compatibilidad con Azure SQL| Se ha agregado compatibilidad con las SKU de núcleos virtuales (De uso general y Crítico para la empresa): Gen4_24 y la serie Gen5 completa.|
|Instancia administrada de Azure SQL|Se han agregado "Inicios de sesión de AAD" como nuevo tipo de inicio de sesión de SMO y SSMS cuando se conecta a una instancia administrada de Azure SQL.|
|AlwaysOn|Se recombinan RTO (tiempo de recuperación estimado) y RPO (pérdida de datos estimada) en el panel Always On de SSMS. Vea la documentación actualizada en [https://docs.microsoft.com/sql/database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups](../database-engine/availability-groups/windows/monitor-performance-for-always-on-availability-groups.md).|
|Always Encrypted| La casilla Habilitar Always Encrypted de la pestaña Always Encrypted del cuadro de diálogo Conectar con el servidor ofrece ahora una manera fácil de habilitar y deshabilitar Always Encrypted para una conexión de base de datos.|
|Always Encrypted con enclaves seguros| Se han realizado varias mejoras para admitir Always Encrypted con enclaves seguros en la versión preliminar de SQL Server 2019:<br>Un campo de texto para especificar la dirección URL de atestación de enclave en el cuadro de diálogo Conectar con el servidor (nueva pestaña Always Encrypted).<br>La nueva casilla del cuadro de diálogo Nueva clave maestra de columna para controlar si una nueva clave maestra de columna permite cálculos de enclave.<br>Otros cuadros de diálogo de administración de claves de Always Encrypted exponen ahora la información sobre qué claves maestras de columna permiten cálculos de enclave.|
|Archivos de auditoría|Se ha cambiado el método de autenticación basada en Clave de cuenta de almacenamiento a autenticación basada en AD Azure.|
|Archivos de auditoría|Se ha actualizado la lista de las acciones de auditoría conocidas para incluir FEATURE RESTRICTION ADD/CHANGE GROUP/DROP.|
|Clasificación de datos| Se ha reorganizado el menú de tareas de clasificación de datos: se ha agregado un submenú al menú de tareas de base de datos y una opción para abrir el informe desde el menú sin tener que abrir primero la ventana de clasificación de datos.|
|Clasificación de datos|Se ha agregado la nueva característica "Clasificación de datos" a SMO. El objeto de columna expone propiedades nuevas: SensitivityLabelName, SensitivityLabelId, SensitivityInformationTypeName, SensitivityInformationTypeId e IsClassified (de solo lectura). Para obtener más información, consulte [ADD SENSITIVITY CLASSIFICATION (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/add-sensitivity-classification-transact-sql)|
|Clasificación de datos|Se ha agregado el elemento de menú "Informe de clasificación" al control flotante "Clasificación de datos".|
|Clasificación de datos| Recomendaciones actualizadas.|
|Actualización del nivel de compatibilidad de la base de datos|Se ha agregado una opción nueva en **<Database name>**  > **Tareas** > **Actualizar base de datos**. Esta opción iniciará el nuevo **Asistente para la optimización de consultas (QTA)** que guía a los usuarios a través de los procesos siguientes:<br>Recopilación de una línea de base de rendimiento antes de actualizar el nivel de compatibilidad de la base de datos.<br>Actualización al nivel de compatibilidad de la base de datos deseado.<br>Recopilación de un segundo paso de datos de rendimiento a través de la misma carga de trabajo.<br>Detección de regresiones de carga de trabajo y proporcionar recomendaciones comprobadas para mejorar el rendimiento de la carga de trabajo.<br>Esto es similar al proceso de actualización de base de datos documentado en [escenarios de uso del almacén de consultas](https://docs.microsoft.com/sql/relational-databases/performance/query-store-usage-scenarios#CEUpgrade), excepto el último paso donde QTA no se basa en un estado correcto conocido previamente para generar las recomendaciones.|
|Asistente para aplicaciones de capa de datos|Se ha agregado compatibilidad para importar o exportar la aplicación de capa de datos con tablas de grafos.|
|Asistente para la importación de archivos planos|Se ha agregado lógica para notificar al usuario que una importación puede haber producido un cambio de nombre de las columnas.|
|Integration Services (SSIS)|Se ha agregado compatibilidad para permitir que los clientes programen paquetes SSIS en los Azure-SSIS IR que están en la nube de Azure Government.|
|Integration Services (SSIS)|Cuando se usa el Agente SQL de Instancia administrada de Azure SQL mediante SSMS, se puede configurar el administrador de conexiones y parámetros en el paso de trabajo de agente SSIS.|
|Integration Services (SSIS)|Al conectarse a Azure SQL DB o Instancia administrada, se puede conectar con la opción *predeterminada* como base de datos inicial.|
|Integration Services (SSIS)|Se ha agregado un nuevo elemento de entrada **Probar SSIS en Azure Data Factory** en el nodo "Catálogos de Integration Services", que se puede usar para iniciar el "Asistente para la creación de un entorno de ejecución de integración" y crear de forma rápida "Azure-SSIS Integration Runtime".
|Integration Services (SSIS)|Se ha agregado un botón **Create SSIS IR** (Crear entorno de ejecución de integración de SSI) a "Catalog Creation Wizard" (Asistente para crear catálogos), que se puede usar para iniciar el "Asistente para la creación de un entorno de ejecución de integración" y crear de forma rápida "Azure-SSIS Integration Runtime".|
|Integration Services (SSIS)|ISDeploymentWizard ahora admite autenticación SQL, autenticación integrada de Azure Active Directory y autenticación de contraseña de Azure Active Directory en el modo de línea de comandos.|
|Integration Services (SSIS)|El Asistente para la implementación ahora admite la creación y la implementación en SSIS Integration Runtime en Azure Data Factory.|
|Scripting de objetos|Se han agregado elementos de menú nuevos para "CREATE OR ALTER" al generar scripts de objetos.|
|Almacén de consultas|Se ha mejorado la facilidad de uso de algunos informes (Consumos de recursos globales) mediante la adición del separador de miles a los números que aparecen en el eje Y de los gráficos.|
|Almacén de consultas|Se ha agregado un nuevo informe de estadísticas de espera de consulta.|
|Almacén de consultas|Se ha agregado la métrica "Recuento de ejecuciones" a la vista "Consulta con seguimiento".|
|Herramientas de replicación|Se ha agregado compatibilidad para la característica de especificación de puerto no predeterminado en el Monitor de replicación y SSMS.|
|ShowPlan|Se han agregado filas estimadas frente a reales en el tiempo real transcurrido en el nodo de operadores de plan de presentación si están disponibles. Esto hará que el plan real tenga una apariencia coherente con el plan de estadísticas de consulta activa.|
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
|Evaluación de vulnerabilidad|Se cambia el conjunto de reglas de evaluación de vulnerabilidades que se ejecuta en servidores de Instancia administrada de Azure SQL para que los resultados del examen de evaluación de vulnerabilidades sean coherentes con los de Azure SQL DB.|
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
|Bloqueos|Se ha corregido un bloqueo al seleccionar "Informes" en el Explorador de objetos que se podía manifestar en conexiones de alta latencia o en la no accesibilidad temporal de los recursos.|
|Bloqueos|Se ha corregido un bloqueo en SSMS cuando se intenta usar el Servidor de administración central y los servidores de Azure SQL. Para obtener más información, consulte [Error y bloqueo de la aplicación SSMS 17.5 cuando se usa el Servidor de administración central](https://feedback.azure.com/forums/908035/suggestions/33374884).|
|Bloqueos|Se ha corregido un bloqueo en el Explorador de objetos mediante la optimización de la manera de recuperar la propiedad IsFullTextEnabled.|
|Bloqueos|Se ha corregido un error en el "Asistente para copiar bases de datos" al evitar la compilación de consultas innecesarias para recuperar propiedades de la base de datos.|
|Bloqueos|Se ha corregido una incidencia que provocaba que SSMS diera error o se bloqueara al editar T-SQL.|
|Bloqueos|Se ha mitigado una incidencia que hacía que SSMS dejara de responder al editar scripts de T-SQL grandes.|
|Bloqueos|Se ha corregido una incidencia que provocaba que SSMS se quedara sin memoria cuando se trataban los grandes conjuntos de datos que devolvían las consultas.|
|SSMS general|Se ha corregido un problema consistente en que "ApplicationIntent" no se pasaba en las conexiones en "Servidores registrados".|
|SSMS general|Se ha corregido un problema consistente en que el formulario "Nueva interfaz de usuario del asistente de sesión de XEvent" no se representaba correctamente en monitores con una configuración elevada de ppp.|
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
|Azure SQL: compatibilidad general|Se ha corregido un problema en el control común de la interfaz de usuario de Azure al enumerar suscripciones que podían generar un error "El índice estaba fuera del intervalo. Debe ser un valor no negativo e inferior al tamaño de la colección." cuando el usuario no tenía suscripciones en algunos inquilinos. Por ejemplo, el usuario podría encontrarse este error al intentar restaurar una copia de seguridad desde una dirección URL.|
|Azure SQL: compatibilidad general|Se ha corregido una incidencia por la que los objetivos de nivel de servicio estaban codificados, lo que dificultaba la compatibilidad de SSMS con nuevos SLO de Azure SQL. Ahora el usuario puede iniciar sesión en Azure y permitir a SSMS recuperar todos los datos de SLO aplicables (edición y tamaño máximo).|
|Compatibilidad con Instancia administrada de Azure SQL DB|Se ha mejorado/perfeccionado la compatibilidad con instancias administradas: se han deshabilitado opciones no admitidas en la interfaz de usuario y una corrección a la opción Ver registros de auditoría para controlar la dirección URL de destino de auditoría.|
|Compatibilidad con Instancia administrada de Azure SQL DB|El asistente para "generar y publicar scripts" crea scripts de cláusulas CREATE DATABASE no admitidas.|
|Compatibilidad con Instancia administrada de Azure SQL DB|Habilite las estadísticas de consultas activas para instancias administradas.|
|Compatibilidad con Instancia administrada de Azure SQL DB|Propiedades de la base de datos -> Archivos incluía un scripting ALTER DB ADD FILE incorrecto.|
|Compatibilidad con Instancia administrada de Azure SQL DB|Se ha corregido la regresión con el programador del servicio Agente SQL por la que se elegía la programación ONIDLE aunque se hubiera elegido algún otro tipo de programación.|
|Compatibilidad con Instancia administrada de Azure SQL DB|Se han ajustado MAXTRANSFERRATE y MAXBLOCKSIZE para realizar copias de seguridad en Azure Storage.|
|Compatibilidad con Instancia administrada de Azure SQL DB|Se ha solucionado el problema por el que el script de la copia de seguridad de registros final se creaba antes de la operación RESTORE (esto no se admite en CL).|
|Compatibilidad con Instancia administrada de Azure SQL DB|El asistente para crear bases de datos no creaba correctamente el scripting de la instrucción CREATE DATABASE.|
|Compatibilidad con Instancia administrada de Azure SQL DB|Tratamiento especial de paquetes SSIS en SSMS cuando se conecta a instancias administradas.|
|Compatibilidad con Instancia administrada de Azure SQL DB|Se ha corregido un problema por el que se mostraba un error al intentar usar el "Monitor de actividad" cuando se estaba conectado a instancias administradas.|
|Compatibilidad con Instancia administrada de Azure SQL DB|Compatibilidad mejorada para los inicios de sesión de AAD (en el Explorador de SSMS).|
|Compatibilidad con Instancia administrada de Azure SQL DB|Se ha mejorado el scripting de los objetos de grupos de archivos de SMO.|
|Compatibilidad con Instancia administrada de Azure SQL DB|Se ha mejorado la interfaz de usuario para las credenciales.|
|Compatibilidad con Instancia administrada de Azure SQL DB|Se ha agregado compatibilidad para la replicación lógica.|
|Compatibilidad con Instancia administrada de Azure SQL DB|Se ha corregido una incidencia que provocaba un error al hacer clic con el botón secundario en una base de datos y al seleccionar "Importar la aplicación de capa de datos".|
|Compatibilidad con Instancia administrada de Azure SQL DB|Se ha corregido una incidencia que provocaba que se mostraran errores al hacer clic con el botón secundario en una "TempDB".|
|Compatibilidad con Instancia administrada de Azure SQL DB|Se ha corregido una incidencia que provocaba que al intentar el scripting de la instrucción ALTER DB ADD FILE de SMO, se generara un script T-SQL vacío.|
|Compatibilidad con Instancia administrada de Azure SQL DB|Se ha mejorado la visualización de las propiedades específicas de servidor de Instancia administrada (generación de hardware, nivel de servicio, almacenamiento usado y reservado).|
|Compatibilidad con Instancia administrada de Azure SQL DB|Se ha corregido un problema que provocaba que el scripting de una base de datos ("Crear script como CREATE...") no generara scripts de grupos de archivos y archivos adicionales. Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/37326799](https://feedback.azure.com/forums/908035/suggestions/37326799). |
|Realizar copia de seguridad/restaurar/adjuntar/desasociar una base de datos|Se ha corregido un problema por el que el usuario no podía adjuntar una base de datos cuando el nombre de archivo físico del archivo .mdf no coincide con el nombre de archivo original.|
|Realizar copia de seguridad/restaurar/adjuntar/desasociar una base de datos|Se ha corregido un problema por el que era posible que SSMS no encontrase un plan de restauración válido o encontrase uno que fuera poco óptimo. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897752). |
|Realizar copia de seguridad/restaurar/adjuntar/desasociar una base de datos|Se ha corregido un problema que provocaba que el asistente "Adjuntar base de datos" no mostrara los archivos secundarios cuyo nombre se hubiera cambiado. Ahora se muestra el archivo y se agrega un comentario sobre él (por ejemplo, "No se ha encontrado"). Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/32897434](https://feedback.azure.com/forums/908035/suggestions/32897434). |
|Asistente para copiar bases de datos|No se fuerza la activación de ansi_padding cuando los asistentes para copiar bases de datos, generar scripts y realizar transferencias intentan crear una tabla con una tabla en memoria.|
|Asistente para copiar bases de datos|Los asistentes para copiar bases de datos y para la tarea Transferir bases de datos se han interrumpido en SQL Server 2017 y SQL Server 2019.|
|Asistente para copiar bases de datos|Los asistentes para copiar bases de datos, para generar scripts y para transferencias incluyen en un script la creación de la tabla antes de crear el origen de datos externo asociado.|
|Cuadro de diálogo de conexión|Se ha habilitado la eliminación de nombres de usuario de la lista anterior de nombres de usuario al presionar la tecla SUPR. Para obtener más información, consulte [Permitir la eliminación de usuarios de la ventana de inicio de sesión de SSMS](https://feedback.azure.com/forums/908035/suggestions/32897632).|
|Asistente para importación de DAC|Se ha corregido un problema que provocaba que el Asistente para importación de DAC no funcionara cuando se conectaba con AAD.|
|Clasificación de datos|Se ha corregido un problema que se producía al guardar clasificaciones en el panel de clasificación de datos mientras hay otros paneles de clasificación de datos abiertos en otras bases de datos.|
|Asistente para aplicaciones de capa de datos|Se ha corregido un problema por el cual el usuario no podía importar una aplicación de capa de datos (.dacpac) debido al acceso limitado al servidor (por ejemplo, falta de acceso a todas las bases de datos en el mismo servidor).|
|Asistente para aplicaciones de capa de datos|Se ha corregido un problema que hacía que la importación fuera muy lenta si muchas bases de datos estaban hospedadas en el mismo servidor SQL Azure.|
|Tablas externas|Se ha agregado compatibilidad con Rejected_Row_Location de plantilla, SMO, IntelliSense y cuadrícula de propiedades.|
|Asistente para la importación de archivos planos|Se ha corregido un problema por el que el "Asistente para la importación de archivos planos" no trataba correctamente las comillas dobles (escape). Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/32897998](https://feedback.azure.com/forums/908035/suggestions/32897998). |
|Asistente para la importación de archivos planos|Se ha corregido una incidencia relacionada con el tratamiento incorrecto de tipos de número de punto flotante (en configuraciones regionales que usan un delimitador distinto en números de punto flotante).|
|Asistente para la importación de archivos planos|Se ha corregido un problema relacionado con la importación de bits cuando los valores son 0 o 1. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898535). |
|Asistente para la importación de archivos planos|Se ha corregido un problema por el que se especificaban valores float como valores NULL.|
|Asistente para la importación de archivos planos|Se ha corregido un problema que evitaba que el Asistente para importación procesara valores decimales negativos.|
|Asistente para la importación de archivos planos|Se ha corregido un problema que evitaba que el asistente importara desde archivos CSV de una sola columna.|
|Asistente para la importación de archivos planos|estará en SSMS 17.9] Se ha corregido un incidencia por la que la importación de archivos planos no permitía cambiar la tabla de destino cuando la tabla ya existe. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186](https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186). |
|Visor de Ayuda|Lógica mejorada en torno al respeto de los modos en línea o sin conexión (aún puede haber algunas incidencias que deban solucionarse).|
|Visor de Ayuda|Se ha corregido la opción "Ver Ayuda" para que se respete la configuración de en línea/sin conexión. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791](https://feedback.azure.com/forums/908035-sql-server/suggestions/32897791). |
|Alta disponibilidad y recuperación ante desastres<BR> Grupos de disponibilidad|Se ha corregido una incidencia que provocaba que los roles del "Asistente de Grupos de disponibilidad de conmutación por error" siempre se mostraran como "Resolviendo".|
|Alta disponibilidad y recuperación ante desastres<BR> Grupos de disponibilidad|Se ha corregido un problema que provocaba que SSMS mostrara advertencias truncadas en el "Panel de grupos de disponibilidad".|
|Integration Services (IS)|Se ha corregido una incidencia en paralelo por la que el Asistente para la implementación no se puede conectar a SQL Server si SQL Server 2019 y SSMS 18.0 están instalados en el mismo equipo.|
|Integration Services (IS)|Se ha corregido un problema que impedía editar una tarea de plan de mantenimiento al diseñar el plan de mantenimiento.|
|Integration Services (IS)|Se ha corregido una incidencia que provocaba el bloqueo del Asistente para la implementación al cambiar el nombre del proyecto en la implementación.|
|Integration Services (IS)|Se ha habilitado la configuración del entorno en la característica de programación de Azure-SSIS IR.|
|Integration Services (IS)|Se ha corregido un problema que provocaba que el Asistente para la creación de un entorno de ejecución de integración de SSIS dejara de responder cuando la cuenta del cliente pertenecía a más de un inquilino.|
|Monitor de actividad de trabajo|Se ha corregido un bloqueo al usar el Monitor de actividad (con filtros).|
|Explorador de objetos|Se ha corregido una incidencia por la que SSMS generaba una excepción "No se puede convertir el objeto del tipo DBNull a otros tipos" al intentar expandir el nodo "Administración" del Explorador de objetos (configuración errónea de DataCollector).|
|Explorador de objetos|Se ha corregido un problema por el que el Explorador de objetos no incluía comillas de escape antes de invocar a "Editar las primeras...", lo que provocaba confusión en el diseñador.|
|Explorador de objetos|Se ha corregido un problema donde el asistente "Importar la aplicación de capa de datos" no se iniciaba desde el árbol de Azure Storage.|
|Explorador de objetos|Se ha corregido un problema en "Configuración de Correo electrónico de base de datos" que provocaba que no se conservara el estado de la casilla SSL. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541](https://feedback.azure.com/forums/908035-sql-server/suggestions/32895541). |
|Explorador de objetos|Se ha corregido una incidencia por la que la opción de SSMS para cerrar las conexiones existentes se atenuaba al intentar restaurar la base de datos con is_auto_update_stats_async_on.|
|Explorador de objetos|Se ha corregido un problema por el que al hacer clic con el botón derecho en nodos del Explorador de objetos (por ejemplo, "Tablas", y querer realizar una acción como filtrar las tablas mediante Filtro > Configuración de filtro, el formulario de configuración de filtro puede aparecer en la otra pantalla y no en la que SSMS está activo actualmente). Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106](https://feedback.azure.com/forums/908035-sql-server/suggestions/34284106). |
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
|Scripting de objetos|Al crear objetos de scripting, se omite la configuración de DB Scoped que tiene valores predeterminados.|
|Scripting de objetos|No se genera T-SQL dinámico al crear un scripting. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898391). |
|Scripting de objetos|Se omite la sintaxis de gráfico "como borde" y "como nodo" en el scripting de una tabla en SQL Server 2016 y versiones anteriores.|
|Scripting de objetos|Se ha corregido una incidencia que provocaba un error de scripting de objetos de base de datos al conectarse a una Azure SQL DB mediante AAD con MFA.|
|Scripting de objetos|Se ha corregido un problema que producía un error al intentar incluir en un script un índice espacial con GEOMETRY_AUTO_GRID o GEOGRAPHY_AUTO_GRID en una instancia de Azure SQL DB.|
|Scripting de objetos|Se ha corregido un problema que provocaba que el scripting de una base de datos (de una base de datos de Azure SQL) tuviera siempre como destino una instancia de SQL Server local, incluso si la configuración de scripting del "Explorador de objetos" se hubiera establecido para coincidir con el origen.|
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
|Cuadrícula de resultados|Se ha corregido un problema que provocaba una excepción "Índice fuera de rango" al hacer clic en la cuadrícula.|
|Cuadrícula de resultados|Se ha corregido un problema por el cual se omitía el color de fondo del resultado de la cuadrícula. Para obtener detalles, vea [https://feedback.azure.com/forums/908035/suggestions/32895916](https://feedback.azure.com/forums/908035/suggestions/32895916). |
|ShowPlan|Las nuevas propiedades del operador de concesión de memoria no se muestran correctamente cuando hay más de un subproceso.|
|ShowPlan|Se han agregado los siguientes cuatro atributos en RunTimeCountersPerThread del plan XML de ejecución real: HpcRowCount (número de filas procesadas por dispositivo hpc), HpcKernelElapsedUs (espera de tiempo transcurrida para la ejecución del kernel en uso), HpcHostToDeviceBytes (bytes transferidos desde el host al dispositivo) y HpcDeviceToHostBytes (bytes transferidos desde el dispositivo al host).|
|ShowPlan|Se ha corregido una incidencia que provocaba que los nodos de plan parecidos se resaltaran en una posición incorrecta.|
|SMO|Se ha corregido un problema por el que SMO/ServerConnection no controlaba correctamente las conexiones basadas en SqlCredential. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941](https://feedback.azure.com/forums/908035-sql-server/suggestions/33698941). |
|SMO|Se ha corregido un problema por el que una aplicación escrita con SMO podía encontrar un error si intentaba enumerar las bases de datos desde el mismo servidor en varios subprocesos, aunque usara instancias de SqlConnection independientes en cada uno.|
|SMO|Se ha corregido la regresión de rendimiento en la transferencia desde tablas externas.|
|SMO|Se ha corregido una incidencia en la seguridad para subprocesos de ServerConnection que hacía que SMO perdiera instancias de SqlConnection cuando el destino es Azure.|
|SMO|Se ha corregido una incidencia que provocaba un error StringBuilder.FormatError al intentar restaurar una base de datos que tenía llaves en su nombre.|
|SMO|Se ha corregido una incidencia por la cual las bases de datos de Azure en SMO aplicaban, de forma predeterminada, la intercalación sin distinguir entre mayúsculas y minúsculas para todas las comparaciones de cadenas en lugar de usar la intercalación especificada para la base de datos.|
|Editor de SSMS|Se ha corregido una incidencia en la que la "Tabla del sistema de SQL" al restaurar los colores predeterminados cambiaba el color a verde lima, y no a verde predeterminado, lo que lo hacía muy difícil de leer sobre un fondo blanco. Para obtener más información, consulte [Restaurar el color predeterminado incorrecto para la Tabla del sistema de SQL](https://feedback.azure.com/forums/908035-sql-server/suggestions/32896906). La incidencia todavía persiste en versiones no inglesas de SSMS.|
|Editor de SSMS|Se ha corregido un problema por el que IntelliSense no funcionaba cuando se conectaba a Azure SQLDW con autenticación de AAD.|
|Editor de SSMS|Se ha corregido IntelliSense en Azure cuando el usuario carece de acceso a la base de datos **maestra**.|
|Editor de SSMS|Se han corregido fragmentos de código para crear "tablas temporales", que se interrumpían cuando la intercalación de la base de datos de destino distinguía mayúsculas de minúsculas.|
|Editor de SSMS|Ahora IntelliSense reconoce la nueva función TRANSLATE. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898430](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898430). |
|Editor de SSMS|Se ha mejorado IntelliSense en la función integrada FORMAT. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898676](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898676). |
|Editor de SSMS|LAG y LEAD ahora se reconocen como funciones integradas. Para obtener detalles, vea [https://feedback.azure.com/forums/908035-sql-server/suggestions/32898757](https://feedback.azure.com/forums/908035-sql-server/suggestions/32898757). |
|Editor de SSMS|Se ha corregido una incidencia que hacía que IntelliSense generara una advertencia al usar "ALTER TABLE...ADD CONSTRAINT...WITH(ONLINE=ON)".|
|Editor de SSMS|Se ha corregido un problema por el cual varias vistas del sistema y funciones de valores de tabla no se coloreaban correctamente.|
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

## <a name="downloadssdtmediadownloadpng-ssms-1791httpsgomicrosoftcomfwlinklinkid2043154clcid0x409"></a>![descargar](../ssdt/media/download.png) [SSMS 17.9.1](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409)

- Número de versión: 17.9.1<br>
- Número de compilación: 14.0.17289.0<br>
- Fecha de publicación: 21 de noviembre de 2018

17.9.1 es una pequeña actualización de 17.9 con las correcciones de errores siguientes:

- Se ha corregido un problema que hace que los usuarios experimenten que su conexión se cierra y se vuelve a abrir con cada invocación de consulta cuando se usa la autenticación "Active Directory: Universal compatible con MFA" con el editor de consultas SQL. Entre los efectos secundarios del cierre de la conexión se incluyen tablas temporales globales que se quitan de forma inesperada y, a veces, la asignación de un SPID nuevo a la conexión.
- Se ha corregido un problema pendiente desde hace mucho tiempo por el que se producía un error al buscar un plan de restauración, o bien se generaba un plan de restauración ineficaz en determinadas condiciones.
- Se ha corregido un problema en el Asistente "para importar aplicaciones de capa de datos" que podía producir un error cuando se conectaba a una base de datos Azure SQL.

> [!NOTE]
> Las versiones localizadas de SSMS 17.x en idiomas diferentes al inglés requieren el [paquete de actualización de seguridad KB 2862966](https://support.microsoft.com/kb/2862966) cuando se instalan en: Windows 8, Windows 7, Windows Server 2012 y Windows Server 2008 R2.

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=2043154&clcid=0x40a)

## <a name="downloadssdtmediadownloadpng-ssms-179httpsgomicrosoftcomfwlinklinkid2014306clcid0x409"></a>![descargar](../ssdt/media/download.png) [SSMS 17.9](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x409)

Número de compilación: 14.0.17285.0<br>
Fecha de publicación: 04 de septiembre de 2018

> [!NOTE]
> Las versiones localizadas de SSMS 17.x en idiomas diferentes al inglés requieren el [paquete de actualización de seguridad KB 2862966](https://support.microsoft.com/kb/2862966) cuando se instalan en: Windows 8, Windows 7, Windows Server 2012 y Windows Server 2008 R2.

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=2014306&clcid=0x40a)

### <a name="whats-new"></a>Novedades

**SSMS general**

Plan de presentación:

- ahora en el plan de presentación gráfico se muestran los nuevos atributos de comentarios de concesión de memoria de modo de fila cuando se activa la característica para un plan concreto: IsMemoryGrantFeedbackAdjusted y LastRequestedMemory se han agregado al elemento XML de plan de consulta MemoryGrantInfo. Para más información sobre los comentarios de concesión de memoria del modo de fila, vea [Procesamiento de consultas adaptable en bases de datos SQL](https://docs.microsoft.com/sql/relational-databases/performance/adaptive-query-processing).

Azure SQL:

- Se agregó compatibilidad para las SKU de núcleo virtual en la creación de la base de datos de Azure. Para más información, vea [Modelo de compra basado en núcleos virtuales](https://docs.microsoft.com/azure/sql-database/sql-database-service-tiers#vcore-based-purchasing-model).
 

### <a name="bug-fixes"></a>Correcciones de errores

**SSMS general**

Monitor de replicación:

- Se ha corregido un problema que hacía que el Monitor de replicación (SqlMonitor.exe) no se iniciara (elemento de User Voice: https://feedback.azure.com/forums/908035-sql-server/suggestions/34791079).

Asistente para la importación de archivos planos:

- Se ha corregido el vínculo a la página de ayuda para el cuadro de diálogo del asistente de archivo sin formato. 
- Se ha corregido un problema por el que el asistente no permitía cambiar la tabla de destino cuando ya existía la tabla: esto permite a los usuarios volver a intentarlo sin tener que salir del asistente, eliminar la tabla errónea y, a continuación, volver a escribir la información en el asistente (elemento Voz de usuario): https://feedback.azure.com/forums/908035-sql-server/suggestions/32896186).

Importar/exportar aplicación de capa de datos:

- Se ha corregido un problema (en DacFx) que causaba que la importación de un archivo .bacpac podía producir un error con un mensaje similar a "Error SQL72014: .Net SqlClient Data Provider: Mensaje 9108, Nivel 16, Estado 10, Línea 1 Este tipo de estadística no puede ser incremental. " cuando se trabaja con tablas con particiones definidas y no hay índices en la tabla.

IntelliSense:

- Se ha corregido un problema consistente en que la finalización de IntelliSense no funcionaba al usar AAD con MFA.

Explorador de objetos:

- Se ha corregido un problema por el que el "cuadro de diálogo de filtro" se mostraba en monitores aleatorios en lugar del monitor en el que se ejecutaba el SSMS (sistemas de varios monitores).

Azure SQL:

- Se ha corregido un problema relacionado con la enumeración de bases de datos en "Bases de datos disponibles" consistente en que la base de datos "maestra" no se mostraba en la lista desplegable cuando se conectaba a una base de datos específica.
- Se ha corregido un problema por el que al intentar generar un script ("Datos" o "Esquema y datos") se producía un error al conectarse a la instancia de Azure SQL Database mediante AAD con MFA.
- Se ha corregido un problema en el diseñador de vistas consistente en que no era posible seleccionar "Agregar tablas" desde la interfaz de usuario cuando se conectaba a una instancia de Azure SQL Database.
- Se ha corregido un problema que hacía que el Editor de consultas SSMS cerrase y volviese a abrir las conexiones de forma silenciosa durante la renovación de los tokens de MFA. Esto evita que se produzcan efectos secundarios sin que el usuario lo sepa (como cerrar una transacción y no volver a abrirla nunca más). El cambio agrega la hora de expiración del token a la ventana de propiedades. 
- Se ha corregido un problema por el que SSMS no aplicaba los avisos de contraseña para las cuentas MSA importadas para AAD con inicio de sesión de MFA. 

Monitor de actividad:

- Se ha corregido un problema que provocaba que se bloqueara la opción "Estadísticas de consultas dinámicas" cuando se iniciaba desde el Monitor de actividad y se utilizaba la autenticación de SQL. 

Integración de Microsoft Azure: 

- Se ha corregido una incidencia por la que SSMS solo mostraba las primeras 50 suscripciones (cuadros de diálogo de Always Encrypted, cuadros de diálogo de copia de seguridad y restauración desde la dirección URL, entre otros).
- Se ha corregido un problema por el que SSMS iniciaba una excepción ("Índice fuera del intervalo") al intentar iniciar sesión en una cuenta de Microsoft Azure que no tenía ninguna cuenta de almacenamiento (en el cuadro de diálogo de restauración de copia de seguridad desde la dirección URL). 

Scripting de objetos:

- Cuando se crea el script "Drop and Create", SSMS ahora evita la generación dinámica de T-SQL.
- Cuando se crea un script para un objeto de base de datos, SSMS ahora no genera ningún script para establecer configuraciones de ámbito de base de datos, si se establecen en los valores predeterminados.

Help:

- Se ha corregido un problema pendiente desde hace mucho tiempo por el que la "Ayuda sobre la Ayuda" no respetaba el modo en línea o sin conexión.
- Al hacer clic en "Help | Community Projects and Samples" (Ayuda | Proyectos y ejemplos de la comunidad), SSMS abre ahora el explorador predeterminado que apunta a una página de Git y no muestra errores o advertencias debidos al uso de un explorador antiguo.

### <a name="known-issues"></a>Problemas conocidos

> [!IMPORTANT]
> Cuando se usa la autenticación *Active Directory: Universal compatible con MFA* con el editor de consultas SQL, es posible que los usuarios experimenten que su conexión se cierra y se vuelve a abrir con cada invocación de consulta. Entre los efectos secundarios de este tipo de cierre se incluyen tablas temporales globales que quitan de forma inesperada y, a veces, un nuevo SPID que se asigna a la conexión. Este cierre no se producirá si hay una transacción abierta en la conexión. Para solucionar este problema, los usuarios pueden establecer `persist security info=true` en los parámetros de conexión.

## <a name="downloadssdtmediadownloadpng-ssms-1781httpsgomicrosoftcomfwlinklinkid875802"></a>![descargar](../ssdt/media/download.png) [SSMS 17.8.1](https://go.microsoft.com/fwlink/?linkid=875802)
*Se detectó un error en 17.8 relacionado con el aprovisionamiento de bases de datos SQL, por lo que SSMS 17.8.1 sustituye a 17.8.*

Número de compilación: 14.0.17277.0<br>
Fecha de publicación: 26 de junio de 2018

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=875802&clcid=0x40a)

### <a name="whats-new"></a>Novedades

**SSMS general**

Propiedades de la base de datos:

- Esta mejora expone la opción de configuración **AUTOGROW_ALL_FILES** para grupos de archivos. Esta nueva opción de configuración se agrega en la ventana Propiedades de base de datos > Grupos de archivos en forma de una nueva columna (Crecimiento automático de todos los archivos) de casillas para cada grupo de archivos disponible (excepto para Secuencia de archivos y Grupos de archivos con optimización para memoria). El usuario puede habilitar o deshabilitar AUTOGROW_ALL_FILES para un determinado grupo de archivos alternando la casilla de Autogrow_All_Files correspondiente. En consecuencia, a la opción **AUTOGROW_ALL_FILES** se le aplica un script adecuado al aplicar scripts en la base de datos para CREATE o generar scripts para la base de datos (SQL2016 y posteriores).

Editor SQL:

- Se ha mejorado la experiencia con Intellisense en Azure SQL Database cuando el usuario no tiene acceso maestro.

Scripting:

- Mejoras generales de rendimiento, especialmente a través de conexiones de alta latencia.

**Analysis Services (AS)**

- Se han actualizado las bibliotecas de cliente y los proveedores de datos de Analysis Services a la versión más reciente, que agregó compatibilidad para la nueva autoridad de AAD de Azure Government (login.microsoftonline.us).

### <a name="bug-fixes"></a>Correcciones de errores

**SSMS general**

Planes de mantenimiento:

- Se ha corregido un problema al editar los planes de mantenimiento con Autenticación SQL por el cual se producía un error en la "Tarea Notificar al operador" al usar la autenticación SQL.
    
Scripting:

- Se ha corregido un problema por el cual las acciones de PostProcess en SMO provocan el agotamiento de recursos y errores de inicio de sesión de SQL.
    
SMO:

- Se ha corregido un problema por el cual se produce un problema en Table.Alter() si se agrega una columna con restricción predeterminada y la tabla ya tiene datos. Para obtener más información, consulte [sql server smo generating inline default constraint when adding a column to a table containing data](https://feedback.azure.com/forums/908035-sql-server/suggestions/32895625) (generación de restricción predeterminada en línea al agregar una columna a una tabla que contiene datos).
    
Always Encrypted:

- Se ha corregido un problema (en DacFx) que provocaba un error de tiempo de espera de bloqueo al habilitar Always Encrypted en una tabla con particiones
    

**Analysis Services (AS)**

- Se ha corregido un problema que se producía al modificar un origen de datos de OAuth en un modelo de compatibilidad de nivel 1400 de Analysis Services tabular, que provocaba que los cambios en los tokens de OAuth no se actualizaran en el origen de datos.
- Se ha corregido un bloqueo en SSMS que podía producirse al usar algunas credenciales de origen de datos no válidas o editar orígenes de datos que no admitían la migración de Cambiar origen de datos en Power Query (por ejemplo, Oracle) en los modelos de compatibilidad de nivel 1400 de Analysis Services tabular.


### <a name="known-issues"></a>Problemas conocidos

- Al hacer clic en el botón *Script* después de modificar cualquier propiedad de grupo de archivos en la ventana *Propiedades*, se generan dos scripts: uno con una instrucción *USE <database>* y un segundo script con una instrucción *USE master*.  El script *USE master* se genera en el error y se debe descartar. Ejecute el script que contiene la instrucción *USE <database>* .
- Algunos cuadros de diálogo muestran un error de edición no válida cuando se trabaja con nuevas ediciones de Azure SQL Database *de uso general* o *crítico para la empresa*.
- Se puede observar alguna latencia en el visor de XEvents. Es un [problema conocido de .Net Framework](https://github.com/Microsoft/dotnet/blob/master/releases/net472/dotnet472-changes.md#sql). Considere la posibilidad de actualizar a NetFx 4.7.2.




## <a name="downloadssdtmediadownloadpng-ssms-177httpsgomicrosoftcomfwlinklinkid873126"></a>![descargar](../ssdt/media/download.png) [SSMS 17.7](https://go.microsoft.com/fwlink/?linkid=873126)

Número de compilación: 14.0.17254.0<br>
Fecha de publicación: 09 de mayo de 2018

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=873126&clcid=0x40a)


### <a name="whats-new"></a>Novedades

**SSMS general**

Monitor de replicación:   
- El monitor de replicación ahora admite el registro de un agente de escucha para escenarios en los que la base de datos del publicador o del distribuidor forma parte del grupo de disponibilidad. Ahora puede supervisar los entornos de replicación en los que la base de datos del publicador o de distribución forma parte de Always On. 
 
Azure SQL Data Warehouse: 
- Se ha agregado compatibilidad con la ubicación de la fila rechazada para las tablas externas en Azure SQL Data Warehouse. 

**Integration Services (IS)**

- Se ha agregado una característica de programación para los paquetes SSIS implementados en Azure SQL Database. A diferencia de SQL Server local y de Instancia administrada de SQL Database, que tienen el Agente SQL Server como programador de trabajos de primera clase, SQL Database no tiene ningún programador integrado. Esta nueva característica de SSMS proporciona una interfaz de usuario conocida que se parece al Agente SQL Server para programar paquetes implementados en SQL Database. Si usa SQL Database para hospedar la base de datos del catálogo SSIS, SSISDB, puede usar esta característica de SSMS para generar las canalizaciones, las actividades y los desencadenadores de Data Factory necesarios para programar los paquetes SSIS. Luego puede editar y extender estos objetos en Data Factory. Para más información, vea [Programar la ejecución de paquetes SSIS implementados en Azure con SQL Server Management Studio (SSMS)](../integration-services/lift-shift/ssis-azure-schedule-packages-ssms.md). Para más información sobre las canalizaciones, las actividades y los desencadenadores de Azure Data Factory, vea [Canalizaciones y actividades de Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-pipelines-activities) y [Ejecución y desencadenadores de la canalización en Azure Data Factory](https://docs.microsoft.com/azure/data-factory/concepts-pipeline-execution-triggers).
- Compatibilidad con la programación de paquetes SSIS en el Agente SQL en Instancia administrada de SQL. Ahora se pueden crear trabajos del Agente SQL para ejecutar paquetes SSIS en la instancia administrada. 

### <a name="bug-fixes"></a>Correcciones de errores

**SSMS general** 

Plan de mantenimiento:   
- Se ha corregido un problema por el que, al intentar cambiar la programación de un plan de mantenimiento existente, se producía una excepción. Para obtener información detallada, vea [SSMS 17.6 crashes when clicking on a schedule in a maintenance plan](https://feedback.azure.com/forums/908035-sql-server/suggestions/33712924) (SSMS 17.6 se bloquea al hacer clic en una programación de un plan de mantenimiento).

AlwaysOn: 
- Se ha corregido un problema por el que el panel de latencia de Always On no funcionaba con SQL Server 2012.
 
Scripting: 
- Se ha corregido un problema por el que el scripting de un procedimiento almacenado en Azure SQL Data Warehouse no funcionaba para los usuarios sin derechos administrativos.
- Se ha corregido un problema por el que el scripting de una base de datos en Azure SQL Database no generaba scripts de las propiedades *SCOPED CONFIGURATION*.
 
Telemetría: 
- Se ha corregido un problema por el que SSMS se bloqueaba y después intentaba conectarse a un servidor después de optar por no enviar datos de telemetría.
 
Azure SQL Database: 
- Se ha corregido un problema por el que el usuario no podía establecer o cambiar el nivel de compatibilidad (la lista desplegable estaba vacía). Con el fin de establecer el nivel de compatibilidad en 150, el usuario aún debe usar el botón *Script* y editar el script manualmente. 
 
SMO: 
- Se ha expuesto la configuración del tamaño del registro de errores en SMO. Para obtener información detallada, vea [Set the Maximum Size of the SQL Server Error Logs](https://feedback.azure.com/forums/908035-sql-server/suggestions/33624115) (Establecer el tamaño máximo de los registros de errores de SQL Server).  
- Se ha corregido el scripting del avance de línea en SMO para Linux.
- Varias mejoras del rendimiento al recuperar propiedades poco usadas.  

IntelliSense: 
- Mejora del rendimiento: se ha reducido el volumen de las consultas de IntelliSense para los datos de columna. Es útil sobre todo cuando se trabaja en tablas que tienen un gran número de columnas. 

Configuración del usuario de SSMS:
- Se ha corregido un problema por el que no se podía cambiar correctamente el tamaño de la página de opciones.

Varios:  
- Se ha mejorado la presentación del texto en la página *Detalles de las estadísticas*. 

**Integration Services (IS)**

- Compatibilidad mejorada para Instancia administrada de Azure SQL Database.
- Se ha corregido un problema por el que el usuario no podía crear un catálogo para SQL Server 2014 o una versión anterior.
- Se han corregido dos problemas con los informes:
   - Se ha quitado el nombre del equipo para los servidores de Azure.
   - Se ha mejorado el tratamiento de nombres de objeto localizados.


### <a name="known-issues"></a>Problemas conocidos

Algunos cuadros de diálogo muestran un error de edición no válida cuando se trabaja con nuevas ediciones de Azure SQL Database *de uso general* o *crítico para la empresa*.

## <a name="downloadssdtmediadownloadpng-ssms-176httpsgomicrosoftcomfwlinklinkid870039"></a>![descargar](../ssdt/media/download.png) [SSMS 17.6](https://go.microsoft.com/fwlink/?linkid=870039)

Número de compilación: 14.0.17230.0<br>
Fecha de publicación: 20 de marzo de 2018

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=870039&clcid=0x40a)

### <a name="whats-new"></a>Novedades

**SSMS general**

Instancia administrada de SQL Database:

- Se ha agregado compatibilidad para [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance). Instancia administrada de Azure SQL Database ofrece una compatibilidad cercana al 100 % con SQL Server local, una implementación nativa de [red virtual (VNet)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) que aborda cuestiones de seguridad comunes y un [modelo empresarial](https://azure.microsoft.com/pricing/details/sql-database/) favorable para los clientes de SQL Server local.
- Compatibilidad con escenarios de administración habituales como los siguientes:
   - Creación y modificación de bases de datos.
   - Copias de seguridad y restauración de bases de datos.
   - Importación, exportación, extracción y publicación de aplicaciones de capa de datos.
   - Consulta y modificación de propiedades del servidor.
   - Compatibilidad total con el Explorador de objetos.
   - Creación de scripts de objetos de base de datos.
   - Compatibilidad con Trabajos del Agente SQL.
   - Compatibilidad con los servidores vinculados.
- Obtenga más información sobre Instancias administradas [aquí](https://azure.microsoft.com/blog/migrate-your-databases-to-a-fully-managed-service-with-azure-sql-database-managed-instance/).

Explorador de objetos:
- Se han incorporado opciones para no forzar los corchetes de los nombres al efectuar una acción de arrastrar y soltar del Explorador de objetos a la ventana de consulta (sugerencias de usuario [32911933](https://feedback.azure.com/forums/908035-sql-server/suggestions/32911933) y [32671051](https://feedback.azure.com/forums/908035-sql-server/suggestions/32671051)).

Clasificación de datos:
- Mejoras y correcciones de errores generales.

**Integration Services (IS)**

- Se ha agregado compatibilidad para implementar paquetes en una [Instancia administrada de SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).

### <a name="bug-fixes"></a>Correcciones de errores

**SSMS general**

Clasificación de datos:

- Se ha corregido un problema en *Clasificación de datos que provocaba que las clasificaciones recién agregadas se mostrasen con un *tipo de información* y una *etiqueta de confidencialidad* obsoletos.
- Se ha corregido un problema por el que *Clasificación de datos* no funcionaba al fijar como destino un servidor establecido en una intercalación que distingue mayúsculas de minúsculas.
        
AlwaysOn:

- Se ha corregido un problema en la opción "Mostrar panel" de un grupo de disponibilidad por el que, al hacer clic en *Recopilar datos de latencia*, se podía producir un error cuando el servidor se establecía en una intercalación que distingue mayúsculas de minúsculas.
- Se ha corregido un problema por el que SSMS notificaba erróneamente un grupo de disponibilidad como *distribuido* al cerrar el Servicio de clúster.
- Se ha corregido un problema por el que, al crear un grupo de disponibilidad con el cuadro de diálogo *Crear grupo de disponibilidad*, se necesitaba una *ReadOnlyRoutingUrl*.
- Se ha corregido un problema por el que, cuando el servidor principal está inactivo y se realiza la conmutación por error manual en el servidor secundario, se genera una excepción NullReferenceException.
- Se ha corregido un problema por el que, al crear un grupo de disponibilidad mediante la copia de seguridad o restauración para inicializar una base de datos, en las réplicas secundarias, los archivos de base de datos se crean en el directorio predeterminado. La corrección incluye lo siguiente:
   - Agregar el validador del directorio de datos/registros.
   - Lleve a cabo la reubicación de archivos únicamente cuando la réplica esté en un sistema operativo diferente a la réplica principal.
- Se ha corregido un problema por el que el asistente de SSMS no genera la opción *CLUSTER_TYPE*, por lo que se produce un error en la combinación secundaria.

Programa de instalación:
- Se ha corregido un problema por el que se producía un error al intentar actualizar SSMS mediante la instalación del "paquete de actualización" si se instalaba SSMS en una ubicación no predeterminada.

SMO:
- Se ha corregido un problema de rendimiento por el que las tablas de scripting de SQL Server 2016 y de versiones posteriores podían llegar a tardar hasta 30 segundos (ahora tardan menos de 1 segundo).

Explorador de objetos:
- Se ha corregido un problema por el que SSMS podría generar una excepción como "Object cannot be cast from DBNull to other types" (No se puede convertir el objeto del tipo DBNull a otros tipos) al intentar expandir el nodo *Administración* en el Explorador de objetos.
- Se ha corregido un problema por el que *Iniciar PowerShell* no detectaba el módulo SQLServer cuando el perfil de PS definido por el usuario generaba la salida.
- Se ha corregido un bloqueo intermitente que se podía producir al hacer clic con el botón derecho en un nodo de tabla o de índice en el Explorador de objetos.

Correo electrónico de base de datos:
- Se ha corregido un problema por el que el *Asistente para configuración de Correo electrónico de base de datos* generaba una excepción al intentar mostrar o administrar más de 16 perfiles.


**Analysis Services (AS)**

- Se ha corregido un problema que hacía que, al modificar un origen de datos en un modelo de nivel de compatibilidad 1400 en SSMS, los cambios no se guardaran en el servidor.

**Integration Services (IS)**

- Se ha corregido un problema por el que SSMS no mostraba los informes ni el nodo de catálogo de SSIS al conectarse a la Instancia administrada de SQL Database.

### <a name="known-issues"></a>Problemas conocidos

> [!WARNING]
> Hay un problema conocido por el que SSMS 17.6 tiene un comportamiento inestable y se bloquea al usar [planes de mantenimiento](../relational-databases/maintenance-plans/maintenance-plans.md). Si usa planes de mantenimiento, no instale SSMS 17.6. Si ya ha instalado la versión 17.6 y experimenta este problema, cambie a la versión 17.5 de SSMS. 



## <a name="downloadssdtmediadownloadpng-ssms-175httpsgomicrosoftcomfwlinklinkid867670"></a>![descargar](../ssdt/media/download.png) [SSMS 17.5](https://go.microsoft.com/fwlink/?linkid=867670)
Disponible con carácter general | Número de compilación: 14.0.17224.0

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x40a)

### <a name="whats-new"></a>Novedades

**SSMS general**

Clasificación y detección de datos:

- Se ha agregado una nueva característica de clasificación y detección de datos de SQL para detectar, clasificar, etiquetar y notificar información confidencial en las bases de datos. 
- La detección automática y la clasificación de la información más confidencial (por ejemplo, empresarial, financiera, sanitaria o datos personales) pueden desempeñar un papel fundamental en el estado de protección de la información de la organización.
- Para más información, vea [Clasificación y detección de datos de SQL](../relational-databases/security/sql-data-discovery-and-classification.md).

Editor de consultas:

- Se ha agregado compatibilidad con la opción SkipRows al formato de archivo externo de texto delimitado para Azure SQL DW. Esta funcionalidad permite a los usuarios omitir un número especificado de filas al cargar archivos de texto delimitado en SQL DW. También se ha agregado la compatibilidad correspondiente de IntelliSense/SMO con la palabra clave FIRST_ROW. 

Plan de presentación:

- Se ha habilitado la presentación del botón de plan estimado para SQL Data Warehouse.
- Se ha agregado el nuevo atributo de plan de presentación *EstimateRowsWithoutRowGoal* y se han agregado nuevos atributos de plan de presentación a *QueryTimeStats*: *UdfCpuTime* y *UdfElapsedTime*. Para más información, vea [Adición de información sobre el objetivo de filas del optimizador en el plan de ejecución en SQL Server 2017 CU3](https://support.microsoft.com/help/4051361).



### <a name="bug-fixes"></a>Correcciones de errores

**SSMS general**

Plan de presentación:

- Se ha corregido el tiempo transcurrido de las estadísticas de consultas dinámicas para que muestre el tiempo de ejecución del motor, en lugar del tiempo transcurrido para la conexión de las estadísticas de consultas dinámicas.
- Se ha corregido un problema que hacía que el plan de presentación no pudiera reconocer operadores lógicos de aplicación, como GbApply e InnerApply.
- Se ha corregido un problema relacionado con ExchangeSpill.

Editor de consultas:

- Se ha corregido un problema relacionado con los SPID que hacía que SSMS produjera un error como el siguiente: "La cadena de entrada no tiene el formato correcto. (mscorlib)"al ejecutar una consulta simple precedida de "SET SHOWPLAN_ALL ON". 


SMO:

- Se ha corregido un problema que hacía que SMO no pudiera obtener las propiedades AvailabilityReplica en caso de que la intercalación del servidor distinguiera mayúsculas de minúsculas (como resultado, SSMS podía mostrar un mensaje de error como el siguiente: "El identificador formado por varias partes 'a.delimited' no se pudo enlazar".
- Se ha corregido un problema en la clase DatabaseScopedConfigurationCollection al controlar incorrectamente las intercalaciones (como resultado, un SSMS en ejecución en un equipo de agente de administración con una configuración regional en turco podría mostrar un error como "Legacy cardinality estimation is not valid scoped configuration" (La estimación de cardinalidad heredada no es una configuración con ámbito válida) al hacer clic con el botón derecho en una base de datos que se ejecute en un servidor con una intercalación que distinga mayúsculas de minúsculas).
- Se ha corregido un problema en la clase JobServer que hacía que SMO no pudiera obtener las propiedades de Agente SQL en un servidor de SQL 2005 (como resultado, SSMS producía un error como "No se puede asignar un valor predeterminado a una variable local. Debe declarar la variable escalar "\@ServiceStartMode" y, en última instancia, no mostraba el nodo de Agente SQL en el Explorador de objetos).

Plantillas: 

- "Correo electrónico de base de datos": se han corregido un par de errores tipográficos [(https://feedback.azure.com/forums/908035/suggestions/33143512)](https://feedback.azure.com/forums/908035/suggestions/33143512).  

Explorador de objetos:
- Se ha corregido un problema por el que la compresión administrada producía un error en los índices (https://feedback.azure.com/forums/908035-sql-server/suggestions/32610058-ssms-17-4-error-when-enabling-page-compression-o).

Auditoría:
- Se ha corregido un problema con la característica *Combinar archivos de auditoría*.
<br>

### <a name="known-issues"></a>Problemas conocidos

Clasificación de datos:
- La eliminación de una clasificación y la posterior adición manualmente de una nueva clasificación para la misma columna hace que se asigne el tipo de información y la etiqueta de confidencialidad anteriores a la columna en la vista principal.<br>
*Solución*: asigne el tipo de información y la etiqueta de confidencialidad nuevos después de volver a agregar la clasificación a la vista principal y antes de guardar.


## <a name="downloadssdtmediadownloadpng-ssms-174httpsgomicrosoftcomfwlinklinkid864329"></a>![descargar](../ssdt/media/download.png) [SSMS 17.4](https://go.microsoft.com/fwlink/?linkid=864329)
Disponible con carácter general | Número de compilación: 14.0.17213.0

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x40a)


### <a name="whats-new"></a>Novedades

**SSMS general**

Evaluación de vulnerabilidad:
- Se ha incluido un nuevo servicio de evaluación de vulnerabilidades de SQL para analizar las bases de datos con objeto de encontrar posibles vulnerabilidades y desviaciones con respecto a los procedimientos recomendados, como errores de configuración, permisos excesivos y datos confidenciales sin protección. 
- Los resultados de la evaluación incluyen pasos que requieren acción con los que se corrige cada problema y scripts de solución personalizados cuando proceda. El informe de evaluación se puede personalizar para ajustarse a cada entorno y adaptarse a los requisitos particulares. Obtenga más información en [Evaluación de vulnerabilidades de SQL](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment).

SMO:
- Se ha corregido un problema en el que *HasMemoryOptimizedObjects iniciaba una excepción en Azure.
- Se ha agregado compatibilidad con la nueva característica CATALOG_COLLATION.

Panel AlwaysOn:
- Mejoras en el análisis de latencia de Grupos de disponibilidad.
- Se han agregado dos informes nuevos: *AlwaysOn\_Latency\_Primary* y *AlwaysOn\_Latency\_Secondary*.

Plan de presentación:
- Se han actualizado los vínculos para que apunten a la documentación correcta.
- Se permite el análisis de plan único directamente desde plan real generado.
- Nuevo conjunto de iconos.
- Se ha agregado compatibilidad para identificar "operadores lógicos de aplicación" como GbApply o InnerApply.

XE Profiler:
- Se ha cambiado el nombre a generador de perfiles XEvent.
- Ahora, los comandos de menú Iniciar y Detener inician o detienen la sesión de forma predeterminada.
- Se han habilitado métodos abreviados de teclado (por ejemplo, **CTRL+F** para realizar búsquedas).
- Se han agregado las acciones database\_name y client\_hostname a los eventos pertinentes en las sesiones del generador de perfiles XEvent. Para que el cambio surta efecto, puede que sea necesario eliminar las instancias de sesión QuickSessionStandard o QuickSessionTSQL existentes en los servidores (vea el [artículo 3142981 de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3142981)).

Línea de comandos:
- Se ha agregado una nueva opción de línea de comandos ("-G") que sirve para conectar SSMS automáticamente a un servidor o a una base de datos por medio de la autenticación de Active Directory ("Integrada" o "Contraseña"). Para más información, vea [Ssms (Utilidad)](ssms-utility.md).

Asistente para la importación de archivos planos:
- Se ha agregado un método para seleccionar un nombre de esquema distinto del predeterminado ("dbo") al crear la tabla.

Almacén de consultas:
- Se ha restaurado el informe "Consultas con regresión" al expandir la lista de informes Almacén de consultas disponible.

**Integration Services (IS)**
- Se ha agregado una función de validación de paquetes al Asistente para la implementación que sirve para que el usuario averigüe qué componentes de los paquetes SSIS no se admiten en Azure-SSIS IR.

### <a name="bug-fixes"></a>Correcciones de errores

**SSMS general**

- Explorador de objetos: Se ha corregido un problema por el que el nodo Función con valores de tabla no aparecía con las instantáneas de base de datos (vea el [artículo de Connect 3140161](https://connect.microsoft.com/SQLServer/feedback/details/3140161)).
Se ha mejorado el rendimiento al expandir el nodo *Bases de datos* cuando el servidor tiene bases de datos AUTOCLOSE.
- Editor de consultas: Se ha corregido un problema por el que se producían errores en IntelliSense con usuarios que no tienen acceso a la base de datos maestra.
Se ha corregido un problema que hacía que SSMS se bloqueara en algunos casos cuando se cerraba la conexión con un equipo remoto (vea el [artículo de Connect 3142557](https://connect.microsoft.com/SQLServer/feedback/details/3142557)).
- Visor de XEvent: Se ha vuelto a habilitar la funcionalidad para exportar a XEL.
Se han corregido problemas por los que, a veces, los usuarios no podían cargar un archivo XEL completo.
- Generador de perfiles XEvent: Se ha corregido un problema que hacía que SSMS se bloqueara si un usuario no tenía el permiso *VER ESTADO DEL SERVIDOR*.
Se ha corregido un problema en el que, al cerrar la ventana de datos actualizados del generador de perfiles XEvent, no se detenía la sesión subyacente.
- Servidores registrados: Se ha corregido un problema por el cual el comando "Mover a..." dejaba de funcionar: [Connect 3142862](https://connect.microsoft.com/SQLServer/feedback/details/3142862) y [Connect 3144359](https://connect.microsoft.com/SQLServer/feedback/details/3144359/).
- SMO: Se ha corregido un problema consistente en que el método TransferData en el objeto de transferencia no funcionaba.
Se ha corregido un problema por el que las bases de datos de servidor iniciaban una excepción con las bases de datos de SQL DW en pausa.
Se ha corregido un problema por el que, al crear scripts de bases de datos SQL en SQL Data Warehouse, se generaban valores de parámetro de T-SQL incorrectos.
Se ha corregido un problema en el que, al crear el script de una base de datos extendida, se emitía incorrectamente la opción *DATA\_COMPRESSION*.
- Monitor de actividad de trabajo: Se ha corregido un problema en el que el usuario obtenía un error "El índice estaba fuera del intervalo. Debe ser un valor no negativo e inferior al tamaño de la colección. 
      Nombre del parámetro: index (System.Windows.Forms)" al intentar filtrar por categoría (vea el [artículo de Connect 3138691](https://connect.microsoft.com/SQLServer/feedback/details/3138691)).
- Cuadro de diálogo de conexión: Se ha corregido un problema por el que los usuarios del dominio sin acceso a un controlador de dominio de lectura/escritura no podían iniciar sesión en un servidor SQL Server por medio de la autenticación SQL (vea el [artículo de Connect 2373381](https://connect.microsoft.com/SQLServer/feedback/details/2373381)).
- Replicación: Se ha corregido un problema en el que se mostraba un error similar a "No se puede aplicar el valor 'null' a la propiedad ServerInstance" al examinar las propiedades de una suscripción de extracción en SQL Server.
- Programa de instalación de SSMS: Se ha corregido un problema que hacía que el programa de instalación de SSMS reconfigurara incorrectamente todos los productos instalados en el equipo.
- Configuración del usuario:
   - Con esta corrección, los usuarios de Azure Government tienen acceso ininterrumpido a sus recursos de Azure SQL Database y Azure Resource Manager con SSMS a través de la autenticación universal y el inicio de sesión de Azure Active Directory.  Los usuarios con versiones anteriores de SSMS deberán abrir Herramientas|Opciones|Servicios de Azure y, en Administración de recursos, cambiar la configuración de la propiedad "Entidad de Active Directory" por https://login.microsoftonline.us.

**Analysis Services (AS)**

- Generador de perfiles: se ha corregido un problema que ocurría al intentar conectarse por medio de la autenticación de Windows en Azure AS.
- Se ha corregido un problema que provocaba un bloqueo al cancelar los detalles de la conexión en un modelo 1400.
- Ahora, cuando se establece una clave de blob de Azure en el cuadro de diálogo de propiedades de la conexión al actualizar las credenciales, dicha clave se enmascara visualmente.
- Se ha corregido un problema en el cuadro de diálogo Selección de usuario de Azure Analysis Services para mostrar el GUID de la aplicación en lugar del identificador del objeto en las búsquedas.
- Se ha corregido un problema en la barra de herramientas Examen de base de datos\Diseñador de consultas de MDX que hacía que los iconos se asignaran incorrectamente a algunos de los botones.
- Se ha corregido un problema que impedía conectarse a SSAS a través de direcciones http/https de IIS de msmdpump.
- Ahora, algunas cadenas del cuadro de diálogo Selector de usuarios de Azure Analysis Services se han traducido a otros idiomas.
- Ahora, la propiedad MaxConnections es visible en los orígenes de datos de los modelos tabulares.
- Ahora, el Asistente para la implementación generará definiciones de JSON correctas para los miembros del rol de Azure AS.
- Se ha corregido un problema en SQL Profiler que hacía que, al seleccionar la autenticación de Windows en Azure AS, se seguía pidiendo que se iniciara sesión.



## <a name="downloadssdtmediadownloadpng-ssms-173httpsgomicrosoftcomfwlinklinkid858904"></a>![descargar](../ssdt/media/download.png) [SSMS 17.3](https://go.microsoft.com/fwlink/?linkid=858904)
Disponible con carácter general | Número de compilación: 14.0.17199.0

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)


### <a name="enhancements"></a>Mejoras

- Se ha agregado el nuevo asistente "Importar archivo plano" para simplificar la experiencia de importación de archivos CSV con un marco de trabajo inteligente, que ahora no exige prácticamente intervención por parte del usuario ni tener conocimientos especializados sobre dominios. Para obtener detalles, vea [Importación de archivos planos mediante el asistente de SQL](../relational-databases/import-export/import-flat-file-wizard.md).
- Se ha agregado el nodo "XEvent Profiler" al Explorador de objetos. Para obtener detalles, vea [Uso de XEvent Profiler de SSMS](../relational-databases/extended-events/use-the-ssms-xe-profiler.md).
- Se han actualizado el filtrado y la categorización de esperas en el informe histórico de esperas del panel de rendimiento.
- Se ha agregado la comprobación de sintaxis de la función "Predict".
- Se ha agregado la comprobación de sintaxis de las consultas de administración de biblioteca externa.
- Se ha agregado compatibilidad con SMO a la administración de biblioteca externa.
- Se ha agregado compatibilidad con "Iniciar PowerShell" a la ventana "Servidores registrados" (se requiere un nuevo módulo de SQL PowerShell).
- Always On: se ha agregado [compatibilidad de enrutamiento de solo lectura](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md) a los grupos de disponibilidad.
- Se ha agregado una opción para enviar detalles de seguimiento a la ventana de salida de los inicios de sesión "Active Directory - Universal compatible con MFA" (desactivados de forma predeterminada; deben activarse en la configuración de usuario, en "Herramientas > Opciones > Servicios de Azure > Nube de Azure > Nivel de seguimiento de la ventana de salida de ADAL"). 
- Almacén de consultas: 
  - La interfaz de usuario del almacén de consultas será accesible aunque QDS esté desactivado, siempre que haya registrado datos.
  - La interfaz de usuario del almacén de consultas ahora expone la categorización de esperas en todos los informes existentes. Esto permite que los clientes desbloqueen los escenarios de consultas que más esperan y muchos otros.
- Se ha convertido en opcional la inclusión de los encabezados de parámetros de scripting (desactivada de forma predeterminada; se puede habilitar en la configuración de usuario, en "Herramientas > Opciones > Explorador de objetos de SQL Server > Scripting > Incluir encabezado de parámetros de scripting"). [Artículo de Connect 3139199](https://connect.microsoft.com/SQLServer/feedback/details/3139199).
- Se ha quitado la personalización de marca "RC".

### <a name="bug-fixes"></a>Correcciones de errores

**SSMS general**

- XEvent: 
   - Se ha corregido el problema que hacía que SSMS abriera únicamente parte de los eventos del archivo .xel.
   - Se ha mejorado la experiencia "Observar datos en directo" cuando la base de datos predeterminada no es "master" (vea el [artículo de Connect 1222582](https://connect.microsoft.com/SQLServer/feedback/details/1222582)).
- AlwaysOn: se ha corregido el problema que podía producir un error "El registro de este conjunto de copia de seguridad finaliza en el LSN x, demasiado pronto para aplicarlo a la base de datos" en "Restaurar copias de seguridad de registro".
- Monitor de actividad de trabajo: se han corregido los iconos incoherentes. [Artículo de Connect 3133100](https://connect.microsoft.com/SQLServer/feedback/details/3133100).
- Almacén de consultas: se ha corregido el problema que hacía que el usuario no pudiera elegir un intervalo de fechas "personalizado" para los informes del almacén de consultas. Vinculado a los artículos de Connect siguientes.
   - [Artículo de Connect 3139842](https://connect.microsoft.com/SQLServer/feedback/details/3139842)
   - [Artículo de Connect 3139399](https://connect.microsoft.com/SQLServer/feedback/details/3139399)
- Se ha corregido un problema que hacía que el cuadro de diálogo de conexión no "borrara" la base de datos usada más recientemente cuando la información guardada tenía una base de datos con nombre y el usuario seleccionaba la predeterminada.
- Scripting de objetos: Se ha corregido un problema que hacía que "Generar script de base de datos" no funcionara y produjera un error cuando el usuario tenía una base de datos DW en pausa en el servidor, pero seleccionaba otra base de datos no DW e intentaba generar scripts de ella.
Se ha corregido el problema por el que el encabezado de los procedimientos almacenados generados por script no coincidía con la configuración de script, lo que daba lugar a un script engañoso (vea el [artículo 3139784 de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3139784)).
Se ha vuelto a habilitar el "botón Script" al dirigir objetos de Azure SQL.
  Se ha corregido un problema por el que SSMS no permitía el scripting de "Alter" o "Execute" en algunos objetos (UDF, View, SP, Trigger) cuando se estaba conectado a una instancia de Azure SQL Database (vea el [artículo 3136386 de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3136386)).
- Editor de consultas:
  - Se ha mejorado Intellisense al seleccionar instancias de Azure SQL Database.
  - Se ha corregido un problema que provocaba un error en las consultas debido a un token de autenticación expirado (autenticación universal).
  - Se ha mejorado Intellisense al trabajar con instancias de Azure SQL Database (en particular, al conectarse a Azure SQL Database, se usa la gramática más reciente de T-SQL (140)).
  - Se ha corregido el problema que hacía que, al abrir una ventana de consulta con una conexión a una base de datos no DW en un servidor, todas las ventanas de consulta subsiguientes de ese servidor a bases de datos DW produjeran distintos errores sobre tipos u opciones no compatibles.
- AlwaysOn:
   - se ha agregado la columna Modo de propagación al panel Always On y a la página de propiedades del grupo de disponibilidad.
   - Se ha corregido el problema que hacía que no se pudiera crear un grupo de disponibilidad de Linux cuando el principal estaba en Windows. [Artículo de Connect 3139856](https://connect.microsoft.com/SQLServer/feedback/details/3139856).
- Se han corregido varios problemas de "memoria insuficiente" en SSMS al ejecutar consultas. [Artículo de Connect 2845190](https://connect.microsoft.com/SQLServer/feedback/details/2845190) y [artículo de Connect 3123864](https://connect.microsoft.com/SQLServer/feedback/details/3123864).
- Profiler: 
   - Se ha corregido el problema por el que Profiler no funcionaba al seleccionar SQL 2005.
   - Se ha corregido el problema que hacía que Profiler no aceptara la opción de conexión "Confiar en certificado de servidor".
- Monitor de actividad: se ha corregido el problema que hacía que el Monitor de actividad no funcionara al apuntar a SQL Server en ejecución en Linux.
- Se ha corregido un problema con la clase de transferencia de SMO que hacía que no se transfirieran objetos de origen de datos externo o formato de archivo externo; ahora los objetos de estos tipos se deben incluir correctamente en la transferencia.
- Servidores registrados:
   - Se ha habilitado la consulta multiservidor para servidores de agente de usuario (intenta usar el mismo token para cada servidor de agente de usuario del grupo).
- Autenticación universal de AD:
   - Se ha corregido el problema que hacía que no se admitiera la autenticación de Azure AD.
   - Se ha corregido el problema que hacía que el diseñador de tablas o vistas no funcionara.
   - Se ha corregido el problema que hacía que "Seleccionar las 1000 primeras filas" y "Editar las 200 primeras filas" no funcionaran.
- Restauración de bases de datos: se ha corregido un problema que hacía que la restauración omitiera la última carpeta de la ruta de acceso al mover archivos a una ubicación alternativa.
- Asistente para comprimir:
   - Se ha corregido un problema del asistente para administrar la compresión de los índices; se ha corregido el problema que hacía que los asistentes para comprimir datos no funcionaran para SQL 2016 y versiones inferiores.
        https://connect.microsoft.com/SQLServer/feedback/details/3139342
   - Se ha agregado el asistente para comprimir a las tablas e índices de Azure.
- Plan de presentación: 
   - Se ha corregido el problema que hacía que no se reconocieran los operadores PDW.
- Propiedades del servidor:
   - Se ha corregido el problema que hacía que no se pudiera modificar la afinidad del procesador del servidor.


**Analysis Services (AS)**

- Se ha corregido una serie de problemas con el Asistente para la implementación para que admita modelos tabulares de nivel de compatibilidad 1400 y orígenes de datos de Power Query.
- El Asistente para la implementación se puede implementar ahora en Azure AS cuando se ejecuta desde la línea de comandos.
- Ahora, cuando se usa autenticación de Windows en Azure AS, el usuario ve correctamente el nombre de la cuenta de usuario en el Explorador de objetos.


### <a name="known-issues-in-this-173-release"></a>Problemas conocidos de la versión 17.3:

**SSMS general**

- La siguiente funcionalidad de SSMS no es compatible con la autenticación de Azure AD mediante UA con MFA:
   - El Asistente para la optimización de motor de base de datos no es compatible con la autenticación de Azure AD; hay un problema conocido que consiste en que el mensaje de error que se presenta al usuario es un poco críptico: "No se puede cargar el archivo o ensamblado "Microsoft.IdentityModel.Clients.ActiveDirectory,..." en lugar del esperado: "El Asistente para la optimización de motor de base de datos no admite Microsoft Azure SQL Database. (DTAClient)".
- El intento de analizar una consulta en DTA produce un error: "El objeto debe implementar IConvertible. (mscorlib)".
- *Consultas con regresión* no aparece en la lista Almacén de consultas de informes del Explorador de objetos.
   - Solución alternativa: haga clic con el botón derecho en el nodo **Almacén de consultas** y seleccione **Ver consultas con regresión**.

**Integration Services (IS)**

- [execution_path] de [catalog].[event_messagea] no es correcta para ejecuciones de paquetes en Escalabilidad horizontal. [execution_path] comienza con "\Package" en lugar del nombre de objeto del ejecutable del paquete. Al ver el informe general sobre ejecuciones de paquetes en SSMS, el vínculo de "Ruta de acceso de ejecución" de Información general de ejecución no puede funcionar. La solución alternativa consiste en hacer clic en "Ver mensajes" en el informe general para comprobar todos los mensajes de eventos.


## <a name="downloadssdtmediadownloadpng-ssms-172httpsgomicrosoftcomfwlinklinkid854085"></a>![descargar](../ssdt/media/download.png) [SSMS 17.2](https://go.microsoft.com/fwlink/?linkid=854085)
Disponible con carácter general | Número de compilación: 14.0.17177.0

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

### <a name="enhancements"></a>Mejoras

- Multi-Factor Authentication (MFA)
  - Autenticación de Azure AD de varios usuarios para la autenticación universal con Multi-Factor Authentication (UA con MFA).
  - Se ha agregado un nuevo campo de entrada de credenciales de usuario para la autenticación universal con MFA a fin de permitir la autenticación de varios usuarios.
- El cuadro de diálogo de conexión ahora admite los siguientes cinco métodos de autenticación:
  - Autenticación de Windows
  - Autenticación de SQL Server
  - Active Directory: Universal compatible con MFA
  - Active Directory: Contraseña
  - Active Directory: Integrado

- El asistente para exportación e importación de bases de datos para DacFx usa la autenticación universal con MFA.
- Para obtener información sobre la compatibilidad de API, consulte [IUniversalAuthProvider Interface](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx) (Interfaz IUniversalAuthProvider).
- La biblioteca administrada de ADAL que usa la autenticación universal de Azure AD con MFA se ha actualizado a la versión 3.13.9.
- Además, se ha publicado una nueva interfaz de la CLI compatible con la configuración de administración de Azure AD para SQL Database y SQL Data Warehouse.

 Para más información sobre los métodos de autenticación de Active Directory, vea [Autenticación universal con SQL Database y SQL Data Warehouse (compatibilidad de SSMS con MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) y [Configuración de la autenticación multifactor para SQL Server Management Studio y Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure).

- La ventana de salida tiene entradas para las consultas que se ejecutan durante la expansión de los nodos del Explorador de objetos.
- Diseñador de vistas habilitado para instancias de Azure SQL Database.
- Han cambiado las opciones de scripting predeterminadas para incluir en script objetos desde el Explorador de objetos en SSMS:
  - Anteriormente, el valor predeterminado en una instalación nueva era que el destino de script generado tuviera la versión más reciente de SQL Server (actualmente, SQL Server 2017).
  - En SSMS 17.2 se ha agregado una opción nueva: *Coincidir configuración del script con origen*. Cuando se establece en *True*, el script generado tiene como destino la misma versión, tipo de motor y edición del motor que el servidor al que pertenece el objeto del que se crea el script.
  - El valor *Coincidir configuración del script con origen* se establece en *True* de forma predeterminada, por lo que las nuevas instalaciones de SSMS tendrán automáticamente la opción predeterminada de crear siempre el script de los objetos en el mismo destino que el servidor original.
  - Cuando el valor *Coincidir configuración del script con origen* se establece en *False*, se habilitarán las opciones de destino de scripting normales y funcionarán como lo hacían anteriormente.
Además, todas las opciones de scripting se han movido a su propia sección: *Opciones de versión*. Ya no están en *Opciones generales de scripting*.

- Se ha agregado compatibilidad con nubes nacionales en "Restore from URL".
- Los informes de QueryStoreUI ahora son compatibles con otras métricas (por ejemplo, RowCount, DOP o tiempo de CLR) de sys.query_store_runtime_stats.
- IntelliSense es ahora compatible con Azure SQL Database https://connect.microsoft.com/SQLServer/feedback/details/3100677/ssms-2016-would-be-nice-to-have-intellisense-on-azure-sql-databases
- El cuadro de diálogo Seguridad: conexión tendrá como valor predeterminado no confiar en certificados de servidor y solicitará cifrado para las conexiones de Azure SQL DB.
- Mejoras generales sobre la compatibilidad de SQL Server con Linux:
 - Se recupera el nodo Correo electrónico de base de datos.
 - Se han solucionado algunos problemas relacionados con las rutas de acceso.
 - El monitor de actividad es más estable.
 - El cuadro de diálogo Propiedades de conexión muestra la plataforma correcta.
- El informe del servidor del panel de rendimiento ahora está disponible como informe predeterminado:
  - Puede conectarse a SQL Server 2008 y versiones más recientes.
  - El subinforme Índices que faltan usa la puntuación para ayudar a identificar los índices más útiles.
  - El subinforme de estadísticas de esperas históricas ahora agrega esperas por categoría. Las esperas Inactivo y En suspensión se filtran de forma predeterminada.
  - Nuevo subinforme Bloqueos temporales del historial.
- La búsqueda del nodo Plan de presentación permite buscar en las propiedades del plan. Busque fácilmente cualquier propiedad de operador como el nombre de la tabla. Para usar esta opción al ver un plan:
  - Haga clic con el botón derecho en el plan y, en el menú contextual, haga clic en la opción Buscar nodo.
  - Use **CTRL+F**.


**Analysis Services (AS)**

- Nueva selección de miembros del rol de AAD para usuarios sin direcciones de correo electrónico en modelos de Azure AS en SSMS

**Integration Services (IS)**

- Se ha agregado una nueva columna ("Recuento ejecutado") al informe de ejecución de SSIS

### <a name="known-issues-in-this-release"></a>Problemas conocidos de esta versión:

- Las ventanas de consulta que usan la autenticación "Active Directory - Universal compatible con MFA" pueden experimentar un error similar al siguiente, al intentar ejecutar una consulta después de que esté abierta durante una hora:

   `Msg 0, Level 11, State 0, Line 0
The connection is broken and recovery isn't possible. The client driver attempted to recover the connection one or more times and all attempts failed. Increase the value of ConnectRetryCount to increase the number of recovery attempts.`

   Si se vuelve a ejecutar la consulta, se debería solucionar el error y realizarse correctamente.

- No se admite la siguiente funcionalidad de SSMS para la autenticación de Azure AD mediante la autenticación universal con MFA:
  - El diseñador **Nueva tabla o vista** muestra el aviso de inicio de sesión antiguo y no funciona para la autenticación de Azure AD.
  - La característica **Editar las primeras 200 filas** no es compatible con la autenticación de Azure AD.
  - El componente **Servidor registrado** no es compatible con la autenticación de Azure AD.
  - El **Asistente para la optimización de motor de base de datos** no es compatible con la autenticación de Azure AD. Hay un problema conocido por el que el mensaje de error que se presenta al usuario no es útil: *No se puede cargar el archivo o ensamblado "Microsoft.IdentityModel.Clients.ActiveDirectory,...* en lugar del esperado *El Asistente para la optimización de motor de base de datos no admite Microsoft Azure SQL Database. (DTAClient)* .

**Analysis Services (AS)**

- El Explorador de objetos de SSAS no mostrará el nombre de usuario de autenticación de Windows en las propiedades de conexión de Azure AS.

### <a name="bug-fixes"></a>Correcciones de errores

- Se ha corregido un problema al intentar imprimir los resultados de una consulta (como texto).  https://connect.microsoft.com/SQLServer/feedback/details/3055225/
- Se ha corregido una incidencia que hacía que SSMS colocara incorrectamente tablas y otros objetos al incluir en un script la eliminación de esos objetos en una base de datos de Azure SQL.
- Se ha corregido un problema que hacía que, en ocasiones, SSMS se negara a iniciar con un error como "No se encuentran uno o más componentes. Reinstale la aplicación".
- Se ha corregido un problema que hacía que el SPID en la interfaz de usuario de SSMS pudiera quedar obsoleto y desactualizado. https://connect.microsoft.com/SQLServer/feedback/details/1898875
- Se ha corregido un problema en el programa de instalación (silenciosa) de SSMS que hacía que el argumento /passive se tratara como /quiet.
- Se ha corregido un problema que hacía que SSMS produjera ocasionalmente un error de "Referencia de objeto no establecida en una instancia de un objeto" durante el inicio. https://connect.microsoft.com/SQLServer/feedback/details/3134698
- Se ha corregido un problema en el "Asistente para compresión de datos" que causaba que SSMS se bloqueara al pulsar "Calcular" en la tabla de Graph
- Se ha solucionado un problema de rendimiento al hacer clic con el botón derecho en un índice de una tabla (en una conexión a Internet lenta). https://connect.microsoft.com/SQLServer/feedback/details/3120783
- Se ha corregido un problema que hacía que SSMS no pudiera enumerar los archivos de copia de seguridad en servidores con una intercalación que distingue mayúsculas de minúsculas. https://connect.microsoft.com/SQLServer/feedback/details/3134787 y https://connect.microsoft.com/SQLServer/feedback/details/3137000
- Diversas correcciones de Plan de presentación y de comparación de planes de presentación
- Se ha corregido un problema que hacía que el cuadro de diálogo Conexión no permitiera al usuario especificar el "protocolo de red" para usarlo en la conexión, a menos que SQL Server estuviera instalado en el equipo que ejecuta SSMS. https://connect.microsoft.com/SQLServer/feedback/details/3134997
- Se ha mejorado la compatibilidad para las configuraciones de varios monitores en las que algunos cuadros de dialogo de SSMS aparecían en ubicaciones "aleatorias". Se ha agregado una nueva opción "Cuadros de diálogo de tareas" en la configuración de usuario "Explorador de objetos de SQL Server | Comandos" para que permita recordar la posición de un cuadro de diálogo de tareas o una hoja de propiedades al cerrarse. https://connect.microsoft.com/SQLServer/feedback/details/889169, https://connect.microsoft.com/SQLServer/feedback/details/1158271, https://connect.microsoft.com/SQLServer/feedback/details/3135260 
- Se ha corregido un problema que hacía que SSMS no pudiera cambiar las propiedades de la base de datos para Azure SQL DB cifrada
- Se ha mejorado la opción "Descartar resultados tras la ejecución". https://connect.microsoft.com/SQLServer/feedback/details/1196581
- Se ha mejorado o corregido un problema que hacía que los usuarios no pudieran tener acceso a las suscripciones de Azure en que no eran administradores.
- Se ha mejorado el asistente para "Restaurar base de datos" para mantener seleccionada la base de datos de destino en OE independientemente de la selección de la base de datos de origen. https://connect.microsoft.com/SQLServer/feedback/details/3118581
- Se ha corregido un problema que hacía que el Explorador de objetos ordenara incorrectamente los "procedimientos almacenados compilados de forma nativa" que se acababan de agregar. https://connect.microsoft.com/SQLServer/feedback/details/3133365
- Se ha corregido un problema que hacía que "SELECCIONAR LAS PRIMERAS n FILAS" no incluyera la cláusula "PRIMERAS". Para Azure SQLDW. https://connect.microsoft.com/SQLServer/feedback/details/3133551 y https://connect.microsoft.com/SQLServer/feedback/details/3135874
- QueryStoreUI: se ha corregido un problema que hacía que los intervalos de tiempo no personalizados no funcionasen correctamente en todos los informes.
- Always Encrypted: se ha mejorado la mensajería del estado de permiso de AKV en el cuadro de diálogo Nuevo CMK. Se ha agregado información sobre herramientas en la lista desplegable CEK para que sea más fácil distinguir las CEK con nombres largos. Se ha corregido un problema por el que algunos proveedores de almacén de claves CNG no aparecían en el cuadro de diálogo Nueva clave maestra de columna de Always Encrypted.
- Se ha corregido el "Nombre de aplicación" incoherente de las conexiones de SSMS. https://connect.microsoft.com/SQLServer/feedback/details/3135115
- Se ha corregido un problema que hacía que SSMS no generara los scripts correctos para Azure SQL (tablas e índices con la opción DATA_COMPRESSIONS). https://connect.microsoft.com/SQLServer/feedback/details/3133148
- Se ha corregido un problema que hacía que el usuario no pudiera usar el método abreviado **CTRL + Q** para el inicio rápido (los nuevos enlaces de teclado para activar o desactivar la opción "IntelliSense habilitado" en el Editor de consultas son ahora **CTRL + B**, **CTRL + I**). https://connect.microsoft.com/SQLServer/feedback/details/3131968
- Se ha corregido un problema en "Restaurar base de datos" que hacía que SSMS produjera una excepción al intentar seleccionar una cuenta de almacenamiento de una suscripción que tiene cuentas con dominios personalizados definidos
- Se ha corregido un problema en "Diagrama de base de datos" que hacía que SSMS produjera el error "Índice fuera de los límites de la matriz"; además, el usuario no podía cambiar la "Vista de tabla" a nada que no fuera estándar. https://connect.microsoft.com/SQLServer/feedback/details/3133792 y https://connect.microsoft.com/SQLServer/feedback/details/3135326
- Se ha corregido un problema en "Copia de seguridad/restauración en URL" que hacía que SSMS no enumerara las cuentas de almacenamiento clásicas.
- Se ha corregido un problema que hacía que se iniciara una excepción al intentar agregar elementos protegibles enlazados al esquema a los roles de base de datos. https://connect.microsoft.com/SQLServer/feedback/details/3118143
- Se ha corregido un problema por el que SSMS mostraba de vez en cuando el error "Los datos tienen valor Null. No se puede llamar a este método o propiedad con valores Null" al expandir un nodo de tabla https://connect.microsoft.com/SQLServer/feedback/details/3136283
- DTA: Se ha corregido un problema que hacía que DTAEngine.exe finalizara con daños en el montón al evaluar la función de partición con determinados valores de límite.


**Analysis Services (AS)**

- Se ha corregido un problema que hacía que Restaurar base de datos de AS produjera un error si la base de datos tiene un nombre distinto al identificador.
- Se ha corregido un problema en la ventana Consulta DAX que pasaba por alto la opción de menú para alternar IntelliSense habilitado
- Se ha corregido un problema que impedía conectarse a SSAS a través de direcciones http/https de IIS de msmdpump
- Se permite la conexión a Azure AS con una contraseña que contenga un punto y coma.
- Al convertir en script el comando Restaurar base de datos de AS con la opción "Omitir pertenencia", se incluirá la nueva opción de JSON correspondiente cuando se use con el servidor de SQL Server 2017 AS o Azure AS
- Se ha corregido un problema muy poco habitual que podía hacer que el cuadro de diálogo Eliminar base de datos generara un error al cargar
- Se ha corregido un problema que podía producirse al intentar ver particiones en modelos de nivel de compatibilidad 1400 que contenían una mezcla de consulta SQL y definiciones de partición de M

**Integration Services (IS)**
- Se ha corregido un problema que hacía que no se pudieran mostrar informes de datos de ejecución del catálogo de SSISDB
- Se han solucionado problemas en SSMS relacionados con el rendimiento deficiente con un gran número de proyectos o paquetes

## <a name="downloadssdtmediadownloadpng-ssms-171httpsgomicrosoftcomfwlinklinkid849819"></a>![descargar](../ssdt/media/download.png) [SSMS 17.1](https://go.microsoft.com/fwlink/?linkid=849819)
Disponible con carácter general | Número de compilación: 14.0.17119.0

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40a)

### <a name="enhancements"></a>Mejoras

- Profiler: en Ayuda > Acerca de ahora se muestra el número de versión de lanzamiento (por ejemplo, 17.1).
- Los usuarios de Analysis Services pueden actualizar las credenciales de sus orígenes de datos de modelos TM 1200 y versiones posteriores desde el menú contextual del origen de datos.
- Los informes integrados de SSIS ahora muestran registros de la ejecución de escalado horizontal en CTP 2.1.
- Aplicación de administración de escalado horizontal de SSIS
  - Vea información básica sobre el patrón de escalabilidad horizontal.
  - Agregue fácilmente un trabajo a la implementación escalada.
  - Vea todos los trabajos de escalado horizontal y la información básica sobre ellos y también puede habilitar o deshabilitarlos fácilmente.

### <a name="bug-fixes"></a>Correcciones de errores
- AlwaysOn:
  - Se ha corregido un problema que hacía que las propiedades de una réplica de disponibilidad siempre aparecieran como modo de "Conmutación automática por error" para grupos de disponibilidad de WSFC.
  - Se ha corregido un problema que hacía que la lista de enrutamiento de solo lectura se sobrescribiera al actualizar el grupo de disponibilidad.
- Always Encrypted: se ha corregido un problema que hacía que en el archivo de registro generado faltara la información generada por DacFx.
- Plan de presentación: se ha corregido un problema que hacía que la interfaz de usuario mostrara siempre el atributo Tipo de combinación real para operadores de combinación no adaptables.
- Programa de instalación:
  - Se ha corregido un problema que hacía que SSMS 17.0 interrumpiera SSDT en Visual Studio 2013 [elemento de conexión 3133479].
  - Se ha corregido un problema que hacía que, al hacer clic en "Reiniciar" al final de la instalación, no se reiniciara el equipo.
- Scripting: se evita temporalmente que SSMS elimine de forma accidental objetos de base de datos de Azure al intentar incluir en script la eliminación al deshabilitar esa opción.  La corrección correcta estará en una próxima versión de SSMS.
- Explorador de objetos: se ha corregido un problema que hacía que no se expandiera el nodo "Bases de datos" al conectarse a una base de datos de Azure creada mediante "AS COPY".

## <a name="downloadssdtmediadownloadpng-ssms-170httpsgomicrosoftcomfwlinklinkid847722"></a>![descargar](../ssdt/media/download.png) [SSMS 17.0](https://go.microsoft.com/fwlink/?LinkID=847722)
Disponible con carácter general | Número de compilación: 14.0.17099.0

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x40a)

### <a name="enhancements"></a>Mejoras 

- Paquete de actualización y Windows Server Update Services (WSUS). Las versiones futuras 17.X incluyen una actualización acumulativa más pequeña. 
  - La actualización también se publicará en el catálogo de WSUS.  
- Se han actualizado los iconos para que sean coherentes con los iconos de VS Shell que se proporcionan y admiten resoluciones de valores altos de ppp. Nuevos iconos de programa para SSMS y Profiler a fin de diferenciar entre las versiones 16.X y 17.X.
- Módulo de SQL PowerShell
  - Se ha quitado el módulo de SQL Server PowerShell de SSMS y ahora se distribuye a través de la Galería de PowerShell (PowerShell 5.0 ahora debe admitir el control de versiones de módulo).
  - Mejoras varias con respecto a la "presentación" (formato) de algunos objetos SMO (por ejemplo, ahora las bases de datos muestran el tamaño y el espacio disponible, y las tablas muestran el recuento de filas y el uso del espacio).
  - Se ha agregado coloración cuando se invoca el símbolo del sistema de PowerShell desde el menú "Iniciar PowerShell" en OE.
  - Se agregaron los parámetros -ClusterType y -RequiredCopiesToCommit a los cmdlets de AG (los cmdlets New-SqlAvailabilityGroup, Join-SqlAvailabilityGroup y Set-SqlAvailabilityGroup)
  - Se agregaron los parámetros -ActiveDirectoryAuthority y -AzureKeyVaultResourceId al cmdlet Add-SqlAzureAuthenticationContext
  - Se han agregado los cmdlets Revoke-SqlAvailabilityGroupCreateAnyDatabase, Grant-SqlAvailabilityGroupCreateAnyDatabase y Set-SqlAvailabilityReplicaRoleToSecondary.
  - Se ha agregado el parámetro -seedingMode a los cmdlets Set-SqlAvailabilityReplica y New-SqlAvailabilityReplica.
  - Se ha agregado el parámetro -ConnectionString a Get-SqlDatabase.
- SQL Server en Linux: mejoras y correcciones generales para el trasvase de registros
  - Se ha agregado compatibilidad con rutas de acceso nativas de Linux para adjuntar, restaurar y realizar una copia de seguridad de la base de datos.
  - Se ha agregado compatibilidad con rutas de acceso nativas de Linux para la carpeta de destino del registro de auditoría.
- Analysis Services
  - Ventana Consulta DAX:
    - Coincidencia de paréntesis en el editor
    - Compatibilidad con la sintaxis DEFINE MEASURE y DEFINE VAR
    - Diversas mejoras de IntelliSense
  - Autenticación universal
    - Permite a los usuarios especificar un nombre de usuario y ninguna contraseña y el cuadro de diálogo de inicio de sesión de Azure controla la conexión.
  - Integración de SSMS PQ: 
    - Scripting de trabajos de orígenes de datos estructurados 
    - Ver y editar orígenes de datos estructurados en la interfaz de usuario de PQ
- Nueva plantilla "Agregar restricción única"
- Plan de presentación: se muestra el máximo en lugar de la suma de los subprocesos en la ventana Propiedades para el tiempo transcurrido. Se exponen nuevas propiedades del operador de concesión de memoria. Se habilitó el botón "Editar consulta" en Estadísticas de consultas dinámicas.
  - Nueva opción "Analizar el plan de ejecución real"
  - Mejoras generales en la comparación de planes de presentación
  - Se ha introducido una funcionalidad en la característica Comparación de plan de presentación para buscar diferencias significativas en la estimación de cardinalidad entre nodos coincidentes de dos planes de consulta y realizar un análisis básico de las posibles causas principales.
- Se quitó Configuration Manager del explorador de Servidores registrados
- Se habilita la lectura de los registros de auditoría desde Azure Blob Storage
- Se ha agregado parametrización para Always Encrypted. Consulte [esta página](https://blogs.msdn.microsoft.com/sqlsecurity/2016/12/13/parameterization-for-always-encrypted-using-ssms-to-insert-into-update-and-filter-by-encrypted-columns/) para obtener más detalles. 
- La conexión autenticada universal de AAD a la base de datos de Azure SQL admite identificadores de inquilino personalizados. 
- La opción Generar scripts de la base de datos de Azure SQL ahora genera scripts para texto completo, reglas y base de datos.
- Se ha corregido la personalización de marca en las pantallas de presentación de SSMS y del generador de perfiles.
- Se ha quitado de SSMS la interfaz de usuario del punto de control de la utilidad.
- SSMS ahora puede crear bases de datos de Azure SQL de la edición "PremiumRS".
- Grupos de disponibilidad AlwaysOn
  - Se ha agregado compatibilidad con nuevos tipos de clúster: EXTERNAL y NONE. Se ha agregado compatibilidad con SQL Server en Linux. Se ha agregado la propagación automática como una opción para la sincronización de datos inicial. Se han corregido algunos defectos, por ejemplo, el control de dirección URL del punto de conexión, la actualización de base de datos y el diseño de la interfaz de usuario. Se han quitado características relacionadas con la réplica de Azure.
  - Se ha mejorado IntelliSense para varias palabras clave de grupo de disponibilidad.
- Monitor de actividad
  - Se ha agregado un nuevo panel "Monitor de actividad" en la ventana de salida de SSMS.
  - Se ha cambiado el mensaje de error o tiempo de espera de conexión por información de registro en la ventana de salida, en lugar de un mensaje emergente.
  - Se ha quitado el gráfico vacío (5.º gráfico) en la sección Información general.
  - Se ha agregado "(en pausa)" al título Información general si se pausa la recopilación de datos del Monitor de actividad.
  - Extensiones Graph a SQL Server: nuevos iconos para el nodo de Graph y las tablas perimetrales. El nodo de Graph y las tablas perimetrales aparecerán en la carpeta Tablas de Graph. Plantillas disponibles para crear el nodo de Graph y tablas perimetrales.
- Modo de presentación: hay tres nuevas tareas disponibles a través de inicio rápido (Ctr-Q). PresentOn: active el modo de presentación. PresentEdit: edite los tamaños de las fuentes de la presentación para el modo de presentación.  "Fuente del Editor de texto" para el Editor de consultas.  "Fuente de entorno" para otros componentes.
RestoreDefaultFonts: revertir a la configuración predeterminada. Por el momento, no hay comando PresentOff. Use RestoreDefaultFonts para desactivar el modo de presentación*.

### <a name="bug-fixes"></a>Correcciones de errores

- Se ha corregido un problema por el que SSMS se bloqueaba cuando el plan de presentación se desplazaba mediante el panel táctil de Surface Book.
- Se ha corregido un problema que hacía que SSMS se bloqueara durante mucho tiempo al obtener las propiedades de una base de datos que se está restaurando o está sin conexión. 
- Se ha corregido un problema que hacía que el "Visor de ayuda" no se pudiera abrir en las compilaciones de RC.
- Se ha corregido un problema que hacía que los elementos del "cuadro de herramientas Tareas de planes de mantenimiento" pudieran faltar en SSMS.
- Se ha corregido un problema en SSMS que hacía que el usuario no pudiera reducir una base de datos cuando el nombre de la base de datos incluía llaves. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3122618)
- Se ha corregido un problema que hacía que, cuando SSMS intentaba generar el script de la eliminación de una base de datos de Azure, se eliminara la base de datos. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3131458/)
- Se ha corregido un error por el que los valores predeterminados no se podían incluir en scripts para los tipos de tabla definidos por el usuario. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3119027)
- Otra ronda de mejoras de rendimiento en torno a índices o menús contextuales. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3120783)
- Se corrigió un problema que provocaba parpadeo excesivo al mantener el puntero del mouse sobre un índice faltante en el plan de ejecución. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3118510)
- Se corrigió un problema en el que SSMS dejaba la base de datos sin conexión cuando genera scripts [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3118550)
- Correcciones varias de interfaz de usuario en versiones localizadas (no en inglés) de SSMS.
- Se corrigió un problema en que faltaba el nodo "Claves de Always Encrypted" cuando la plataforma de destino era SQL 2016 SP1 Standard Edition.
- Always Encrypted: el menú "Always Encrypted" se habilitaba de forma incorrecta cuando el destino era SQL 2016 RTM Standard Edition o los servidores SQL 2014 (y versiones posteriores). Se ha corregido un problema por el que IntelliSense informa de un error cuando se usa la sintaxis CREATE OR ALTER. Se ha corregido un problema por el que se produce un error de cifrado en caso de que CMK o CEK contengan caracteres que deben ser de escape, es decir, estar incluidos entre corchetes. Cuando se produce una excepción de memoria insuficiente en SSMS, el usuario recibe un error que sugiere el uso de PowerShell nativo (64 bits) en su lugar.
Se ha corregido un problema por el que el Asistente de AE no se ejecutaba si el usuario usaba suscripciones de Resource Group Manager en lugar de suscripciones clásicas de Azure. Se Ha corregido un problema en que el Asistente de AE mostraba un error si el usuario no tenía permisos en ninguna suscripción o no tenía instancias de Azure Key Vault en ninguna de ellas.
Se ha corregido un problema del Asistente de AE por el que la página de inicio de sesión de Azure Key Vault no mostraba suscripciones de Azure en caso de varias instancias de AAD. Se ha corregido un problema del Asistente de AE por el que la página de inicio de sesión de Azure Key Vault no mostraba suscripciones de Azure para las que el usuario tenía permisos de lectura.
  - Se ha corregido un problema que hacía que los archivos de recursos no cargaran correctamente, por lo que aparecían mensajes de error incorrectos.
- Se mejoró el contraste de los hipervínculos en la página de configuración de SSMS
- Se ha corregido un problema en que los nodos de PolyBase no se mostraban cuando se conectaba a SQL Server Express (2016 SP1)
- Se ha corregido un problema que hacía que SSMS no pudiera cambiar el nivel de compatibilidad de una base de datos de Azure a la versión 140.
- Se mejoró el rendimiento de Explorador de objetos cuando se expande la lista de bases de datos de Azure [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3100675)
- Se corrigió un problema en que el elemento de menú contextual "Ver registro de SQL Server" aparecía de forma incorrecta para los tipos de servidores no relacionales (AS\RS\IS) 
- Se corrigió un error en que la comprobación de la sintaxis de una consulta de partición de Analysis Services mediante la autenticación de SQL podía generar un mensaje de error de inicio de sesión
- Se corrigió un problema en que cambiar el nombre de un modelo tabular AS de nivel de compatibilidad 1400 de versión preliminar podía generar un error en SSMS
- Se ha corregido un problema del tipo "error de operación en el modelo" que podía producirse después de intentar una operación no válida en el servidor AS en circunstancias excepcionales, revertir los cambios locales después de que no se guardaran correctamente en el modelo.
- Se corrigió un error de escritura en el cuadro de diálogo emergente Sincronizar base de datos de Analysis Services
- Los cuadros de diálogo para realizar copia de seguridad y restaurar contenedor aparecen fuera de pantalla en varias configuraciones de monitor. 
- Se produce un error en la creación de SecurityPolicy si el nombre del objeto de destino contiene `]`.
- El menú "Abrir recientes" de SSMS 2016 no muestra los archivos guardados recientemente. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)
- Se ha quitado el restablecimiento de la configuración de usuario cuando se actualiza el shell de VS.
- Se ha corregido un problema que impedía que el usuario cambiase el nivel de compatibilidad de una base de datos en SQL Server 2017.
- Las ventanas de consulta que usan la autenticación universal de AAD no pueden actualizar la consulta después de una hora.
- Se ha quitado de SSMS la interfaz de usuario del punto de control de la utilidad.
- Las conexiones de autenticación universal de AD no pueden consultar datos después de la expiración del token inicial.
- No se pueden generar scripts para reglas de la base de datos de Azure SQL a esta misma base de datos.
- Se ha corregido un problema por el que SQL PowerShell no podía conectarse a instancias de SQL heredadas (2014 y versiones anteriores). [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/1138754/sql-server-sqlps-powershell-module-fails-connection-to-sql-2012-instance)
- Se ha corregido un problema que hacía que SSMS se bloquease cuando no podía importar servidores registrados.
- Se ha corregido un problema que hacía que SSMS se bloquease si un usuario tenía ciertos permisos en una base de datos.
- SSMS: las tablas desaparecen de la superficie de diseño mientras se revisan las vistas. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/2946125/ssms-tables-disappears-from-design-surface-while-reviewing-views) 
- La barra de desplazamiento de la tabla no permite al usuario desplazar el contenido de la tabla; solo lo permite la flecha arriba o abajo. También es posible desplazar el contenido de la tabla después de intentar desplazarse con la barra de desplazamiento, lo que es un error. [Artículo de Connect](
https://connect.microsoft.com/SQLServer/feedback/details/3106561/sql-server-manager-2016-bug-in-design-view) 
- Los servidores registrados no muestran iconos después de actualizar el nodo raíz.
- El botón de script para crear una base de datos en servidores de Azure v12 ejecuta el script y, después, muestra el mensaje "No hay ninguna acción para incluir en el script".
- El cuadro de diálogo Conectar al servidor de SSMS no borra la pestaña "Propiedades adicionales" para cada nueva conexión.
- El script Generar tareas no genera scripts de creación de base de datos para una base de datos de SQL Azure.
- La barra de desplazamiento aparece deshabilitada en el Diseñador de vistas.
- Las rutas de acceso de claves de AVK de Always Encrypted no incluyen identificadores de versión.
- Se ha reducido el número de consultas sobre la edición del motor en la ventana de consultas. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3113387)
- Los errores de Always Encrypted al actualizar los módulos después del cifrado se tratan incorrectamente.
- Se ha cambiado de 15 a 30 segundos el tiempo de espera predeterminado de conexión para OLTP y OLAP a fin de corregir una clase de errores de conexión que se omitían. 
- Se ha corregido un bloqueo en SSMS cuando se iniciaba un informe personalizado. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3118856)
- Se ha corregido un problema por el que se produce un error en "Generar script…" para bases de datos SQL de Azure.
- Se ha corregido la opción "Script como" y el "Asistente para generar scripts" para que no agreguen nuevas líneas adicionales al generar scripts para objetos, como procedimientos almacenados. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3115850)
- Proveedor SQLAS de PowerShell: se ha agregado la propiedad LastProcessed a las carpetas Dimension y MeasureGroup. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3111879)
- Estadísticas de consultas activas: se ha corregido un problema que hacía que solo se mostrase la primera consulta de un lote. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3114221)  
- Plan de presentación: se muestra el máximo en lugar de la suma de los subprocesos en la ventana Propiedades.
- Almacén de consultas: se ha agregado un nuevo informe en las consultas con una alta variación de ejecución.
- Problemas de rendimiento del explorador de objetos: el menú contextual [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3114074) de las tablas se bloquea momentáneamente. SSMS funciona con lentitud cuando se hace clic con el botón derecho en el índice de una tabla (a través de una conexión remota de Internet). Se impide la emisión de consultas de tabla que se ordenan en el servidor.
- Se ha quitado de SSMS el Asistente para la implementación de Azure (implementar la base de datos en la máquina virtual de Azure).
- Se ha corregido un problema que hacía que los índices que faltaban no se mostrasen en los planes de ejecución en SSMS. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3114194)
- Se ha corregido un problema común de bloqueo durante el apagado en SSMS.
- Se ha corregido un problema en el Explorador de objetos que provocaba un error al abrir el menú contextual de los nodos PolyBase|Grupo de escalado horizontal. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3115128)
- Se ha corregido un problema que podía hacer que SSMS se bloquease al intentar mostrar los permisos de una base de datos.
- Almacén de consultas: se han realizado mejoras generales en los elementos del menú contextual para las cuadrículas de resultados del informe del almacén de consultas.
- La configuración de Always Encrypted para una tabla existente produce errores en los objetos relacionados. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3103181)
- La Configuración de Always Encrypted para una base de datos existente con varios esquemas no funciona. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3109591)
- El Asistente para columnas cifradas de Always Encrypted produce un error debido a la base de datos que contiene vistas que hacen referencia a vistas del sistema. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3111925)
- Cuando se cifra mediante Always Encrypted, los errores al actualizar los módulos después del cifrado se tratan incorrectamente.
- Se ha corregido un problema de truncamiento de la interfaz de usuario del cuadro de diálogo "Nuevo registro de servidor".
- Se ha corregido la interfaz de usuario de la condición DMF, que actualizaba incorrectamente las expresiones con valores de constante de cadena que incluían comillas.
- Se ha corregido un problema que podía hacer que SSMS se bloquease al ejecutar informes personalizados.
- Se ha agregado el elemento de menú "Ejecución en escalabilidad horizontal..." al nodo de carpeta.
- Se ha corregido un problema con la característica de lista de direcciones IP permitidas de firewall de base de datos SQL de Azure.
- Se ha corregido un problema en SSMS que hacía que una referencia de objeto no estableciera la excepción al editar el origen de la partición multidimensional de AS.
- Se ha corregido un problema en SSMS que hacía que una referencia de objeto no estableciera la excepción al eliminar un ensamblado personalizado del servidor multidimensional de AS.
- Se ha corregido un problema que hacía que no se pudiera cambiar el nombre de una base de datos tabular 1400 de AS.
- Se ha corregido un problema con el scripting de un origen de datos tabular de AS de nivel de compatibilidad 1400 del cuadro de diálogo de propiedades de la conexión.
- Se ha quitado la suposición de que las tablas en el modelo de nivel de compatibilidad 1400 de AS tengan al menos una partición.
- Ctrl-R ahora alterna el panel de resultados en el editor de consultas DAX de SSMS.


## <a name="downloadssdtmediadownloadpng-ssms-1653httpsgomicrosoftcomfwlinklinkid840946"></a>![descargar](../ssdt/media/download.png) [SSMS 16.5.3](https://go.microsoft.com/fwlink/?LinkID=840946)
Disponible con carácter general | Número de compilación: 13.0.16106.4

[Chino (simplificado)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804)| [Chino (tradicional)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404)| [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409)| [Francés](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c)| [Alemán](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407)| [Italiano](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410)| [Japonés](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411)| [Coreano](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412)| [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416)| [Ruso](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419)| [Español](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)

Se han corregido los problemas siguientes en esta versión:

* Se ha corregido un problema detectado en SSMS 16.5.2 que provocaba la expansión del nodo "Tabla" cuando la tabla tenía más de una columna dispersa.

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
