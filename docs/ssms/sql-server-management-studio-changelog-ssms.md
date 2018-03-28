---
title: 'SQL Server Management Studio: Registro de cambios (SSMS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/20/2018
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9865ff96b084d70b3dcd067ad8d57c7cece01a62
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/21/2018
---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio: Registro de cambios (SSMS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
En este artículo, se proporcionan detalles sobre las actualizaciones, mejoras y correcciones de errores de las versiones actuales y anteriores de SSMS. Descargue las [versiones anteriores de SSMS a continuación](#previous-ssms-releases).


## <a name="ssms-176download-sql-server-management-studio-ssmsmd"></a>[SSMS 17.6](download-sql-server-management-studio-ssms.md)

Número de versión: 17.6<br>
Número de compilación: 14.0.17230.0<br>
Fecha de lanzamiento: 20 de marzo de 2018

### <a name="whats-new"></a>Novedades

**SSMS general**

Instancia administrada de SQL Database:

- Se ha agregado compatibilidad para [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance). Instancia administrada de Azure SQL Database (versión preliminar) es una nueva opción de Azure SQL Database, que proporciona una compatibilidad cercana al 100% con SQL Server local, una implementación nativa de [red virtual (VNet)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) que aborda cuestiones de seguridad comunes y un [modelo empresarial](https://azure.microsoft.com/pricing/details/sql-database/) favorable para los clientes de SQL Server local.
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

- Se ha corregido un problema en *Clasificación de datos* que provocaba que las clasificaciones que se acababan de agregar se mostrasen con un *tipo de información* y una *etiqueta de confidencialidad* obsoletos.
- Se ha corregido un problema por el que *Clasificación de datos* no funcionaba al fijar como destino un servidor establecido en una intercalación que distingue mayúsculas de minúsculas.
        
AlwaysOn:

- Se ha corregido un problema en la opción "Mostrar panel" de un grupo de disponibilidad por el que, al hacer clic en *Recopilar datos de latencia*, se podía producir un error cuando el servidor se establecía en una intercalación que distingue mayúsculas de minúsculas.
- Se ha corregido un problema por el que SSMS notificaba erróneamente un grupo de disponibilidad como *distribuido* al cerrar el Servicio de clúster.
- Se ha corregido un problema por el que, al crear un grupo de disponibilidad con el cuadro de diálogo *Crear grupo de disponibilidad*, se necesitaba una *ReadOnlyRoutingUrl*.
- Se ha corregido un problema por el que, cuando el servidor principal está inactivo y se efectúa una conmutación por error manual en el servidor secundario, se genera una excepción NullReferenceException.
- Se ha corregido un problema por el que, al crear un grupo de disponibilidad mediante la copia de seguridad o restauración para inicializar una base de datos, en las réplicas secundarias, los archivos de base de datos se creaban en el directorio predeterminado. La corrección incluye lo siguiente:
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

En este momento no hay ningún problema conocido en esta versión.

## <a name="previous-ssms-releases"></a>Versiones de SSMS anteriores

Para descargar las versiones anteriores de SSMS, haga clic en los vínculos de título de las secciones siguientes.

## <a name="downloadssdtmediadownloadpng-ssms-175httpsgomicrosoftcomfwlinklinkid867670"></a>![descargar](../ssdt/media/download.png) [SSMS 17.5](https://go.microsoft.com/fwlink/?linkid=867670)
Disponible con carácter general | Número de compilación: 14.0.17224.0

[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=867670&clcid=0x40a)

### <a name="whats-new"></a>Novedades

**SSMS general**

Clasificación y detección de datos:

- Se ha agregado una nueva característica de clasificación y detección de datos de SQL para detectar, clasificar, etiquetar y notificar información confidencial en las bases de datos. 
- La detección automática y la clasificación de la información más confidencial (empresarial, financiera, sanitaria, personal, etc.) pueden desempeñar un papel fundamental en el estado de protección de la información de la organización.
- Para más información, vea [Clasificación y detección de datos de SQL](../relational-databases/security/sql-data-discovery-and-classification.md).

Editor de consultas:

- Se ha agregado compatibilidad con la opción SkipRows al formato de archivo externo de texto delimitado para Azure SQL DW. Esta funcionalidad permite a los usuarios omitir un número especificado de filas al cargar archivos de texto delimitado en SQL DW. También se ha agregado la compatibilidad correspondiente de IntelliSense/SMO con la palabra clave FIRST_ROW. 

Plan de presentación:

- Se ha habilitado la presentación del botón de plan estimado para SQL Data Warehouse.
- Se ha agregado el nuevo atributo de plan de presentación *EstimateRowsWithoutRowGoal* y se han agregado nuevos atributos de plan de presentación a *QueryTimeStats*, *UdfCpuTime* y  *UdfElapsedTime*. Para más información, vea [Adición de información sobre el objetivo de filas del optimizador en el plan de ejecución en SQL Server 2017 CU3](http://support.microsoft.com/help/4051361).



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
- Se ha corregido un problema en la clase DatabaseScopedConfigurationCollection al controlar incorrectamente las intercalaciones (como resultado, un SSMS en ejecución en un equipo de agente de administración con una configuración regional en turco podría mostrar un error como "Legacy cardinality estimation is not valid scoped configuration" (La estimación de cardinalidad heredada no es una configuración con ámbito válida) al hacer clic con el botón derecho en una base de datos que se ejecutase en un servidor con una intercalación que distinguiera mayúsculas de minúsculas).
- Se ha corregido un problema en la clase JobServer que hacía que SMO no pudiera obtener las propiedades de Agente SQL en un servidor de SQL 2005 (como resultado, SSMS producía un error como "No se puede asignar un valor predeterminado a una variable local. Debe declarar la variable escalar "@ServiceStartMode" y, en última instancia, no mostraba el nodo de Agente SQL en el Explorador de objetos).

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
*Solución alternativa*: asigne el tipo de información y la etiqueta de confidencialidad nuevos después de volver a agregar la clasificación a la vista principal y antes de guardar.


## <a name="downloadssdtmediadownloadpng-ssms-174httpsgomicrosoftcomfwlinklinkid864329"></a>![descargar](../ssdt/media/download.png) [SSMS 17.4](https://go.microsoft.com/fwlink/?linkid=864329)
Disponible con carácter general | Número de compilación: 14.0.17213.0

[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=864329&clcid=0x40a)


### <a name="whats-new"></a>Novedades

**SSMS general**

Evaluación de vulnerabilidad:
- Se ha incluido un nuevo servicio de evaluación de vulnerabilidades de SQL para analizar las bases de datos con objeto de encontrar posibles vulnerabilidades y desviaciones con respecto a los procedimientos recomendados, como errores de configuración, permisos excesivos y datos confidenciales sin protección. 
- Los resultados de la evaluación incluyen pasos que requieren acción con los que se corrige cada problema y scripts de solución personalizados cuando proceda. El informe de evaluación se puede personalizar para ajustarse a cada entorno y adaptarse a los requisitos particulares. Obtenga más información en [Evaluación de vulnerabilidades de SQL](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment).

SMO:
- Se ha corregido un problema en el que *HasMemoryOptimizedObjects* iniciaba una excepción en Azure.
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
- Se han habilitado métodos abreviados de teclado (como CTRL+F para realizar búsquedas).
- Se han agregado las acciones database\_name y client\_hostname a los eventos pertinentes en las sesiones del generador de perfiles XEvent. Para que el cambio surta efecto, puede que sea necesario eliminar las instancias de sesión QuickSessionStandard o QuickSessionTSQL existentes en los servidores (vea el [artículo 3142981 de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3142981)).

Línea de comandos:
- Se ha agregado una nueva opción de línea de comandos ("-G") que sirve para conectar SSMS automáticamente a un servidor o a una base de datos por medio de la autenticación de Active Directory ("Integrado" o "Contraseña"). Para más información, vea [Ssms (Utilidad)](ssms-utility.md).

Asistente para la importación de archivos planos:
- Se ha agregado un método para seleccionar un nombre de esquema distinto del predeterminado ("dbo") al crear la tabla.

Almacén de consultas:
- Se ha restaurado el informe "Consultas con regresión" al expandir la lista de informes Almacén de consultas disponible.

**Integration Services (IS)**
- Se ha agregado una función de validación de paquetes al Asistente para la implementación que sirve para que el usuario averigüe qué componentes de los paquetes SSIS no se admiten en Azure-SSIS IR.

### <a name="bug-fixes"></a>Correcciones de errores

**SSMS general**

- Explorador de objetos:
    - Se ha corregido un problema por el que el nodo de función con valores de tabla no aparecía con las instantáneas de base de datos (vea el [artículo de Connect 3140161](https://connect.microsoft.com/SQLServer/feedback/details/3140161)).
    - Se ha mejorado el rendimiento al expandir el nodo *Bases de datos* cuando el servidor tiene bases de datos AUTOCLOSE.
- Editor de consultas:
    - Se ha corregido un problema por el que se producían errores en IntelliSense con usuarios que no tienen acceso a la base de datos maestra.
    - Se ha corregido un problema que hacía que SSMS se bloqueara en algunos casos cuando se cerraba la conexión con un equipo remoto (vea el [artículo de Connect 3142557](https://connect.microsoft.com/SQLServer/feedback/details/3142557)).
- Visor de XEvent:
    - Se ha vuelto a habilitar la funcionalidad para exportar a XEL.
    - Se han corregido problemas por los que, a veces, los usuarios no podían cargar un archivo XEL completo.
- Generador de perfiles XEvent:
    - Se ha corregido un problema que hacía que SSMS se bloqueara si un usuario no tenía el permiso *VER ESTADO DEL SERVIDOR*.
    - Se ha corregido un problema en el que, al cerrar la ventana de datos actualizados del generador de perfiles XEvent, no se detenía la sesión subyacente.
- Servidores registrados:
    - Se ha corregido un problema que hacía que el comando "Mover a…" dejara de funcionar (vea el [artículo de Connect 3142862](https://connect.microsoft.com/SQLServer/feedback/details/3142862) y el [artículo de Connect 3144359](https://connect.microsoft.com/SQLServer/feedback/details/3144359/)).
- SMO:
    - Se ha corregido un problema en el que el método TransferData en el objeto de transferencia no funcionaba.
    - Se ha corregido un problema por el que las bases de datos de servidor iniciaban una excepción con las bases de datos de SQL DW en pausa.
    - Se ha corregido un problema en el que, al crear scripts de bases de datos SQL en SQL DW, se generaban valores de parámetro de T-SQL incorrectos.
    - Se ha corregido un problema en el que, al crear el script de una base de datos extendida, se emitía incorrectamente la opción *DATA\_COMPRESSION*.
- Monitor de actividad de trabajo:
    - Se ha corregido un problema en el que el usuario obtenía un error "El índice estaba fuera del intervalo. Debe ser un valor no negativo e inferior al tamaño de la colección. 
        Nombre del parámetro: index (System.Windows.Forms)" al intentar filtrar por categoría (vea el [artículo de Connect 3138691](https://connect.microsoft.com/SQLServer/feedback/details/3138691)).
- Cuadro de diálogo de conexión:
    - Se ha corregido un problema en el que los usuarios del dominio sin acceso a un controlador de dominio de lectura/escritura no podían iniciar sesión en un servidor SQL Server por medio de la autenticación SQL (vea el [artículo de Connect 2373381](https://connect.microsoft.com/SQLServer/feedback/details/2373381)).
- Replicación:
    - Se ha corregido un problema en el que se mostraba un error similar a "No se puede aplicar el valor 'null' a la propiedad ServerInstance" al examinar las propiedades de una suscripción de extracción en SQL Server.
- Programa de instalación de SSMS:
    - Se ha corregido un problema que hacía que el programa de instalación de SSMS reconfigurara incorrectamente todos los productos instalados en el equipo.
- Configuración del usuario:
   - Con esta corrección, los usuarios de la nube al amparo del Gobierno de Estados Unidos tendrán acceso ininterrumpido a sus recursos de Azure SQL Database y ARM con SSMS a través de la autenticación universal y del inicio de sesión de Azure Active Directory.  Los usuarios con versiones anteriores de SSMS deberán abrir Herramientas|Opciones|Servicios de Azure y, en Administración de recursos, cambiar la configuración de la propiedad "Entidad de Active Directory" por https://login.microsoftonline.us.

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

[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=858904&clcid=0x40a)


### <a name="enhancements"></a>Mejoras

- Se ha agregado el nuevo asistente "Importar archivo plano" para simplificar la experiencia de importación de archivos CSV con un marco de trabajo inteligente, que ahora no exige prácticamente intervención por parte del usuario ni poseer conocimientos especializados sobre dominios. Para obtener detalles, vea [Importación de archivos planos mediante el asistente de SQL](../relational-databases/import-export/import-flat-file-wizard.md).
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
   - Se ha mejorado la experiencia "Observar datos en directo" cuando la base de datos predeterminada no es "master". [Artículo de Connect 1222582](https://connect.microsoft.com/SQLServer/feedback/details/1222582).
- Always On: se ha corregido el problema que podía producir un error "El registro de este conjunto de copia de seguridad finaliza en el LSN x, demasiado pronto para aplicarlo a la base de datos" en "Restaurar copias de seguridad de registro".
- Monitor de actividad de trabajo: se han corregido los iconos incoherentes. [Artículo de Connect 3133100](https://connect.microsoft.com/SQLServer/feedback/details/3133100).
- Almacén de consultas: se ha corregido el problema que hacía que el usuario no pudiera elegir un intervalo de fechas "personalizado" para los informes del almacén de consultas. Vinculado a los artículos de Connect siguientes.
   - [Artículo de Connect 3139842](https://connect.microsoft.com/SQLServer/feedback/details/3139842)
   - [Artículo de Connect 3139399](http://connect.microsoft.com/SQLServer/feedback/details/3139399)
- Se ha corregido el problema que hacía que el cuadro de diálogo de conexión no "borrara" la base de datos usada más recientemente cuando la información guardada tenía una base de datos con nombre y el usuario seleccionaba <default>.
- Scripting de objetos:
    - Se ha corregido un problema que hacía que "Generar script de base de datos" no funcionara y produjera un error cuando el usuario tenía una base de datos DW en pausa en el servidor, pero seleccionaba otra base de datos no DW e intentaba generar scripts de ella.
    - Se ha corregido el problema que hacía que el encabezado de los procedimientos almacenados generados por script no coincidiera con la configuración de script, lo que daba lugar a un script engañoso. [Artículo de Connect 3139784](http://connect.microsoft.com/SQLServer/feedback/details/3139784).
    - Se ha vuelto a habilitar el "botón Script" al seleccionar objetos de SQL Azure.
    - Se ha corregido el problema que hacía que SSMS no permitiera el scripting de "Alter" o "Execute" en algunos objetos (UDF, View, SP, Trigger) cuando se conectaba a una instancia de Azure SQL Database. [Artículo de Connect 3136386](https://connect.microsoft.com/SQLServer/feedback/details/3136386).
- Editor de consultas:
  - Se ha mejorado Intellisense al seleccionar instancias de Azure SQL Database.
  - Se ha corregido un problema que provocaba un error en las consultas debido a un token de autenticación expirado (autenticación universal).
  - Se ha mejorado Intellisense al trabajar con instancias de Azure SQL Database (en particular, al conectarse a Azure SQL Database, se usa la gramática más reciente de T-SQL (140)).
  - Se ha corregido el problema que hacía que, al abrir una ventana de consulta con una conexión a una base de datos no DW en un servidor, todas las ventanas de consulta subsiguientes de ese servidor a bases de datos DW produjeran distintos errores sobre tipos u opciones no compatibles.
- AlwaysOn:
   - Se ha agregado la columna Modo de propagación al panel Always On y a la página de propiedades del grupo de disponibilidad.
   - Se ha corregido el problema que hacía que no se pudiera crear un grupo de disponibilidad de Linux cuando el principal estaba en Windows. [Artículo de Connect 3139856](https://connect.microsoft.com/SQLServer/feedback/details/3139856).
- Se han corregido varios problemas de "memoria insuficiente" en SSMS al ejecutar consultas. [Artículo de Connect 2845190](https://connect.microsoft.com/SQLServer/feedback/details/2845190) y [artículo de Connect 3123864](https://connect.microsoft.com/SQLServer/feedback/details/3123864).
- Profiler: 
   - Se ha corregido el problema que hacía que Profiler no funcionara al seleccionar SQL 2005.
   - Se ha corregido el problema que hacía que Profiler no aceptara la opción de conexión "Confiar en certificado de servidor".
- Monitor de actividad: se ha corregido el problema que hacía que el Monitor de actividad no funcionara al apuntar a SQL Server en ejecución en Linux.
- Se ha corregido un problema con la clase de transferencia de SMO que hacía que no se transfirieran objetos de origen de datos externo o formato de archivo externo; ahora los objetos de estos tipos deben incluirse correctamente en la transferencia.
- Servidores registrados:
   - Se ha habilitado la consulta multiservidor para servidores de agente de usuario (se intenta usar el mismo token para cada servidor de agente de usuario del grupo).
- Autenticación universal de AD:
   - Se ha corregido el problema que hacía que no se admitiera la autenticación de Azure AD.
   - Se ha corregido el problema que hacía que el diseñador de tablas o vistas no funcionara.
   - Se ha corregido el problema que hacía que "Seleccionar las 1000 primeras filas" y "Editar las 200 primeras filas" no funcionaran.
- Restauración de bases de datos: se ha corregido un problema que hacía que la restauración omitiera la última carpeta de la ruta de acceso al mover archivos a una ubicación alternativa.
- Asistente para comprimir:
   - Se ha corregido un problema del asistente para administrar la compresión de índices; se ha corregido el problema que hacía que los asistentes para comprimir datos no funcionaran para SQL 2016 e inferior.
        https://connect.microsoft.com/SQLServer/feedback/details/3139342
   - Se ha agregado el asistente para comprimir a las tablas e índices de Azure.
- Plan de presentación: 
   - Se ha corregido el problema que hacía que no se reconocieran los operadores PDW.
- Propiedades del servidor:
   - Se ha corregido el problema que hacía que no se pudiera modificar la afinidad del procesador del servidor.


**Analysis Services (AS)**

- Se ha corregido una serie de problemas con el Asistente para la implementación para que admita modelos tabulares de nivel de compatibilidad 1400 y orígenes de datos de Power Query.
- El Asistente para la implementación ahora se puede implementar en Azure AS cuando se ejecuta desde la línea de comandos.
- Ahora, cuando se usa autenticación de Windows en Azure AS, el usuario ve correctamente el nombre de la cuenta de usuario en el Explorador de objetos.


### <a name="known-issues-in-this-173-release"></a>Problemas conocidos de la versión 17.3:

**SSMS general**

- La siguiente funcionalidad de SSMS no es compatible con la autenticación de Azure AD mediante UA con MFA:
   - El Asistente para la optimización de motor de base de datos no es compatible con la autenticación de Azure AD; hay un problema conocido que consiste en que el mensaje de error que se presenta al usuario es un poco críptico: "No se puede cargar el archivo o ensamblado 'Microsoft.IdentityModel.Clients.ActiveDirectory,..." en lugar del esperado: "El Asistente para la optimización de motor de base de datos no admite Microsoft Azure SQL Database. (DTAClient)".
- Al intentar analizar una consulta en DTA se produce un error: "El objeto debe implementar IConvertible. (mscorlib)".
- *Consultas con regresión* no aparece en la lista Almacén de consultas de informes del Explorador de objetos.
   - Solución: haga clic con el botón derecho en el nodo **Almacén de consultas** y seleccione **Ver consultas con regresión**.

**Integration Services (IS)**

- La [execution_path] de [catalog].[event_messagea] no es correcta para ejecuciones de paquetes en Escalabilidad horizontal. [execution_path] comienza con "\Package" en lugar del nombre de objeto del ejecutable del paquete. Al ver el informe general sobre ejecuciones de paquetes en SSMS, el vínculo de "Ruta de acceso de ejecución" de Información general de ejecución no puede funcionar. La solución es hacer clic en "Ver mensajes" en el informe general para comprobar todos los mensajes de eventos.


## <a name="downloadssdtmediadownloadpng-ssms-172httpsgomicrosoftcomfwlinklinkid854085"></a>![descargar](../ssdt/media/download.png) [SSMS 17.2](https://go.microsoft.com/fwlink/?linkid=854085)
Disponible con carácter general | Número de compilación: 14.0.17177.0

[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=854085&clcid=0x40a)

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
- Además, se ha publicado una nueva interfaz de CLI compatible con la configuración de administración de Azure AD para SQL Database y SQL Data Warehouse.

 Para obtener más información sobre los métodos de autenticación de Active Directory, vea [Autenticación universal con SQL Database y SQL Data Warehouse (compatibilidad de SSMS con MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) y [Configurar Multi-Factor Authentication de Azure SQL Database para SQL Server Management Studio](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure).

- La ventana de salida tiene entradas para las consultas que se ejecutan durante la expansión de los nodos del Explorador de objetos.
- Diseñador de vistas habilitado para instancias de Azure SQL Database.
- Han cambiado las opciones de scripting predeterminadas para incluir en script objetos desde el Explorador de objetos en SSMS:
  - Anteriormente, el valor predeterminado en una instalación nueva era que el destino de script generado tuviera la versión más reciente de SQL Server (actualmente, SQL Server 2017).
  - En SSMS 17.2 se ha agregado una nueva opción: *Coincidir configuración del script con origen*. Cuando se establece en *True*, el script generado tiene como destino la misma versión, tipo de motor y edición del motor que el servidor al que pertenece el objeto del que se crea el script.
  - El valor *Coincidir configuración del script con origen* se establece en *True* de forma predeterminada, por lo que las nuevas instalaciones de SSMS tendrán automáticamente la opción predeterminada de crear siempre el script de los objetos en el mismo destino que el servidor original.
  - Cuando el valor *Coincidir configuración del script con origen* se establece en *False*, se habilitarán las opciones de destino de scripting normales y funcionarán como lo hacían anteriormente.
    - Además, todas las opciones de scripting se han movido a su propia sección: *Opciones de versión*. Ya no están en *Opciones generales de scripting*.

- Se ha agregado compatibilidad con nubes nacionales en "Restore from URL".
- Los informes de QueryStoreUI ahora son compatibles con otras métricas (RowCount, DOP, tiempo de CLR, etc.) de sys.query_store_runtime_stats.
- IntelliSense ahora es compatible con Azure SQL Database.
    - https://connect.microsoft.com/SQLServer/feedback/details/3100677/ssms-2016-would-be-nice-to-have-intellisense-on-azure-sql-databases
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
  - Use CTRL+F.


**Analysis Services (AS)**

- Nueva selección de miembros del rol de AAD para usuarios sin direcciones de correo electrónico en modelos de Azure AS en SSMS

**Integration Services (IS)**

- Se ha agregado una nueva columna ("Recuento ejecutado") al informe de ejecución de SSIS

### <a name="known-issues-in-this-release"></a>Problemas conocidos de esta versión:

- Las ventanas de consulta que usan la autenticación "Active Directory - Universal compatible con MFA" pueden experimentar un error similar al siguiente, al intentar ejecutar una consulta después de que esté abierta durante una hora:

   `Msg 0, Level 11, State 0, Line 0
The connection is broken and recovery is not possible. The client driver attempted to recover the connection one or more times and all attempts failed. Increase the value of ConnectRetryCount to increase the number of recovery attempts.`

   Si se vuelve a ejecutar la consulta, se debería solucionar el error y realizar correctamente.

- No se admite la siguiente funcionalidad de SSMS para la autenticación de Azure AD mediante la autenticación universal con MFA:
  - El diseñador **Nueva tabla o vista** muestra el aviso de inicio de sesión antiguo y no funciona para la autenticación de Azure AD.
  - La característica **Editar las primeras 200 filas** no es compatible con la autenticación de Azure AD.
  - El componente **Servidor registrado** no es compatible con la autenticación de Azure AD.
  - El **Asistente para la optimización de motor de base de datos** no es compatible con la autenticación de Azure AD. Hay un problema conocido en el que el mensaje de error que se presenta al usuario no es nada útil: *No se puede cargar el archivo o ensamblado 'Microsoft.IdentityModel.Clients.ActiveDirectory,...* en lugar del que se espera *El Asistente para la optimización de motor de base de datos no admite Microsoft Azure SQL Database. (DTAClient)*.

**Analysis Services (AS)**

- El Explorador de objetos de SSAS no mostrará el nombre de usuario de autenticación de Windows en las propiedades de conexión de Azure AS.

### <a name="bug-fixes"></a>Correcciones de errores

- Se ha corregido un problema al intentar imprimir los resultados de una consulta (como texto).  https://connect.microsoft.com/SQLServer/feedback/details/3055225/
- Se ha corregido un problema que hacía que SSMS colocara incorrectamente tablas y otros objetos al incluir en script la eliminación de esos objetos en una base de datos de Azure SQL.
- Se ha corregido un problema que hacía que, en ocasiones, SSMS se negara a iniciar con un error como "No se encuentran uno o más componentes. Reinstale la aplicación".
- Se ha corregido un problema que hacía que el SPID en la interfaz de usuario de SSMS pudiera quedar obsoleto y desactualizado. https://connect.microsoft.com/SQLServer/feedback/details/1898875
- Se ha corregido un problema en el programa de instalación (silenciosa) de SSMS que hacía que el argumento /passive se tratara como /quiet.
- Se ha corregido un problema que hacía que SSMS produjera ocasionalmente un error de "Referencia de objeto no establecida en una instancia de un objeto" durante el inicio. http://connect.microsoft.com/SQLServer/feedback/details/3134698
- Se ha corregido un problema en el "Asistente para compresión de datos" que causaba que SSMS se bloqueara al pulsar "Calcular" en la tabla de Graph
- Se ha solucionado un problema de rendimiento al hacer clic con el botón derecho en un índice de una tabla (en una conexión a Internet lenta). https://connect.microsoft.com/SQLServer/feedback/details/3120783
- Se ha corregido un problema que hacía que SSMS no pudiera enumerar los archivos de copia de seguridad en servidores con una intercalación que distingue mayúsculas de minúsculas. http://connect.microsoft.com/SQLServer/feedback/details/3134787 y https://connect.microsoft.com/SQLServer/feedback/details/3137000
- Diversas correcciones de Plan de presentación y de comparación de planes de presentación
- Se ha corregido un problema que hacía que el cuadro de diálogo Conexión no permitiera al usuario especificar el "protocolo de red" para usarlo en la conexión, a menos que SQL Server estuviera instalado en el equipo que ejecuta SSMS. https://connect.microsoft.com/SQLServer/feedback/details/3134997
- Se ha mejorado la compatibilidad para las configuraciones de varios monitores en las que algunos cuadros de dialogo de SSMS aparecían en ubicaciones "aleatorias". Se ha agregado una nueva opción "Cuadros de diálogo de tareas" en la configuración de usuario "Explorador de objetos de SQL Server | Comandos" para que permita recordar la posición de un cuadro de diálogo de tareas o una hoja de propiedades al cerrarse. https://connect.microsoft.com/SQLServer/feedback/details/889169, https://connect.microsoft.com/SQLServer/feedback/details/1158271, https://connect.microsoft.com/SQLServer/feedback/details/3135260 
- Se ha corregido un problema que hacía que SSMS no pudiera cambiar las propiedades de la base de datos para Azure SQL DB cifrada
- Se ha mejorado la opción "Descartar resultados tras la ejecución". https://connect.microsoft.com/SQLServer/feedback/details/1196581
- Se ha mejorado o corregido un problema que hacía que los usuarios no pudieran tener acceso a las suscripciones de Azure en que no eran administradores.
- Se ha mejorado el asistente para "Restaurar base de datos" para mantener seleccionada la base de datos de destino en OE independientemente de la selección de la base de datos de origen. https://connect.microsoft.com/SQLServer/feedback/details/3118581
- Se ha corregido un problema que hacía que el Explorador de objetos ordenara incorrectamente los "procedimientos almacenados compilados de forma nativa" que se acababan de agregar. http://connect.microsoft.com/SQLServer/feedback/details/3133365
- Se ha corregido un problema que hacía que "SELECCIONAR LAS PRIMERAS n FILAS" no incluyera la cláusula "PRIMERAS". Para Azure SQLDW. https://connect.microsoft.com/SQLServer/feedback/details/3133551 y https://connect.microsoft.com/SQLServer/feedback/details/3135874
- QueryStoreUI: se ha corregido un problema que hacía que los intervalos de tiempo no personalizados no funcionasen correctamente en todos los informes.
- Always Encrypted:
    - Se ha mejorado la mensajería del estado de permiso de AKV en el cuadro de diálogo Nuevo CMK
    - Se ha agregado información sobre herramientas en la lista desplegable CEK para que sea más fácil distinguir las CEK con nombres largos
    - Se ha corregido un problema que hacía que algunos proveedores de almacén de claves CNG no aparecieran en el cuadro de diálogo Nueva clave maestra de columna de Always Encrypted
- Se ha corregido el "Nombre de aplicación" incoherente de las conexiones de SSMS. http://connect.microsoft.com/SQLServer/feedback/details/3135115
- Se ha corregido un problema que hacía que SSMS no generara los scripts correctos para SQL Azure (tablas e índices con la opción DATA_COMPRESSIONS). https://connect.microsoft.com/SQLServer/feedback/details/3133148
- Se ha corregido un problema que hacía que el usuario no pudiera usar el método abreviado CTRL+Q para el inicio rápido. Nota: Los nuevos enlaces de teclado para activar o desactivar la opción "IntelliSense habilitado" en el Editor de consultas son ahora CTRL+B, CTRL+I. https://connect.microsoft.com/SQLServer/feedback/details/3131968
- Se ha corregido un problema en "Restaurar base de datos" que hacía que SSMS produjera una excepción al intentar seleccionar una cuenta de almacenamiento de una suscripción que tiene cuentas con dominios personalizados definidos
- Se ha corregido un problema en "Diagrama de base de datos" que hacía que SSMS produjera el error "Índice fuera de los límites de la matriz"; además, el usuario no podía cambiar la "Vista de tabla" a nada que no fuera estándar. https://connect.microsoft.com/SQLServer/feedback/details/3133792 y http://connect.microsoft.com/SQLServer/feedback/details/3135326
- Se ha corregido un problema en "Copia de seguridad/restauración en URL" que hacía que SSMS no enumerara las cuentas de almacenamiento clásicas.
- Se ha corregido un problema que hacía que se iniciara una excepción al intentar agregar elementos protegibles enlazados al esquema a los roles de base de datos. https://connect.microsoft.com/SQLServer/feedback/details/3118143
- Se ha corregido un problema que hacía que SSMS mostrara de vez en cuando el error "Los datos tienen valor Null. No se puede llamar a este método o propiedad con valores Null" al expandir un nodo de tabla http://connect.microsoft.com/SQLServer/feedback/details/3136283
- DTA: Se ha corregido un problema que hacía que DTAEngine.exe finalizara con daños en el montón al evaluar la función de partición con determinados valores de límite.


**Analysis Services (AS)**

- Se ha corregido un problema que hacía que Restaurar base de datos de AS produjera un error si la base de datos tiene un nombre distinto al identificador.
- Se ha corregido un problema en la ventana Consulta DAX que pasaba por alto la opción de menú para alternar IntelliSense habilitado
- Se ha corregido un problema que impedía conectarse a SSAS a través de direcciones http/https de IIS de msmdpump
- Se permite la conexión a Azure AS con una contraseña que contenga un punto y coma
- Al convertir en script el comando Restaurar base de datos de AS con la opción "Omitir pertenencia", se incluirá la nueva opción de JSON correspondiente cuando se use con el servidor de SQL Server 2017 AS o Azure AS
- Se ha corregido un problema muy poco habitual que podía hacer que el cuadro de diálogo Eliminar base de datos generara un error al cargar
- Se ha corregido un problema que podía producirse al intentar ver particiones en modelos de nivel de compatibilidad 1400 que contenían una mezcla de consulta SQL y definiciones de partición de M

**Integration Services (IS)**
- Se ha corregido un problema que hacía que no se pudieran mostrar informes de datos de ejecución del catálogo de SSISDB
- Se han solucionado problemas en SSMS relacionados con el rendimiento deficiente con un gran número de proyectos o paquetes

## <a name="downloadssdtmediadownloadpng-ssms-171httpsgomicrosoftcomfwlinklinkid849819"></a>![descargar](../ssdt/media/download.png) [SSMS 17.1](https://go.microsoft.com/fwlink/?linkid=849819)
Disponible con carácter general | Número de compilación: 14.0.17119.0

[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=849819&clcid=0x40a)

### <a name="enhancements"></a>Mejoras

- Generador de perfiles: Ayuda > ahora muestra el número de versión de lanzamiento (por ejemplo, 17.1)
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

## <a name="downloadssdtmediadownloadpng-ssms-170httpgomicrosoftcomfwlinklinkid847722"></a>![descargar](../ssdt/media/download.png) [SSMS 17.0](http://go.microsoft.com/fwlink/?LinkID=847722)
Disponible con carácter general | Número de compilación: 14.0.17099.0

[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=847722&clcid=0x40a)

### <a name="enhancements"></a>Mejoras 

- Paquete de actualización y Windows Server Update Services (WSUS) 
    - Las versiones futuras 17.X incluyen una actualización acumulativa más pequeña. 
  - La actualización también se publicará en el catálogo de WSUS.  
- Actualizaciones de iconos
    - Se han actualizado los iconos para que sean coherentes con los iconos de VS Shell que se proporcionan y admiten resoluciones de valores altos de PPP.
    - Nuevos iconos de programa para SSMS y Profiler a fin de diferenciar entre las versiones 16.X y 17.X
- Módulo de SQL PowerShell
  - Se ha quitado el módulo de SQL Server PowerShell de SSMS y ahora se distribuye a través de la Galería de PowerShell (PowerShell 5.0 ahora debe admitir el control de versiones de módulo).
  - Mejoras varias con respecto a la "presentación" (formato) de algunos objetos SMO (por ejemplo, ahora las bases de datos muestran el tamaño y el espacio disponible, y las tablas muestran el recuento de filas y el uso del espacio).
  - Se ha agregado coloración cuando se invoca el símbolo del sistema de PowerShell desde el menú "Iniciar PowerShell" en OE.
  - Se agregaron los parámetros -ClusterType y -RequiredCopiesToCommit a los cmdlets de AG (los cmdlets New-SqlAvailabilityGroup, Join-SqlAvailabilityGroup y Set-SqlAvailabilityGroup)
  - Se agregaron los parámetros -ActiveDirectoryAuthority y -AzureKeyVaultResourceId al cmdlet Add-SqlAzureAuthenticationContext
  - Se han agregado los cmdlets Revoke-SqlAvailabilityGroupCreateAnyDatabase, Grant-SqlAvailabilityGroupCreateAnyDatabase y Set-SqlAvailabilityReplicaRoleToSecondary.
  - Se ha agregado el parámetro -SeedingMode a los cmdlets Set-SqlAvailabilityReplica y New-SqlAvailabilityReplica.
  - Se ha agregado el parámetro -ConnectionString a Get-SqlDatabase.
- SQL Server en Linux
    - Mejoras y correcciones generales para el trasvase de registros
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
- Showplan
    - Se muestra el máximo en lugar de la suma de los subprocesos en la ventana Propiedades para el tiempo transcurrido
    - Se exponen nuevas propiedades del operador de concesión de memoria
    - Se habilitó el botón "Editar consulta" en Estadísticas de consultas activas
    - Compatibilidad con la ejecución intercalada
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
- SSMS ahora puede crear bases de datos de SQL Azure de la edición "PremiumRS".
- Grupos de disponibilidad AlwaysOn
  - Se ha agregado compatibilidad con nuevos tipos de clúster: EXTERNAL y NONE.
    - Se ha agregado compatibilidad con SQL Server en Linux.
    - Se ha agregado la propagación automática como una opción para la sincronización de datos inicial.
    - Se han corregido algunos defectos, por ejemplo, el control de dirección URL del punto de conexión, la actualización de base de datos y el diseño de la interfaz de usuario.
    - Se han quitado características relacionadas con la réplica de Azure.
  - Se ha mejorado IntelliSense para varias palabras clave de grupo de disponibilidad.
- Monitor de actividad
  - Se ha agregado un nuevo panel "Monitor de actividad" en la ventana de salida de SSMS.
  - Se ha cambiado el mensaje de error o tiempo de espera de conexión por información de registro en la ventana de salida, en lugar de un mensaje emergente.
  - Se ha quitado el gráfico vacío (5.º gráfico) en la sección Información general.
  - Se ha agregado "(en pausa)" al título Información general si se pausa la recopilación de datos del Monitor de actividad.
  - Extensiones de Graph a SQL Server 
    - Nuevos iconos para las tablas perimetrales y de nodo de Graph
    - Las tablas perimetrales y de nodo de Graph se mostrarán en la carpeta Tablas de Graph
    - Hay disponibles plantillas para crear tablas perimetrales y de nodo de Graph
- Modo de presentación
    - 3 tareas nuevas disponibles a través de Inicio rápido (Ctr-Q)
    - PresentOn: active el modo de presentación
    - PresentEdit: edite los tamaños de las fuentes de la presentación para el modo de presentación.  "Fuente del Editor de texto" para el Editor de consultas.  "Fuente de entorno" para otros componentes.
    - RestoreDefaultFonts: revertir a la configuración predeterminada.
    - *Nota: Por el momento, no hay comando PresentOff.  Use RestoreDefaultFonts para desactivar el modo de presentación*

### <a name="bug-fixes"></a>Correcciones de errores

- Se ha corregido un problema que hacía que SSMS se bloqueara cuando el plan de presentación se desplazaba mediante el panel táctil de Surface Book.
- Se ha corregido un problema que hacía que SSMS se bloqueara durante mucho tiempo al obtener las propiedades de una base de datos que se está restaurando o está sin conexión. 
- Se ha corregido un problema que hacía que el "Visor de ayuda" no se pudiera abrir en las compilaciones de RC.
- Se ha corregido un problema que hacía que los elementos del "cuadro de herramientas Tareas de planes de mantenimiento" pudieran faltar en SSMS.
- Se ha corregido un problema en SSMS que hacía que el usuario no pudiera reducir una base de datos cuando el nombre de la base de datos incluía llaves. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3122618)
- Se ha corregido un problema que hacía que, cuando SSMS intentaba generar el script de la eliminación de una base de datos de Azure, se eliminara la base de datos. [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3131458/)
- Se corrigió un error en el que los valores predeterminados no se podían incluir en scripts para los tipos de tabla definidos por el usuario. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3119027)
- Otra ronda de mejoras de rendimiento en torno a índices o menús contextuales. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3120783)
- Se corrigió un problema que provocaba parpadeo excesivo al mantener el puntero del mouse sobre un índice faltante en el plan de ejecución. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3118510)
- Se corrigió un problema en el que SSMS dejaba la base de datos sin conexión cuando genera scripts [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3118550)
- Correcciones varias de interfaz de usuario en versiones localizadas (no en inglés) de SSMS.
- Se corrigió un problema en que faltaba el nodo "Claves de Always Encrypted" cuando la plataforma de destino era SQL 2016 SP1 Standard Edition.
- Always Encrypted
    - El menú "Always Encrypted" se habilita de forma incorrecta cuando la plataforma de destino era SQL 2016 RTM Standard Edition o cualquier servidor SQL 2014 (y anterior)
    - Se corrigió un problema en que IntelliSense informa un error cuando se usa la sintaxis CREATE OR ALTER
    - Se corrigió un problema en que el cifrado presenta un error si CMK/CEK contienen caracteres de escape, es decir, entre corchetes
    - Cuando se produce una excepción de memoria insuficiente en SSMS, el usuario ve un mensaje de error que sugiere usar en su lugar la instancia de PowerShell nativa (64 bits).
    - Se corrigió un problema en que el Asistente de AE presentaba errores si el usuario usaba suscripciones de Resource Group Manager en lugar de suscripciones clásicas de Azure
    - Se corrigió un problema en que el Asistente de AE mostraba un error incorrecto si el usuario no tenía permisos en ninguna suscripción o no tenía instancias de Azure Key Vault en ninguna de ellas.
    - Se corrigió un problema en el Asistente de AE en que la página de inicio de sesión de Azure Key Vault no mostraba suscripciones de Azure en caso de varias instancias de AAD
    - Se corrigió un problema en el Asistente de AE en que la página de inicio de sesión de Azure Key Vault no mostraba suscripciones de Azure para las que el usuario tenía permisos de lectura
  - Se ha corregido un problema que hacía que los archivos de recursos no cargaran correctamente, por lo que aparecían mensajes de error incorrectos.
- Se mejoró el contraste de los hipervínculos en la página de configuración de SSMS
- Se corrigió un problema en que los nodos de Polybase no se mostraban cuando se conectaba a SQL Server Express (2016 SP1)
- Se ha corregido un problema que hacía que SSMS no pudiera cambiar el nivel de compatibilidad de una base de datos de Azure a la versión 140.
- Se mejoró el rendimiento de Explorador de objetos cuando se expande la lista de bases de datos de Azure [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3100675)
- Se corrigió un problema en que el elemento de menú contextual "Ver registro de SQL Server" aparecía de forma incorrecta para los tipos de servidores no relacionales (AS\RS\IS) 
- Se corrigió un error en que la comprobación de la sintaxis de una consulta de partición de Analysis Services mediante la autenticación de SQL podía generar un mensaje de error de inicio de sesión
- Se corrigió un problema en que cambiar el nombre de un modelo tabular AS de nivel de compatibilidad 1400 de versión preliminar podía generar un error en SSMS
- Se corrigió un problema del tipo "error de operación en el modelo" que podía producirse después de intentar una operación no válida en el servidor AS en circunstancias excepcionales, revertir los cambios locales después de que no se guardaron correctamente en el modelo
- Se corrigió un error de escritura en el cuadro de diálogo emergente Sincronizar base de datos de Analysis Services
- Los cuadros de diálogo para realizar copia de seguridad y restaurar contenedor aparecen fuera de pantalla en varias configuraciones de monitor. 
- Se produce un error en la creación de SecurityPolicy si el nombre del objeto de destino contiene ].
- El menú "Abrir recientes" de SSMS 2016 no muestra los archivos guardados recientemente. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)
- Se ha quitado el restablecimiento de la configuración de usuario cuando se actualiza el shell de VS.
- Se ha corregido un problema que impedía que el usuario cambiase el nivel de compatibilidad de una base de datos en SQL Server 2017.
- Las ventanas de consulta que usan la autenticación universal de AAD no pueden actualizar la consulta después de una hora.
- Se ha quitado de SSMS la interfaz de usuario del punto de control de la utilidad.
- Las conexiones de autenticación universal de AD no pueden consultar datos después de la expiración del token inicial.
- No se pueden generar scripts para reglas de la base de datos de Azure SQL a esta misma base de datos.
- Se ha corregido un problema que hacía que SQL PowerShell no pudiese conectarse a instancias de SQL heredadas (2014 y versiones anteriores). [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/1138754/sql-server-sqlps-powershell-module-fails-connection-to-sql-2012-instance)
- Se ha corregido un problema que hacía que SSMS se bloquease cuando no podía importar servidores registrados.
- Se ha corregido un problema que hacía que SSMS se bloquease si un usuario tenía ciertos permisos en una base de datos. 
- SSMS: las tablas desaparecen de la superficie de diseño mientras se revisan las vistas. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/2946125/ssms-tables-disappears-from-design-surface-while-reviewing-views) 
- La barra de desplazamiento de la tabla no permite al usuario desplazar el contenido de la tabla; solo lo permite la flecha arriba o abajo. También es posible desplazar el contenido de la tabla después de intentar desplazarse con la barra de desplazamiento, lo cual es un error. [Artículo de Connect](
http://connect.microsoft.com/SQLServer/feedback/details/3106561/sql-server-manager-2016-bug-in-design-view) 
- Los servidores registrados no muestran iconos después de actualizar el nodo raíz.
- El botón de script para crear una base de datos en servidores de Azure v12 ejecuta el script y, después, muestra el mensaje "No hay ninguna acción para incluir en el script".
- El cuadro de diálogo Conectar al servidor de SSMS no borra la pestaña "Propiedades adicionales" para cada nueva conexión.
- El script Generar tareas no genera scripts de creación de base de datos para una base de datos de SQL Azure.
- La barra de desplazamiento aparece deshabilitada en el Diseñador de vistas.
- Las rutas de acceso de claves de AVK de Always Encrypted no incluyen identificadores de versión.
- Se ha reducido el número de consultas sobre la edición del motor en la ventana de consultas. [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3113387)
- Los errores de Always Encrypted al actualizar los módulos después del cifrado se tratan incorrectamente.
- Se ha cambiado de 15 a 30 segundos el tiempo de espera predeterminado de conexión para OLTP y OLAP a fin de corregir una clase de errores de conexión que se omitían. 
- Se ha corregido un bloqueo en SSMS cuando se iniciaba un informe personalizado. [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3118856)
- Se ha corregido un problema que hacía que se produjese un error en "Generar script…" para las bases de datos de SQL Azure.
- Se ha corregido la opción "Script como" y el "Asistente para generar scripts" para que no agreguen nuevas líneas adicionales al generar scripts para objetos, como procedimientos almacenados. [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3115850)
- Proveedor SQLAS de PowerShell: se ha agregado la propiedad LastProcessed a las carpetas Dimension y MeasureGroup. [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3111879)
- Estadísticas de consultas activas: se ha corregido un problema que hacía que solo se mostrase la primera consulta de un lote. [Artículo de Connect] (http://connect.microsoft.com/SQLServer/feedback/details/3114221)  
- Plan de presentación: se muestra el máximo en lugar de la suma de los subprocesos en la ventana Propiedades.
- Almacén de consultas: se ha agregado un nuevo informe en las consultas con una alta variación de ejecución.
- Problemas de rendimiento del explorador de objetos. [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3114074)
    - El menú contextual de las tablas se bloquea momentáneamente.
    - SSMS funciona con lentitud cuando se hace clic con el botón derecho en el índice de una tabla (a través de una conexión remota de Internet). 
    - Se impide la emisión de consultas de tabla que se ordenan en el servidor.
- Se ha quitado de SSMS el Asistente para la implementación de Azure (implementar la base de datos en la máquina virtual de Azure).
- Se ha corregido un problema que hacía que los índices que faltaban no se mostrasen en los planes de ejecución en SSMS. [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3114194)
- Se ha corregido un problema común de bloqueo durante el apagado en SSMS.
- Se ha corregido un problema en el Explorador de objetos que provocaba un error al abrir el menú contextual de los nodos PolyBase|Grupo de escalado horizontal. [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3115128)
- Se ha corregido un problema que podía hacer que SSMS se bloquease al intentar mostrar los permisos de una base de datos.
- Almacén de consultas: se han realizado mejoras generales en los elementos del menú contextual para las cuadrículas de resultados del informe del almacén de consultas.
- La configuración de Always Encrypted para una tabla existente produce errores en los objetos relacionados. [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3103181)
- La Configuración de Always Encrypted para una base de datos existente con varios esquemas no funciona. [Artículo de Connect] (http://connect.microsoft.com/SQLServer/feedback/details/3109591)
- El Asistente para columnas cifradas de Always Encrypted produce un error debido a la base de datos que contiene vistas que hacen referencia a vistas del sistema. [Artículo de Connect] (http://connect.microsoft.com/SQLServer/feedback/details/3111925)
- Cuando se cifra mediante Always Encrypted, los errores al actualizar los módulos después del cifrado se tratan incorrectamente.
- Se ha corregido un problema de truncamiento de la interfaz de usuario del cuadro de diálogo "Nuevo registro de servidor".
- Se ha corregido la interfaz de usuario de la condición DMF, que actualizaba incorrectamente las expresiones con valores de constante de cadena que incluían comillas.
- Se ha corregido un problema que podía hacer que SSMS se bloquease al ejecutar informes personalizados.
- Se ha agregado el elemento de menú "Execution in Scale Out…" (Ejecución en escalado horizontal…) al nodo de carpeta.
- Se ha corregido un problema con la característica de dirección IP de lista blanca de firewall de base de datos SQL de Azure.
- Se ha corregido un problema en SSMS que hacía que una referencia de objeto no estableciera la excepción al editar el origen de la partición multidimensional de AS.
- Se ha corregido un problema en SSMS que hacía que una referencia de objeto no estableciera la excepción al eliminar un ensamblado personalizado del servidor multidimensional de AS.
- Se ha corregido un problema que hacía que no se pudiera cambiar el nombre de una base de datos tabular 1400 de AS.
- Se ha corregido un problema con el scripting de un origen de datos tabular de AS de nivel de compatibilidad 1400 del cuadro de diálogo de propiedades de la conexión.
- Se ha quitado la suposición de que las tablas en el modelo de nivel de compatibilidad 1400 de AS tengan al menos una partición.
- Ctrl-R ahora alterna el panel de resultados en el editor de consultas DAX de SSMS.


## <a name="downloadssdtmediadownloadpng-ssms-1653httpgomicrosoftcomfwlinklinkid840946"></a>![descargar](../ssdt/media/download.png) [SSMS 16.5.3](http://go.microsoft.com/fwlink/?LinkID=840946)
Disponible con carácter general | Número de compilación: 13.0.16106.4

[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=840946&clcid=0x40a)

Se han corregido los problemas siguientes en esta versión:

* Se ha corregido un problema detectado en SSMS 16.5.2 que provocaba la expansión del nodo "Tabla" cuando la tabla tenía más de una columna dispersa.

* Los usuarios pueden implementar paquetes SSIS que contienen el Administrador de conexiones OData que se conectan a un recurso de Microsoft Dynamics AX/CRM Online en el catálogo de SSIS. Para obtener más información, vea [Administrador de conexiones OData](../integration-services/connection-manager/odata-connection-manager.md).

* La configuración de Always Encrypted en una tabla existente produce errores en los objetos relacionados. [Id. de Connect 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* La Configuración de Always Encrypted para una base de datos existente con varios esquemas no funciona. [Id. de Connect 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* El Asistente para columnas cifradas de Always Encrypted produce un error debido a la base de datos que contiene vistas que hacen referencia a vistas del sistema. [Id. de Connect 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* Cuando se cifra mediante Always Encrypted, los errores al actualizar los módulos después del cifrado se tratan incorrectamente.

* El menú *Abrir recientes* no muestra los archivos guardados recientemente. [Id. de Connect 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* SSMS funciona con lentitud cuando se hace clic con el botón derecho en el índice de una tabla (a través de una conexión remota de Internet). [Id. de Connect 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* Se ha corregido un problema de la barra de desplazamiento del Diseñador de SQL. [Id. de Connect 3114856](http://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* El menú contextual de las tablas se bloquea momentáneamente. 
 
* En algunas ocasiones, SSMS produce excepciones en el Monitor de actividad y se bloquea. [Id. de Connect 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* SSMS 2016 se bloquea con error "El proceso terminó debido a un error interno en el runtime de .NET en la dirección IP 71AF8579 (71AE0000) con el código de salida 80131506".


## <a name="ssms-1651"></a>SSMS 16.5.1
Disponible con carácter general | Número de compilación: 13.0.16100.1

* Se ha corregido un problema por el que Invoke-Sqlcmd insertaba erróneamente varias filas cuando se produce la restricción Check. [Microsoft Connect, n.º 811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

* Se ha corregido un problema en versiones de idiomas diferentes de ESN que no funcionaban completamente al crear Grupos de disponibilidad.

* Se ha corregido un problema por el que al hacer clic en el plan de consulta XML no se abría la IU de SSMS adecuada.


## <a name="downloadssdtmediadownloadpng-ssms-165httpgomicrosoftcomfwlinklinkid832812"></a>![descargar](../ssdt/media/download.png) [SSMS 16.5](http://go.microsoft.com/fwlink/?LinkID=832812)
Disponible con carácter general | Número de compilación: 13.0.16000.28


[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=832812&clcid=0x40a)

* Se ha corregido un problema de bloqueo que se producía al hacer clic en una base de datos con un nombre de tabla que contenía ";:".
* Se ha corregido un problema que ocasionaba que los cambios realizados en la página Modelo en la ventana de propiedades de base de datos tabular de AS creasen scripts fuera de la definición original. 
[Microsoft Connect, elemento n.º 3080744](https://connect.microsoft.com/SQLServer/feedback/details/3080744) 
* Se ha corregido el problema por el que los archivos temporales se agregan a la lista de "Archivos recientes".  
[Microsoft Connect, elemento n.º 2558789](https://connect.microsoft.com/SQLServer/feedback/details/2558789)
* Corregido el problema por el que se deshabilitaba el elemento del menú "Administrar compresión" para los nodos de la tabla de usuario en el árbol del explorador de objetos.  
[Microsoft Connect, elemento n.º 3104616](https://connect.microsoft.com/SQLServer/feedback/details/3104616)

* Se ha corregido el problema por el que el usuario no es capaz de establecer el tamaño de fuente para el explorador de objetos, el explorador del servidor registrado, el explorador de plantillas y los detalles del explorador de objetos. La fuente para los exploradores utilizada será la fuente del entorno.  
[Microsoft Connect, elemento n.º 691432](https://connect.microsoft.com/SQLServer/feedback/details/691432)

* Se ha corregido el problema por el que SSMS se vuelve a conectar siempre a la base de datos predeterminada cuando se pierde la conexión.  
[Microsoft Connect, elemento n.º 3102337](https://connect.microsoft.com/SQLServer/feedback/details/3102337)

* Se han corregido muchos de los problemas de valores de ppp altos en la ventana del editor de consultas y de administración de directivas, incluidos los iconos de los planes de ejecución.

* Se ha corregido el problema por el que faltaba la opción de configuración de color y fuente para eventos extendidos.

* Se ha corregido el problema de bloqueos de SSMS que se producían al cerrar la aplicación o al intentar mostrar el cuadro de diálogo de error.


## <a name="downloadssdtmediadownloadpng-ssms-1641-september-2016httpgomicrosoftcomfwlinklinkid828615"></a>![descargar](../ssdt/media/download.png) [SSMS 16.4.1 (septiembre de 2016)](http://go.microsoft.com/fwlink/?LinkID=828615)
Disponible con carácter general | Número de compilación: 13.0.15900.1

[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=828615&clcid=0x40a)

*  Se ha corregido un problema que producía un error al alterar o modificar un procedimiento almacenado:  
[Microsoft Connect, n.º 3103831](https://connect.microsoft.com/SQLServer/feedback/details/3103831)

* Nuevos cmdlets 'Read-SqlTableData', 'Read-SqlViewData' y 'Write-SqlTableData' para ver y escribir datos mediante PowerShell.  
[Trello Read-SqlTableData Card](https://trello.com/c/FXVUNJ8x/131-read-sqltabledata)  
[Microsoft Connect, nº 2685363](https://connect.microsoft.com/SQLServer/feedback/details/2685363)
    
* Nuevo cmdlet 'Add-SqlLogin' para permitir nuevos escenarios de administración de inicio de sesión mediante PowerShell.  
[Microsoft Connect, nº 2588952](https://connect.microsoft.com/SQLServer/feedback/details/2588952)
    
*  Compatibilidad y usabilidad mejoradas para usuarios que se conectan a varias nubes nacionales.
    
    
*  Se corrigió un problema donde se iniciaban excepciones de memoria agotada.  
[Microsoft Connect, nº 3062914](https://connect.microsoft.com/SQLServer/feedback/details/3062914)  
[Microsoft Connect, nº 3074856](https://connect.microsoft.com/SQLServer/feedback/details/3074856)
    
*  Se corrigió un problema donde el filtrado por esquema no era una opción de filtro válida.  
[Microsoft Connect, nº 3058105](https://connect.microsoft.com/SQLServer/feedback/details/3058105)  
[Microsoft Connect, nº 3101136](https://connect.microsoft.com/SQLServer/feedback/details/3101136)
    
*  Se corrigió un problema donde la ventana Monitor para una base de datos ajustada no estaría accesible.
    
*  Se corrigió un problema donde la Ayuda F1 siempre abría contenido en línea. Los usuarios ahora pueden seleccionar si prefieren ayuda en línea o sin conexión a través de la opción "Establecer preferencias de la Ayuda" en el menú Ayuda.   
[Microsoft Connect, nº 2826366](https://connect.microsoft.com/SQLServer/feedback/details/2826366)
    
*  Se corrigió un problema donde un modelo tabular de Analysis Services de 1200 niveles no generaría scripts de la contraseña para scripting, aunque la versión del servidor tuviera [objeto de modelo de cliente está ahora sincronizado antes de aplicar el script].
    
*  Se ha corregido un problema donde la opción "SELECT TOP N ROWS" generaba una sintaxis en desuso para el operador TOP.  
[Microsoft Connect, nº 3065435](https://connect.microsoft.com/SQLServer/feedback/details/3065435)
    
*  Se corrigieron varios problemas de diseño a lo largo de SSMS, incluida la página Propiedades de inicio de sesión y las opciones de ejecución de consultas avanzadas.   
[Microsoft Connect, nº 3058199](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect, nº 3079122](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect, nº 3071384](https://connect.microsoft.com/SQLServer/feedback/details/3071384)
    
*  Se corrigió un problema donde una solución se creaba automáticamente cada vez que un usuario abría una nueva ventana de consulta.   
[Microsoft Connect, nº 2924667](https://connect.microsoft.com/SQLServer/feedback/details/2924667)    
[Microsoft Connect, nº 2917742](https://connect.microsoft.com/SQLServer/feedback/details/2917742)   
[Microsoft Connect, nº 2612635](https://connect.microsoft.com/SQLServer/feedback/details/2612635)
    
*  Se corrigió un problema donde las tablas temporales no se podrían expandir en el Explorador de objetos en las bases de datos del sistema.  
[Microsoft Connect, nº 2551649](https://connect.microsoft.com/SQLServer/feedback/details/2551649)
    
*  Se ha corregido un problema por el que SSMS ejecutaba una consulta en SELECT @@trancount después de ejecutar un lote.    
[Microsoft Connect, nº 3042364](https://connect.microsoft.com/SQLServer/feedback/details/3042364)
    
*  Se ha corregido un problema en Analysis Services que producía que, al crear un script desde la página de propiedades de un servidor, se crease un cuadro de diálogo de conexión oculto.
    
*  Se corrigió un problema donde Ctrl+Q no seleccionaría la barra de herramientas Inicio rápido.
    
*  Se corrigió un problema donde el cambio de MaxSize de una base de datos mediante el cuadro de diálogo Propiedades del servidor se rompía para bases de datos > 2 TB.  
[Microsoft Connect, nº 1231091](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  Se corrigió un problema en el asistente Restaurar base de datos no aceptaría nombres de archivo con espacios en blanco iniciales:   
[Microsoft Connect, n.º 2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="downloadssdtmediadownloadpng-ssms-163-august-2016httpgomicrosoftcomfwlinklinkid824938"></a>![descargar](../ssdt/media/download.png) [SSMS 16.3 (agosto de 2016)](http://go.microsoft.com/fwlink/?LinkID=824938)
Disponible con carácter general | Número de versión: 13.0.15700.28


[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=824938&clcid=0x40a)

* Las versiones mensuales de SSMS ahora se marcan numéricamente.

* [Nueva opción de autenticación **'Autenticación universal de Active Directory'**](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Se trata de un mecanismo de autenticación basado en token impulsado por Azure Active Directory que es compatible con mecanismos de autenticación integrados, contraseñas y multifactor.

* Nuevas plantillas de eventos extendidos que coinciden con la funcionalidad de las plantillas de SQL Server Profiler [(Microsoft Connect, n.º 2543925)](../tools/sql-server-profiler/sql-server-profiler-templates.md).

* Nuevos cuadros de diálogo Crear base de datos y propiedades de bases de datos para Bases de datos SQL de Azure.

* Nuevos cmdlets 'Get-SqlLogin' y 'Remove-SqlLogin' para ayuda a realizar la administración de inicio de sesión de SQL Server con PowerShell.  
*Solicitudes de error de clientes vinculadas:*   
[Microsoft Connect, n.º 2588952.](https://connect.microsoft.com/SQLServer/feedback/details/2588952/)

* Nuevo cmdelt de PowerShell 'New-SqlColumnMasterKeySettings' que proporciona soporte para la creación de claves maestra de columna para proveedores arbitrarios y rutas de acceso de claves.

* Nuevo cuadro de diálogo 'Crear base de datos' para mejorar la creación de las bases de datos SQL de Azure en SSMS>

* Compatibilidad con el filtrado en el nodo 'Databases' del Explorador de objetos SSMS. Desplácese hasta el nodo 'Databases' en el Explorador de objetos y haga clic en el icono de filtro en la barra de herramientas del Explorador de objetos para filtrar la lista de bases de datos.

* Compatibilidad con cuentas de almacenamiento de tipo Azure-Resource Manager (ARM) en los asistentes de copia de seguridad y restauración.

* [Compatibilidad con la versión beta inicial para pantallas de alta resolución](https://blogs.msdn.microsoft.com/sqlreleaseservices/ssms-highdpi-support/).  
*Solicitudes de error de clientes vinculadas:*   
[Microsoft Connect, n.º 1129301](https://connect.microsoft.com/SQLServer/feedback/details/1129301/management-studio-is-unusable-on-a-4k-display), [Microsoft Connect, n.º 1858763](https://connect.microsoft.com/SQLServer/feedback/details/1858763/), [Microsoft Connect, n.º 1852671](https://connect.microsoft.com/SQLServer/feedback/details/1852671/), [Microsoft Connect, n.º 1487643](https://connect.microsoft.com/SQLServer/feedback/details/1487643/),  [Microsoft Connect, n.º 1355641](https://connect.microsoft.com/SQLServer/feedback/details/1355641/), [Microsoft Connect, n.º 2161595](https://connect.microsoft.com/SQLServer/feedback/details/2161595/), [Microsoft Connect, n.º 1854041](https://connect.microsoft.com/SQLServer/feedback/details/1854041/), [Microsoft Connect, n.º 1055617](https://connect.microsoft.com/SQLServer/feedback/details/1055617/), [Microsoft Connect, n.º 2448774](https://connect.microsoft.com/SQLServer/feedback/details/2448774/), [Microsoft Connect, n.º 1521405](https://connect.microsoft.com/SQLServer/feedback/details/1521405/), [Microsoft Connect, n.º 2117853](https://connect.microsoft.com/SQLServer/feedback/details/2117853/), [Microsoft Connect, n.º 2014256](https://connect.microsoft.com/SQLServer/feedback/details/2014256/), [Microsoft Connect, n.º 2162218](https://connect.microsoft.com/SQLServer/feedback/details/2162218/), [Microsoft Connect, n.º 2344551](https://connect.microsoft.com/SQLServer/feedback/details/2344551/), [Microsoft Connect, n.º 1664436](https://connect.microsoft.com/SQLServer/feedback/details/1664436/), [Microsoft Connect, n.º 2554043](https://connect.microsoft.com/SQLServer/feedback/details/2554043/), [Microsoft Connect, n.º 2983216](https://connect.microsoft.com/SQLServer/feedback/details/2983216/), [Microsoft Connect, n.º 2021706](https://connect.microsoft.com/SQLServer/feedback/details/2021706/)

* Mejoras del Asistente para la optimización de motor de base de datos para admitir una carga de trabajo de lectura automáticamente desde el almacén de consultas de SQL Server.

* Mejoras del Asistente para la optimización de motor de base de datos para mostrar las recomendaciones de índices para los índices de almacén de columnas en el clúster, índices de almacén de columnas que no están en el clúster e índices de almacenamiento de filas.

* Compatibilidad para enviar comandos de consola de base de datos (DBCC) mediante cmdlets de PowerShell de SQL Server Analysis Services.

* Corrección de errores para ver el texto no cifrado de columnas de objetos grandes (LOB) de descifrado AlwaysEncrypted en SSMS.  
*Solicitudes de error de clientes vinculadas:*   
[Microsoft Connect, n.º 2413024](https://connect.microsoft.com/SQLServer/feedback/details/2413024/cannot-view-cleartext-of-alwaysencrypted-lob-columns-in-ssms)

* Corrija los errores en el cuadro de diálogo de Always Encrypted para corregir bloqueos cuando los estilos visuales de Windows no estén habilitados (por ejemplo, habilitar la visualización de contraste alto).

* Corrección de errores para el error 'No se encontró el método', que impide la conexión con instancias de SQL Server.

* Corrección de errores de bloqueo SSMS al crear una función de partición con el desplazamiento de fecha y hora.

* Corrección de errores para agregar/quitar el requisito de Microsoft .NET 3.5 para iniciar la herramienta de administración de Distributed Replay (DReplay.exe).

* Corrección de errores en el Asistente para implementación de Analysis Services para admitir nombres de servidor completos.

* Corrección de errores en SSMS para mostrar las particiones en los modelos tabulares de Analysis Services con un modelo de compatibilidad de 2016.  
*Solicitudes de error de clientes vinculadas:*   
[Microsoft Connect, n.º 2845053](https://connect.microsoft.com/SQLServer/feedback/details/2845053/ssms-cannot-display-partitions-in-tabular-models-in-2016-compatibility-level) 

* Mejoras de rendimiento y correcciones de errores en los modelos tabulares de Analysis Services y objetos de administración compartida de SQL Server (SMO). 


---
## <a name="downloadssdtmediadownloadpng-ssms-july-2016-hotfix-updatehttpgomicrosoftcomfwlinklinkid822301"></a>![descargar](../ssdt/media/download.png) [Actualización de revisión de SSMS de julio de 2016](http://go.microsoft.com/fwlink/?LinkID=822301)
Disponible con carácter general | Número de versión: 13.0.15600.2

[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=822301&clcid=0x40a)

* **Corrija los errores en SSMS para habilitar elementos de menú de clic con el botón derecho que faltan**.  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2883440](https://connect.microsoft.com/SQLServer/feedback/details/2883440/lost-table-design-and-edit-top-n-rows-in-tables-context-menu)  
[Microsoft Connect, n.º 2909644](https://connect.microsoft.com/SQLServer/feedback/details/2909644/ssms-2016-is-missing-edit-options-against-sql-express-2014)  
[Microsoft Connect, n.º 2924345](https://connect.microsoft.com/SQLServer/feedback/details/2924345/some-ssms-object-explorer-right-click-menu-options-missing-in-july-update)

---
## <a name="ssms-july-2016-install-the-july-2016-hotfix"></a>SSMS, julio de 2016 (instalación de la revisión de julio de 2016)
Disponible con carácter general | Número de versión: 13.0.15500.91

* *Edición, 5 de julio:* compatibilidad mejorada para bases de datos tabulares de SQL Server 2016 (nivel de compatibilidad de 1200) en el cuadro de diálogo del proceso de Analysis Services y el Asistente para la implementación de Analysis Services.

* *Edición, 5 de julio:* opción nueva en el cuadro de diálogo de opciones de ejecución de consulta de SSMS para establecer "XACT_ABORT". Esta opción está habilitada de forma predeterminada en esta versión de SSMS e indica a SQL Server que revierta la transacción completa y anule el lote si se produce un error de tiempo de ejecución.

* Compatibilidad con Almacenamiento de datos SQL de Azure en SSMS.

* Actualizaciones importantes para el módulo de PowerShell de SQL Server. Esto incluye un nuevo [módulo de PowerShell de SQL y nuevos CMDLETs para Always Encrypted, Agente SQL y los registros de error de SQL](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update).

* Compatibilidad con la generación de scripts de PowerShell en el asistente para Always Encrypted.

* Tiempos de conexión significativamente mejorados para las bases de datos SQL de Azure.

* Nuevo cuadro de diálogo "Copia de seguridad en URL" para admitir la creación de credenciales de Azure Storage para copias de seguridad de bases de datos de SQL Server 2016. Este cuadro de diálogo proporciona una experiencia más sencilla para almacenar las copias de seguridad de la base de datos en una cuenta de Azure Storage.
 
* Nuevo cuadro de diálogo de restauración para simplificar la restauración de una copia de seguridad de una base de datos de SQL Server 2016 desde el servicio de almacenamiento de Microsoft Azure.
 
* Corrección de errores en el diseñador de consultas SSMS para permitir agregar tablas al diseñador si un usuario no tiene permisos SELECT sobre ellos.

* Corrección de errores para agregar compatibilidad con IntelliSense para las funciones 'TRY_CAST()' y 'TRY_CONVERT()'.  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, elemento n.º 2453461](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast).

* Corrección de errores del módulo de PowerShell para habilitar la carga de la extensión 'SQLAS' (Microsoft Connect, n.º 2544902).  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2544902](https://connect.microsoft.com/SQLServer/feedback/details/2544902/ssms-march-2016-refresh-sqlps-failed-to-load-the-sqlas-extension).

* Corrección de errores en la ventana del editor de SSMS para permitir arrastrar y colocar archivos abiertos de SQL.  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2690658](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios).

* Corrección de errores en el generador de perfiles para corregir el bloqueo del generador de perfiles al salir.  
*Solicitudes de error de clientes vinculadas:*  
[(Microsoft Connect, n.º 2616550)](https://connect.microsoft.com/SQLServer/feedback/details/2616550/sql-server-2016-rc2-profiler-version-13-0-1300-275-wont-close-after-trace-is-started-even-after-trace-is-stopped).  
[(Microsoft Connect, n.º 2319968)](https://connect.microsoft.com/SQLServer/Feedback/Details/2319968).

* Corrección de errores en SSMS para evitar el bloqueo al intentar editar un vínculo de unión en el diseñador de tablas de SSMS.  
*Solicitudes de error de clientes vinculadas:*  
[(Microsoft Connect, n.º 2721052)](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms).

* Corrección de errores en SSMS para habilitar la generación de scripts de base de datos para los miembros del rol db_owner.  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2869241](https://connect.microsoft.com/SQLServer/feedback/details/2869241/error-with-script-database-as-create-to-in-ssms-2008r2-and-ssms-2016-june).

* Corrección de errores en el editor de SSMS para quitar el retraso al cerrar una pestaña de consulta si el servidor se ha desconectado.  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2656058](https://connect.microsoft.com/SQLServer/feedback/details/2656058/ssms-2014-2016-query-tab-takes-significantly-longer-to-close-if-the-instance-it-was-connected-to-is-now-offline).

* Corrección de errores para habilitar la opción de copia de seguridad de bases de datos de SQL Server Express. 
*Solicitudes de error de clientes vinculadas:*  
[(Microsoft Connect, n.º 2801910)](https://connect.microsoft.com/SQLServer/feedback/details/2801910/ssms-2016-backup-option-not-appearing-in-tasks).  
[(Microsoft Connect, n.º 2874434)](https://connect.microsoft.com/SQLServer/feedback/details/2874434/backup-missing-from-tasks-context-menu-in-ssms-2016-when-you-are-connected-to-an-express-instance).

* Corrección de errores en Analysis Services para mostrar correctamente el proveedor de fuente de datos para modelos multidimensionales de Analysis Services.

----
## <a name="downloadssdtmediadownloadpng-ssms-june-2016httpgomicrosoftcomfwlinklinkid799832"></a>![descargar](../ssdt/media/download.png) [SSMS de junio de 2016](http://go.microsoft.com/fwlink/?LinkID=799832)
Disponible con carácter general | Número de versión: 13.0.15000.23

[Chino (República Popular China)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x804) | [Chino (Taiwán)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x404) | [Inglés (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x409) | [Francés](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40c) | [Alemán](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x410) | [Japonés](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x412) | [Portugués (Brasil)](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x416) | [Ruso](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x419) | [Español](https://go.microsoft.com/fwlink/?linkid=799832&clcid=0x40a)

* SSMS está generalmente disponible a partir de la versión de junio de 2016.

* Nuevo cuadro de diálogo de búsqueda rápida en SSMS que se integra mejor en el documento actual y permite realizar búsquedas mediante expresiones regulares. 
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/>

* Mejoras en el instalador de SSMS para que pueda realizar un seguimiento de los códigos de salida de proceso y progreso de instalación para instalaciones desatendidas mediante scripts.

* Corrija los errores en la ayuda F1 contextual de SSMS para ver correctamente los artículos y documentos de ayuda.

* Corrija los errores en la vista 'Consultas con regresión' del almacén de datos de consulta que creó que SSMS se bloqueara al desplazarse.

* Corrija los errores en el conector OLEDB de Excel Analysis Services para permitir las conexiones de Excel 2016 a SQL Server Analysis Services.

* Corrija los errores en el cuadro de diálogo de conexión de SSMS para mostrar el cuadro de diálogo de conexión en el mismo monitor que la ventana principal de SSMS en sistemas de varios monitores.  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/>
<https://connect.microsoft.com/SQLServer/feedback/details/755689/sql-server-management-studio-connect-to-server-popup-dialog/>  
<https://connect.microsoft.com/SQLServer/feedback/details/389165/sql-server-management-studio-gets-confused-dealing-with-multiple-displays/>

* Correcciones de errores en la experiencia de Always Encrypted. Se ha corregido en el que la opción de menú de Always Encrypted no estaba habilitada correctamente para las bases de datos de Stretch. También se ha corregido el error en el asistente de Always Encrypted donde no se ha utilizado correctamente el proveedor HSM de SafeNet (Luna SA).


## <a name="additional-downloads"></a>Descargas adicionales  
Para obtener una lista de todas las descargas de SQL Server Management Studio, consulte el [Centro de descargas de Microsoft](https://www.microsoft.com/en-us/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending).  
  
Para obtener la versión más reciente de SQL Server Management Studio, vea [Descargar SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
