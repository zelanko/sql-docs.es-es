---
title: 'SQL Server Management Studio: Registro de cambios (SSMS) | Microsoft Docs'
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3dc76cc1-3b4c-4719-8296-f69ec1b476f9
caps.latest.revision: 72
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 470e6c83318eaf8eb579d053f65b5353862eb4c7
ms.openlocfilehash: 23e304e52967d5d16672872d8d5712f26ef8c610
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="sql-server-management-studio---changelog-ssms"></a>SQL Server Management Studio - Changelog (SSMS)

## <a name="ssms-171-release"></a>Versión de SSMS 17.1
Disponible con carácter general | Número de compilación: 14.0.17119.0

### <a name="enhancements"></a>Mejoras

- Generador de perfiles: Ayuda > aproximadamente ahora muestra el número de versión de lanzamiento (por ejemplo, 17.1)
- Análisis de servicio a los usuarios puede actualizar las credenciales de sus orígenes de datos de 1200 los modelos de TM y versiones posteriores en el menú contextual en el origen de datos
- SSIS integrados informes ahora mostrar registros de ejecución de escalado horizontal SSIS en CTP 2.1
- Aplicación de administración de escalado horizontal SSIS
  - Ver información básica sobre el patrón de escalabilidad horizontal.
  - Agregar fácilmente un trabajo a la implementación de ampliación horizontal.
  - Ver todos los trabajadores de la escala horizontal y la información básica acerca de ellos y puede también habilitar o deshabilitar ellos fácilmente.

### <a name="bug-fixes"></a>Correcciones de errores
- AlwaysOn:
  - Se ha corregido un problema donde las propiedades de una réplica de disponibilidad siempre aparecía como "Conmutación automática por error" modo para grupos de disponibilidad de WSFC.
  - Se corrigió un problema en la que se ha sobrescrito la lista de enrutamiento de solo lectura al actualizar el grupo de disponibilidad
- Always Encrypted: corregido un problema en el archivo de registro generado faltaba la información generada por DacFx.
- Plan de presentación: se ha corregido en problema donde la interfaz de usuario siempre muestra el atributo de tipo de combinación real para operadores de combinación no es adaptable.
- Programa de instalación:
  - Se corrigió un problema donde 17,0 SSMS se interrumpa SSDT con Visual Studio 2013 [conectarse elemento 3133479]
  - Se corrigió un problema donde al hacer clic en "Reiniciar" al final del programa de instalación no se reiniciar el equipo
- Secuencias de comandos: evita temporalmente que SSMS de eliminación accidental de objetos de base de datos de Azure al intentar la eliminación de script al deshabilitar esa opción.  Corrección correcta estará en una próxima versión de SSMS.
- Explorador de objetos: se corrigió un problema donde no se ha expandido nodo "Bases de datos" cuando se conecta a una base de datos de Azure creado mediante "la copia AS"

## <a name="ssms-170-release"></a>Versión de SSMS 17,0
Disponible con carácter general | Número de compilación: 14.0.17099.0

### <a name="enhancements"></a>Mejoras 

- Paquete de actualización y Windows Software Update Services (WSUS) 
    - Las versiones futuras de 17.X incluyen un paquete de actualización acumulativa más pequeño 
  - El paquete de actualización también se publicarán en el catálogo de WSUS  
- Actualizaciones de iconos
    - Iconos se han actualizado para ser coherentes con los iconos de Shell de VS que se proporciona y admite resoluciones valores altos de PPP
    - Nuevos iconos de programa para SSMS y Profiler a fin de diferenciar entre las versiones 16.X y 17.X
- Módulo de SQL PowerShell
  - Módulo de PowerShell de SQL Server quitará SSMS y ahora se distribuye a través de la Galería de PowerShell (PowerShell 5.0 ahora debe para admitir el control de versiones de módulo)
  - Varias mejoras en la "presentación" (formato) de algunos objetos SMO (por ejemplo, las bases de datos ahora muestran el tamaño y el espacio disponible y el uso de recuento y el espacio de la fila del Mostrar tablas)
  - Colores agregados cuando se invoca la línea de comandos de PowerShell en el menú "Iniciar PowerShell" en Ayuda de OE
  - Se agregaron los parámetros -ClusterType y -RequiredCopiesToCommit a los cmdlets de AG (los cmdlets New-SqlAvailabilityGroup, Join-SqlAvailabilityGroup y Set-SqlAvailabilityGroup)
  - Se agregaron los parámetros -ActiveDirectoryAuthority y -AzureKeyVaultResourceId al cmdlet Add-SqlAzureAuthenticationContext
  - Revoke-SqlAvailabilityGroupCreateAnyDatabase agregada, Grant SqlAvailabilityGroupCreateAnyDatabase y SqlAvailabilityReplicaRoleToSecondary del conjunto de cmdlets
  - Parámetro - SeedingMode agregado a los cmdlets Set-SqlAvailabilityReplica y New-SqlAvailabilityReplica
  - Parámetro - ConnectionString agregado a Get-SqlDatabase
- SQL Server en Linux
    - Mejoras y correcciones generales para el trasvase de registros
  - Se agregó compatibilidad para rutas de acceso de Linux nativo adjuntar, base de datos de copia de seguridad y restauración
  - Se agregó compatibilidad para rutas de acceso de Linux nativo para la carpeta de destino de registro de auditoría
- Analysis Services
  - Ventana de consulta DAX:
    - Búsqueda de coincidencias en el editor de paréntesis
    - Compatibilidad con la sintaxis definir medida y defina VAR
    - Diversas mejoras de Intellisense
  - Autenticación universal
    - Permite a los usuarios especificar que un nombre de usuario y no hay ninguna contraseña y el cuadro de diálogo de inicio de sesión de Azure controla la conexión
  - Integración de SSMS PQ: 
    - Scripting de trabajos de orígenes de datos estructurados 
    - Visualización y edición de orígenes de datos estructurados en la interfaz de usuario de PQ
- Nueva plantilla "Agregar restricción única"
- Showplan
    - Se muestra el máximo en lugar de la suma de los subprocesos en la ventana Propiedades para el tiempo transcurrido
    - Se exponen nuevas propiedades del operador de concesión de memoria
    - Se habilitó el botón "Editar consulta" en Estadísticas de consultas activas
    - Compatibilidad con la ejecución intercalada
  - Nueva opción de "Analizar el Plan de ejecución real"
  - Mejoras generales para la comparación del plan de presentación
  - Introdujo funcionalidad en función de comparación del plan de presentación para buscar diferencias significativas en la estimación de cardinalidad entre nodos coincidentes de dos planes de consulta y realizar un análisis básico de las causas posibles
- Se quitó Configuration Manager del explorador de Servidores registrados
- Se habilita la lectura de los registros de auditoría desde Azure Blob Storage
- Se ha agregado parametrización para Always Encrypted. Consulte [esta página](https://blogs.msdn.microsoft.com/sqlsecurity/2016/12/13/parameterization-for-always-encrypted-using-ssms-to-insert-into-update-and-filter-by-encrypted-columns/) para obtener más detalles. 
- La conexión autenticada universal de AAD a la base de datos de Azure SQL admite identificadores de inquilino personalizados. 
- La opción Generar scripts de la base de datos de Azure SQL ahora genera scripts para texto completo, reglas y base de datos.
- Se ha corregido la personalización de marca en las pantallas de presentación de SSMS y del generador de perfiles.
- Se ha quitado de SSMS la interfaz de usuario del punto de control de la utilidad.
- SSMS ahora puede crear bases de datos de SQL Azure "PremiumRS" edition
- Grupos de disponibilidad AlwaysOn
  - Agregar compatibilidad con nuevos tipos de clúster: externos y ninguno
    - Agregar compatibilidad con SQL Server en Linux
    - Agregar la propagación automática como una opción para la sincronización de datos iniciales
    - Fija la algunos defectos, por ejemplo, dirección URL del extremo de control, la actualización de base de datos y el diseño de la interfaz de usuario
    - Características relacionadas con la réplica de Azure quitado
  - IntelliSense mejorada para varias palabras clave de grupo de disponibilidad
- Monitor de actividad
  - Ha agregado nuevo panel "Monitor de actividad" en la ventana de salida de SSMS
  - Cambiar el mensaje de error o tiempo de espera de conexión para registrar información para generar la ventana, en lugar de un mensaje emergente
  - Vacío quitado del gráfico (gráfico de 5) en la sección información general
  - Agrega "(en pausa)" al título de la información general sobre si se detiene la recopilación de datos del Monitor de actividad
  - Extensiones de gráfico a las tablas de nodo y el borde del gráfico de SQL Server - nuevos iconos para las tablas de nodo y el borde del gráfico - se mostrarán en la carpeta tablas de gráfico: plantillas para crear tablas disponibles de nodo y el borde del gráfico
- Modo de presentación
    - 3 tareas nuevas disponibles a través de Inicio rápido (Ctr-Q)
    - PresentOn: active el modo de presentación
    - PresentEdit: edite los tamaños de las fuentes de la presentación para el modo de presentación.  "Fuente del Editor de texto" para el Editor de consultas.  "Fuente de entorno" para otros componentes.
    - RestoreDefaultFonts: revertir a la configuración predeterminada.
    - *Nota: Por el momento, no hay comando PresentOff.  Use RestoreDefaultFonts para desactivar el modo de presentación*

### <a name="bug-fixes"></a>Correcciones de errores

- Se corrigió un problema donde SSMS bloqueado al plan de presentación se desplaza a través de la pantalla táctil surfacebook
- Se corrigió un problema donde SSMS se bloquea durante mucho veces al obtener las propiedades de una base de datos que se va a restaurar o sin conexión 
- Se corrigió un problema donde "Visor de ayuda" no se pudo abrir en las compilaciones RC
- Se corrigió un problema donde los elementos "Herramientas de tareas de planes de mantenimiento" pueden faltar en SSMS.
- Se corrigió un problema en SSMS donde el usuario no pudo reducir una base de datos cuando el nombre de la base de datos incluye llaves. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3122618)
- Se corrigió un problema donde estaba intentando SSMS generar el script de la eliminación de un Azure base de datos causa la eliminación de la base de datos. [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3131458/)
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
  - Se corrigió un problema donde los archivos de recursos pueden no cargarse correctamente, por lo que genera mensajes de error incorrectos
- Se mejoró el contraste de los hipervínculos en la página de configuración de SSMS
- Se corrigió un problema en que los nodos de Polybase no se mostraban cuando se conectaba a SQL Server Express (2016 SP1)
- Se corrigió un problema donde SSMS es no se puede cambiar el nivel de compatibilidad de una base de datos de Azure en v140
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
- Se ha corregido un problema que impedía que el usuario pueda cambiar el nivel de compatibilidad de una base de datos en SQL Server 2017.
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
- Estadísticas de consultas activas: se ha corregido un problema que hacía que solo se mostrase la primera consulta de un lote. [Conectar elemento] (http://connect.microsoft.com/SQLServer/feedback/details/3114221)  
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
- La Configuración de Always Encrypted para una base de datos existente con varios esquemas no funciona. [Conectar elemento] (http://connect.microsoft.com/SQLServer/feedback/details/3109591)
- El Asistente para columnas cifradas de Always Encrypted produce un error debido a la base de datos que contiene vistas que hacen referencia a vistas del sistema. [Conectar elemento] (http://connect.microsoft.com/SQLServer/feedback/details/3111925)
- Cuando se cifra mediante Always Encrypted, los errores al actualizar los módulos después del cifrado se tratan incorrectamente.
- Se ha corregido un problema de truncamiento de la interfaz de usuario del cuadro de diálogo "Nuevo registro de servidor".
- Se ha corregido la interfaz de usuario de la condición DMF, que actualizaba incorrectamente las expresiones con valores de constante de cadena que incluían comillas.
- Se ha corregido un problema que podía hacer que SSMS se bloquease al ejecutar informes personalizados.
- Se ha agregado el elemento de menú "Execution in Scale Out…" (Ejecución en escalado horizontal…) al nodo de carpeta.
- Se corrigió un problema con la característica de direcciones de base de datos de SQL Azure firewall lista blanca de direcciones IP
- Un problema en SSMS que produjo una referencia de objeto que no establezca excepción al editar el origen de partición multidimensional fijo
- Un problema en SSMS que produjo una referencia de objeto que no establezca excepción al eliminar un ensamblado de cliente de AS multidimensionales fijo server
- Se corrigió un problema donde no pudo cambiar el nombre de una base de datos de 1400 tabular de AS
- Se corrigió un problema con un nivel de compatibilidad de 1400 de secuencias de comandos como origen de datos tabular de cuadro de diálogo de propiedades de conexión
- Quitar la suposición de que las tablas en que el modelo de nivel de compatibilidad de 1400 tengan al menos una partición
- CTRL-R alterna ahora el panel de resultados en el editor de consultas de SSMS DAX


## <a name="ssms-1653-release"></a>Versión de SSMS 16.5.3
Disponible con carácter general | Número de compilación: 13.0.16106.4

Se han corregido los problemas siguientes en esta versión:

* Se ha corregido un problema detectado en SSMS 16.5.2 que provocaba la expansión del nodo "Tabla" cuando la tabla tenía más de una columna dispersa.

* Los usuarios pueden implementar paquetes SSIS que contienen el Administrador de conexiones OData que se conectan a un recurso de Microsoft Dynamics AX/CRM Online en el catálogo de SSIS. Para obtener más información, vea [Administrador de conexiones OData](https://msdn.microsoft.com/library/dn584133.aspx).

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


## <a name="ssms-1651-release"></a>Versión de SSMS 16.5.1
Disponible con carácter general | Número de compilación: 13.0.16100.1

* Se ha corregido un problema por el que Invoke-Sqlcmd insertaba erróneamente varias filas cuando se produce la restricción Check. [Microsoft Connect, n.º 811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

* Se ha corregido un problema en versiones de idiomas diferentes de ESN que no funcionaban completamente al crear Grupos de disponibilidad.

* Se ha corregido un problema por el que al hacer clic en el plan de consulta XML no se abría la IU de SSMS adecuada.


## <a name="ssms-165-release"></a>Versión de SSMS 16.5
Disponible con carácter general | Número de compilación: 13.0.16000.28

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


## <a name="ssms-1641-september-2016-release"></a>SSMS 16.4.1, versión de septiembre de 2016
Disponible con carácter general | Número de compilación: 13.0.15900.1

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
    
*  Se corrigió un problema donde opción “SELECT TOP N ROWS” generaba una sintaxis en desuso para el operador TOP.  
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
[Microsoft Connect, n.º 1231091](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  Se corrigió un problema en el asistente Restaurar base de datos no aceptaría nombres de archivo con espacios en blanco iniciales:   
[Microsoft Connect, n.º 2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="ssms-163-august-2016-release"></a>Versión de SSMS 16.3 (agosto de 2016)
Disponible con carácter general | Número de versión: 13.0.15700.28

* Las versiones mensuales de SSMS ahora se marcan numéricamente.

* [Nueva opción de autenticación **'Autenticación universal de Active Directory'**](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Se trata de un mecanismo de autenticación basado en token impulsado por Azure Active Directory que es compatible con mecanismos de autenticación integrados, contraseñas y multifactor.

* Nuevas plantillas de eventos extendidos que coinciden con la funcionalidad de las plantillas de SQL Server Profiler [(Microsoft Connect, n.º 2543925)](https://connect.microsoft.com/SQLServer/feedback/details/2543925/sql-server-extended-events-profiler-tool). Obtenga más información acerca de las [plantillas de SQL Server Profiler](https://msdn.microsoft.com/library/ms190176.aspx).

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
## <a name="ssms-july-2016-hotfix-update-release"></a>Versión de actualización de revisión SSMS, julio de 2016 
Disponible con carácter general | Número de versión: 13.0.15600.2

* **Corrija los errores en SSMS para habilitar elementos de menú de clic con el botón derecho que faltan**.  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2883440](https://connect.microsoft.com/SQLServer/feedback/details/2883440/lost-table-design-and-edit-top-n-rows-in-tables-context-menu)  
[Microsoft Connect, n.º 2909644](https://connect.microsoft.com/SQLServer/feedback/details/2909644/ssms-2016-is-missing-edit-options-against-sql-express-2014)  
[Microsoft Connect, n.º 2924345](https://connect.microsoft.com/SQLServer/feedback/details/2924345/some-ssms-object-explorer-right-click-menu-options-missing-in-july-update)

---
## <a name="ssms-july-2016-release"></a>Versión SSMS, julio de 2016 
Disponible con carácter general | Número de versión: 13.0.15500.91

* *Edición, 5 de julio:*  **compatibilidad mejorada para bases de datos tabulares de SQL Server 2016 (nivel de compatibilidad de 1200) en el cuadro de diálogo del proceso de Analysis Services y el Asistente para la implementación de Analysis Service**.

* *Edición, 5 de julio:*  **opción nueva en el cuadro de diálogo de opciones de ejecución de consulta de SSMS para establecer 'XACT_ABORT'. Esta opción está habilitada de forma predeterminada en esta versión de SSMS e indica a SQL Server que revierta la transacción completa y anule el lote si se produce un error de tiempo de ejecución**.

* **Compatibilidad con Almacenamiento de datos SQL de Azure en SSMS.**

* **Actualizaciones importantes para el módulo de PowerShell de SQL Server. Esto incluye un nuevo [módulo de PowerShell de SQL y nuevos CMDLET para Always Encrypted, Agente SQL y los registros de error de SQL](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update)**.

* **Compatibilidad con la generación de scripts de PowerShell en el asistente para Always Encrypted**.

* **Tiempos de conexión significativamente mejorados para las bases de datos SQL de Azure.**

* **Nuevo cuadro de diálogo de copia de seguridad en la dirección URL para admitir la creación de credenciales de Almacenamiento de Azure para copias de seguridad de la base de datos de SQL Server 2016. Esto proporciona una experiencia más sencilla para almacenar las copias de seguridad de la base de datos en una cuenta de almacenamiento de Azure.**
 
* **Nuevo cuadro de diálogo de restauración para simplificar la restauración de una copia de seguridad de una base de datos de SQL Server 2016 desde el servicio de almacenamiento de Microsoft Azure.**
 
* **Corrección de errores en el diseñador de consultas SSMS para permitir agregar tablas al diseñador si un usuario no tiene permisos SELECT sobre ellos.**

* **Corrección de errores para agregar compatibilidad con IntelliSense para las funciones "TRY_CAST()" y "TRY_CONVERT()".**  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, elemento n.º 2453461](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast).

* **Corrección de errores del módulo de PowerShell para habilitar la carga de la extensión Analysis Services de "SQLAS".**  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2544902](https://connect.microsoft.com/SQLServer/feedback/details/2544902/ssms-march-2016-refresh-sqlps-failed-to-load-the-sqlas-extension).

* **Corrección de errores en la ventana del editor de SSMS para permitir arrastrar y colocar archivos abiertos de SQL.**  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2690658](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios).

* **Corrección de errores en el generador de perfiles para corregir el bloqueo del generador de perfiles al salir.**  
*Solicitudes de error de clientes vinculadas:*  
[(Microsoft Connect, n.º 2616550)](https://connect.microsoft.com/SQLServer/feedback/details/2616550/sql-server-2016-rc2-profiler-version-13-0-1300-275-wont-close-after-trace-is-started-even-after-trace-is-stopped).  
[(Microsoft Connect, n.º 2319968)](https://connect.microsoft.com/SQLServer/Feedback/Details/2319968).

* **Corrección de errores en SSMS para evitar el bloqueo al intentar editar un vínculo de unión en el diseñador de tablas de SSMS.**  
*Solicitudes de error de clientes vinculadas:*  
[(Microsoft Connect, n.º 2721052)](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms).

* **Corrección de errores en SSMS para habilitar la generación de scripts de base de datos para los miembros del rol db_owner.**  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2869241](https://connect.microsoft.com/SQLServer/feedback/details/2869241/error-with-script-database-as-create-to-in-ssms-2008r2-and-ssms-2016-june).

* **Corrección de errores en el editor de SSMS para quitar el retraso al cerrar una pestaña de consulta si el servidor se ha desconectado.**  
*Solicitudes de error de clientes vinculadas:*  
[Microsoft Connect, n.º 2656058](https://connect.microsoft.com/SQLServer/feedback/details/2656058/ssms-2014-2016-query-tab-takes-significantly-longer-to-close-if-the-instance-it-was-connected-to-is-now-offline).

* **Corrección de errores para habilitar la opción de copia de seguridad de bases de datos de SQL Server Express.**  
*Solicitudes de error de clientes vinculadas:*  
[(Microsoft Connect, n.º 2801910)](https://connect.microsoft.com/SQLServer/feedback/details/2801910/ssms-2016-backup-option-not-appearing-in-tasks).  
[(Microsoft Connect, n.º 2874434)](https://connect.microsoft.com/SQLServer/feedback/details/2874434/backup-missing-from-tasks-context-menu-in-ssms-2016-when-you-are-connected-to-an-express-instance).

* **Corrección de errores en Analysis Services para mostrar correctamente el proveedor de fuente de datos para modelos multidimensionales de Analysis Services.**

----
## <a name="ssms-june-2016-generally-available-release"></a>Versión de disponibilidad general SSMS de junio de 2016
Disponible con carácter general | Número de versión: 13.0.15000.23

* **SSMS está generalmente disponible a partir de la versión de junio de 2016.**

* **Nuevo cuadro de diálogo de búsqueda rápida en SSMS que se integra mejor en el documento actual y permite realizar búsquedas mediante expresiones regulares.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/>

* **Mejoras en el instalador de SSMS para que pueda realizar un seguimiento de los códigos de salida de proceso y progreso de instalación para instalaciones desatendidas mediante secuencias de comandos.**

* **Corrección de errores en la ayuda F1 contextual de SSMS para ver correctamente los artículos y documentos de ayuda.**

* **Corrección de errores en la vista "Consultas con regresión" del almacén de datos de consulta que provocaban que SSMS se bloquease al desplazarse.** 

* **Corrección de errores en el conector OLEDB de Excel Analysis Services para permitir las conexiones de Excel 2016 a SQL Server Analysis Services.**

* **Corrección de errores en el cuadro de diálogo de conexión de SSMS para mostrar el cuadro de diálogo de conexión en el mismo monitor que la ventana principal de SSMS en sistemas de varios monitores.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/>
<https://connect.microsoft.com/SQLServer/feedback/details/755689/sql-server-management-studio-connect-to-server-popup-dialog/>  
<https://connect.microsoft.com/SQLServer/feedback/details/389165/sql-server-management-studio-gets-confused-dealing-with-multiple-displays/>

* **Correcciones de errores en la experiencia de Always Encrypted. Se ha corregido en el que la opción de menú de Always Encrypted no estaba habilitada correctamente para las bases de datos de Stretch. También se ha corregido el error en el asistente de Always Encrypted por el que no se ha utilizaba correctamente el proveedor HSM de SafeNet (Luna SA).**

---
## <a name="ssms-april-2016-preview"></a>Versión preliminar de SafeNet, abril de 2016 
Número de versión: 13.0.14000.36
  
* **Mejora en el instalador de SSMS para agregar mensajes de error legibles.**  
  
* **Mejora en el Asistente para la base de datos de Stretch para agregar compatibilidad con predicados**.  
  
* **Mejora en el cmdlet de AlwaysEncrypted Powershell para agregar las API de cifrado de clave**.  
  
* **Corrección de errores para desactivar IntelliSense en la barra de herramientas SSMS si se ha deshabilitado en el cuadro de diálogo Opciones, Herramientas.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2555163/sql-2016-rc2-turning-off-intellisense-from-options-does-not-turn-it-off-on-toolbar/>  
    
* **Las mejoras y correcciones de errores en la interfaz de usuario de comparación de Showplan para reducir el espacio utilizado por los planes de consulta largos**.  
  
* **Correcciones de errores en SSMS para corregir los problemas que causaron que SSMS se bloqueara al salir**.   
  
* **Correcciones de errores en el asistente de Always Encrypted para conservar los permisos de usuario durante el cifrado y para permitir que la base de datos separara las operaciones una vez completado el asistente**.  
  
* **Corrección de errores en el cuadro de diálogo de nueva clave maestra de columna de Always Encrypted para proporcionar comentarios sobre el intento de generar una clave mediante un proveedor de algoritmo criptográfico (CNG) no admitido.**  
  
---  
## <a name="ssms-march-2016-preview-refresh"></a>Actualización de versión preliminar de SSMS, marzo de 2016
Número de versión: 13.0.13000.55
  
* **SSMS utiliza el shell aislado de Visual Studio 2015.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2390544/update-ssms-to-use-visual-studio-2015-dependencies/>  
  
* **Nueva barra de herramientas de inicio rápido que le ayuda a encontrar rápidamente elementos del menú y opciones. (VS 2015, shell aislado)**  
  
* **Mejoras en las opciones de temas de SSMS para agregar compatibilidad para un tema claro de SSMS. (VS 2015, shell aislado)**  
  
* **Corrección de errores en la opción del menú de herramientas de SSMS para restablecer correctamente los accesos directos de consulta si se presiona el botón "Restablecer valores predeterminados".**  
  
* **Corrección de errores en las nuevas plantillas de proyecto de SSMS para mostrar los nombres de plantilla fácilmente legibles.**  
  
* **Error resuelto con la visualización del historial de trabajos del Agente SQL en SSMS.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2458860/error-viewing-job-history-microsoft-datawarehouse-sqm/>  
    
* **Corrección de errores para permitir la instalación sin conexión de SSMS. Esto le permite instalar sin necesidad de una conexión a Internet. (VS 2015, shell aislado)**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2497178/cannot-install-ssms-when-server-has-no-internet-access/>  
    
* **Corrección de errores para conservar el directorio actual del usuario cuando se importa el módulo de SQL Server PowerShell (SQLPS).**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2434605/loading-sqlps-module-changes-current-directory-to-ps-sqlserver/>  
    
* **Corrección de errores en el módulo de SQL Server PowerShell (SQLPS) para usar los verbos de PowerShell aprobados.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2432891/sqlps-module-uses-unapproved-powershell-verbs/>  
    
* **Corrección de errores en el módulo de SQL Server PowerShell (SQLPS) para cargar el módulo más rápido.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2429153/sqlps-module-is-slow-to-load/>  
    
* **Corrección de errores en los pasos de trabajo del Agente SQL para permitir la modificación del paso de trabajo.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2453996/issues-with-agent-in-ssms-2016-rc0-13-0-12000-65/>  
    
* **Corrección de errores en el Explorador de objetos de SSMS para enumerar las tablas alfabéticamente.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2424718/sql-server-2016-ssms-table-list-confusing/>  
    
* **Corrección de errores en la lista desplegable "bases de datos disponibles" para mostrar la lista exacta de los nombres de base de datos cuando se modifica una conexión de SQL Server.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2513420/available-databases-drop-down-box-does-not-update-when-connection-changes-in-ssms/>  
    
* **Corrección de errores en los métodos abreviados de teclado de SSMS para centrarse en la lista desplegable "bases de datos disponibles" con la pulsación de tecla "CTRL+U"**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2534820/ssms-ctrl-u-doesnt-work/>  
  
---  
## <a name="ssms-march-2016-preview"></a>Versión preliminar de SSMS, marzo de 2016 
Número de versión: 13.0.12500.29 
  
* **Mejora en el instalador web de SSMS para permitir la navegación utilizando las teclas del teclado.**  
  
* **Mejora en el Asistente de AlwaysEncrypted para admitir tipos de datos de alias para el cifrado.**  
  
* **Corrección de errores en el asistente "Nuevo grupo de disponibilidad" de AlwaysOn para mostrar el número correcto de destinos máximos de conmutación por error automática.**  
*Solicitudes de error de clientes vinculadas:* <https://connect.microsoft.com/SQLServer/feedback/details/2333670/ssms-is-showing-the-wrong-number-of-maximum-automatic-failover-targets/>  
    
* **Corrección de errores en el instalador web de SSMS para corregir los errores que afectan a la instalación.**  
*Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2181548/sql-server-2016-ctp-3-2-management-studio-setup/>  
    
* **Corrección de errores en la versión de versión preliminar de SSMS para habilitar el guardado de planes de mantenimiento en SQL Server 2012 y versiones inferiores.**  
      
* **Correcciones de errores en el Asistente para la copia de seguridad para permitir varios nombres de copia de seguridad personalizados para las copias de seguridad seccionadas y para mostrar el nombre de archivo de copia de seguridad adecuado si se escribe un nombre nuevo después de seleccionar una credencial de almacenamiento.**  
  
---  
## <a name="ssms-february-2016-preview"></a>Versión preliminar de SSMS, febrero de 2016 
Número de versión: 13.0.12000.65
  
* **Mejora en el monitor de actividad para mostrar las opciones de texto cuando se habilita la configuración de alto contraste en SSMS.**  
  
* **Mejora en el cuadro de diálogo del asistente de Always Encrypted para mostrar una advertencia si se va a cambiar la intercalación de una columna durante el proceso de cifrado.**  
  
* **Mejora en la administración de directivas para agregar compatibilidad para la creación de condiciones en las claves de cifrado de columnas, los valores de clave de cifrado de columnas y las claves maestras de columnas.**  
  
* **Corrección de errores para mejorar el uso del cuadro de diálogo de limpieza de clave maestra de Always Encrypted y mensajes de error de Always Encrypted.**  
  
* **Corrección de errores para deshabilitar la rotación de claves maestras de la columna de Always Encrypted si solo existe una clave.**  
  
* **Corrección de errores para el error "inicializador de tipo" que se produce si el cuadro de diálogo de Always Encrypted se inicia mediante la versión de enero de SSMS o la versión de SSMS incluida en el medio de RC0 de SQL Server.**  
  
---  
## <a name="ssms-january-2016-preview"></a>Versión preliminar de SSMS, enero de 2016 
Número de versión: 13.0.11000.78 
  
* **Corrección de errores en SSMS para permitir que se eliminen las sesiones de eventos extendidos (XEvent).**  
  
* **Corrección de errores para poder abrir el cuadro de diálogo Propiedades de un grupo de disponibilidad de SQL Server 2014.**  
 *Solicitudes de error de clientes vinculadas:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/1609719/>  
     
* **Corrección de errores para poder agregar una réplica de Azure a un grupo de disponibilidad.**  
 *Solicitudes de error de clientes vinculadas:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2029135/>  
     
* **Corrección de errores para poder abrir el cuadro de diálogo Propiedades de las bases de datos de SQL Server 2014.**  
 *Solicitudes de error de clientes vinculadas:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2080209/>  
     
* **Corrección de errores destinada a quitar las columnas duplicadas que aparecen para cada tabla cuando se conectan a una base de datos de SQL Azure.**  
 *Solicitudes de error de clientes vinculadas:*  
 <https://connect.microsoft.com/SQLServer/feedback/details/2103116/>  
---  
## <a name="ssms-december-2015-preview"></a>Versión preliminar de SSMS, diciembre de 2015 
Número de versión: 13.0.900.73
  
* **Mejoras en la comparación de plan de presentación para habilitar la comparación del plan de ejecución de consulta actual con uno guardado en un archivo.**  
  
* **Compatibilidad con IntelliSense mejorada para los índices de almacén de columnas insertados en SSMS.**  
  
* **Corrección de errores en el asistente para la sesión de Eventos extendidos para habilitar la selección de plantillas cuando se conecte a un servidor Azure V12.**  
  
* **Nuevas tabulaciones en los cuadros de diálogo "Crear auditoría" y "Nuevo inicio de sesión" de la carpeta de seguridad para permitir una navegación más sencilla mediante el teclado.**  
  
* **Corrección de errores para habilitar la funcionalidad para "Cambiar a la pestaña de resultados tras la ejecución de la consulta" si SSMS está establecido para mostrar los resultados en formato de cuadrícula.**   
 *Solicitudes de error de clientes vinculadas:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1390296/switch-to-results-tab-after-query-execution-grid-mode-in-ssms-2016>  
  
* **Corrección de errores para mostrar los encabezados de columna sin truncar si SSMS se establece para mostrar los resultados en formato de cuadrícula.**  
 *Solicitudes de error de clientes vinculadas:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/2004111/bugbash-column-headers-in-grid-mode-truncated-with-courier-new-8>  
      
* **Correcciones de errores para permitir la correcta instalación del instalador web SSMS.**  
 *Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/2003865/ssms-october-preview-incoherent-error-message>  
<https://connect.microsoft.com/SQLServer/feedback/details/2079557/unable-to-instal-sql-server-update-13-0-800-111-over-13-0-700-242-error-code-2711>  
  
---  
## <a name="ssms-november-2015-preview"></a>Versión preliminar de SSMS, noviembre de 2015
Número de versión: 13.0.800.111
  
* **Compatibilidad con el ajuste de escala de mapa de bits para las pantallas con valores altos de PPP en SSMS.**  
  
* **Mejoras en la interfaz de usuario de asistentes y cuadros de diálogo de AlwaysEncrypted para simplificar el proceso de creación de claves de cifrado de base de datos.**  
  
* **Nueva opción del menú contextual en la lista de "Procesos" del monitor de actividad para ver las estadísticas de consultas dinámicas.**  
  
* **Corrección de errores para habilitar la correcta desinstalación de las versiones preliminares de SSMS en equipos cliente.**  
  *Solicitudes de error de clientes vinculadas:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1868474/ssms-2016-preview-can-be-installed-but-not-uninstalled>  
  
* **Corrección de errores para permitir la edición de pasos de trabajo en el agente de trabajo SQL incluso cuando falta un archivo**.  
  *Solicitudes de error de clientes vinculadas:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
    <https://connect.microsoft.com/SQLServer/feedback/details/1502100/ssms-preview-error>  
      
* **Corrección de errores en la opción de menú "Ver datos de destino" para una sesión de Eventos extendidos en una base de datos que se ejecuta en una máquina virtual de Azure.**  
  *Solicitudes de error de clientes vinculadas*:  
  <https://connect.microsoft.com/SQLServer/feedback/details/1769778/management-studio-2016-sql-job-agent>  
***  

## <a name="ssms-october-2015-preview"></a>Versión preliminar de SSMS, octubre de 2015 
Número de versión: 13.0.700.242  
* **Nuevo instalador web ligero y modernizado que simplifica el proceso de instalación y descarga de SSMS.**  
  
* **Nuevo asistente para el cifrado de columnas Always Encrypted que permite el cifrado en el cliente y el descifrado de las columnas seleccionadas.**  
  
* **Nuevo cuadro de diálogo de rotación de claves maestras de columna (CMK) para bases de datos Always Encrypted que simplifica el proceso de rotación de claves de cifrado con el fin de proteger los datos.**  
  
* **Nuevo monitor de Stretch Database que permite solucionar problemas y supervisar el estado de la migración de los datos a la nube de Azure.**  
  
* **Mejoras en el asistente para Stretch Database para admitir la elección de un servidor de Microsoft Azure que no esté en la suscripción predeterminada de Microsoft Azure.**  
  *Solicitudes de error de clientes vinculadas:*  
  <https://connect.microsoft.com/SQLServer/feedback/details/1687063/cannot-choose-from-multiple-microsoft-azure-subscriptions>  
* **Corrección de errores para permitir la visualización adecuada del plan de ejecución activo en SSMS.**  
  *Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1774446/viewing-live-execution-plan-from-activity-monitor-crashes-ssms>    
* **Corrección de errores para quitar opciones no válidas de scripting de SSMS de las instantáneas de la base de datos**  
  *Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1515168/ssms-scripting-of-database-snapshots-includes-invalid-options>  
* **Corrección de errores en la interfaz de usuario del almacén de datos de consulta para mostrar detalles en el panel "Consultas que más recursos consumen".**  
  *Solicitudes de error de clientes vinculadas:*  
<https://connect.microsoft.com/SQLServer/feedback/details/1737185/sql-server-2016-overall-resource-consumption-query-store-pane-issue>  
***  

## <a name="ssms-september-2015-preview"></a>Versión preliminar de SSMS, septiembre de 2015 
Número de versión: 13.0.600.65  
* **Nuevo cuadro de diálogo para la regla de firewall que agiliza el proceso de conexión a una base de datos de SQL Azure.**      
    
* **Se ha actualizado el cuadro de diálogo "Nuevo índice" que permite la creación de los índices de almacén de filas no agrupados cuando hay un índice de almacén de columnas agrupado presente. Esta funcionalidad está disponible para SQL 2016 y versiones superiores.**      
  *Solicitudes de error de clientes vinculadas:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1552617/creation-of-nc-index-when-clustered-columnstore-index>  
      
* **Corrección de errores para poder ver y editar los pasos del trabajo del Agente SQL en las versiones preliminares de SSMS que se ejecutan en Windows 7.**      
  *Solicitudes de error de clientes vinculadas:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1548140/cannot-view-or-edit-any-sql-agent-job-step>,    
  <https://connect.microsoft.com/SQLServer/feedback/details/1626895/unable-to-load-dll-dts>,    
  <https://connect.microsoft.com/SQLServer/feedback/details/1576662/error-creating-new-job-step>     
      
* **Corrección de errores para mostrar los nodos de desencadenador en SSMS para SQL Server 2014 y versiones posteriores.**      
  *Solicitudes de error de clientes vinculadas:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1617533/trigger-node-missing>   
      
* **Correcciones de errores en la interfaz de usuario para informes estándar del servidor y la base de datos para excluir la información de la versión del encabezado.**      
  *Solicitudes de error de clientes vinculadas:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1387471/report-headings-wrongly-named>  
      
* **Corrección de errores para evitar que se muestre un nodo de estadísticas de consultas activas como completado si está incompleto.**      
  *Solicitudes de error de clientes vinculadas:*    
  <https://connect.microsoft.com/SQLServer/feedback/details/1589096/live-query-statistics-node-shows-as-completed>  
  
***      
## <a name="ssms-august-2015-preview"></a>Versión preliminar de SSMS, agosto de 2015 
Número de versión: 13.0.500.53
  
* **Actualizaciones del explorador de objetos para reducir el retraso de la carga cuando hay un gran número de bases de datos.**  
  
* **Mejoras para la instalación de SSMS en equipos con Windows 10.**  
  
* **Correcciones de errores y actualizaciones para el administrador de configuración de SQL Server y la interfaz de usuario de informes de usuario de SSMS**    
***  
  
## <a name="ssms-july-2015-preview"></a>Versión preliminar de SSMS, julio de 2015
Número de versión: 13.0.400.91
  
* **Diagramas de base de datos para la Base de datos SQL de Azure (V12).**  
  
* **Se ha mejorado la compatibilidad de IntelliSense con la nueva sintaxis de tabla temporal.**  
  
* **Se ha actualizado la biblioteca de DacFx para admitir las características más recientes de las bases de datos SQL de Azure, como la seguridad de nivel de fila y la autenticación de Azure Active Directory.**  
  
* **Correcciones de errores (se ha actualizado la interfaz de usuario para "buscar actualizaciones", se ha corregido la interfaz de usuario en la lista "nivel de compatibilidad", etc.).**  
***  
  
## <a name="ssms-june-2015-preview"></a>Versión preliminar de SSMS, junio de 2015 
Número de versión: 13.0.300.44
  
* **Nuevo instalador web ligero de SSMS.**  
  
* **Búsqueda automática de actualizaciones.**  
  
* **SSMS es ahora compatible con la búsqueda de texto completo de la Base de datos SQL de Azure (V12).**  
  
* **Principales solicitudes de cliente tratadas:**  
  * Se ha habilitado "Editar las primeras 200 filas" para las tablas y vistas del Explorador de objetos.  
  * Se ha habilitado el diseñador de tablas de la Base de datos SQL de Azure (V12).  
  * Se han habilitado cuadros de diálogos de propiedades de la base de datos y de las tablas para la Base de datos SQL de Azure (V12).  
    
 * **Nueva opción para omitir la pregunta de si desea guardar los archivos de T-SQL.**  
   
 * **Compatibilidad del asistente para importación y exportación con los nuevos niveles de servicio de Base de datos SQL de Azure (Basic, Standard, Premium).**  
   
 * **Numerosas correcciones de errores (escenarios de scripting, habilitación del seguimiento de cambios para bases de datos SQL, etc.).**   

