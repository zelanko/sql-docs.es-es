---
title: Registro de cambios para SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssdt
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b071f8b8-c8e5-44e0-bbb6-04804dd1863a
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 5bd0e1d3955d898824d285d28979089e2de6f322
ms.openlocfilehash: 243d2e6187a58554cee80066912de7dfcc0c52fc
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="changelog-for-sql-server-data-tools-ssdt"></a>Registro de cambios para SQL Server Data Tools (SSDT)
Este registro de cambios es para [SQL Server Data Tools (SSDT) para Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx).  
  
Para artículos detallados sobre las novedades y los cambios, visite [el blog del equipo de SSDT](https://blogs.msdn.microsoft.com/ssdt/)

## <a name="ssdt-171"></a>SSDT 17.1
Número de compilación: 14.0.61705.170

### <a name="whats-new"></a>¿' S New?
**Proyectos de AS:**
- Los usuarios pueden establecer codificación sugerencias en columnas de la interfaz de usuario en los modelos de 1400
- IntelliSense relacionado con el modelo no estará disponible en modo sin conexión
- Explorador de modelos tabulares ahora contiene un nodo para representar expresiones de M con nombre disponibles en el modelo (modelos tabulares de nivel de compatibilidad de 1400)
- Azure Active Directory selector de personas similar a IAM del Portal de Microsoft Azure ya está disponible al configurar los miembros del rol en los modelos tabulares

**Proyectos de base de datos:**
- Actualiza a DacFx 17.1

### <a name="bug-fixes"></a>Correcciones de errores
- Se corrigió un problema donde se muestra incorrectamente el nombre del grupo de diseñadores de Business Intelligence en las opciones de Visual Studio en VS2017
- Se corrigió un problema que puede producirse un bloqueo de generar un mapa de código para una solución con un proyecto de informe o como proyecto
- Se ha corregido una serie de problemas con la integración de PowerQuery para modelos tabulares de nivel de compatibilidad de Analysis Services 1400
- Ventana de herramientas, donde el operador de asignación no podría encontrarse en una línea independiente al definir una medida se corrigió un problema en el nuevo editor de DAX
- Se corrigió un problema que impide que la presentación tabular medida actualizar al cambiar el nombre de las medidas de perspectiva
- Implementar actualizada motor del área de trabajo integrado de Analysis Services y modelo de objetos tabulares que corrige una regresión que provocó que contiene traducciones produce un error en los proyectos tabulares 1200 en servidor SQL Server 2016 Analysis Services
- Corregido un problema de rendimiento que realiza creation\deletion de nuevos orígenes de datos tabulares de 1400 muy lento
- Se corrigió un problema en el diagrama de la DSV en modelos multidimensionales podría detener representación si cambiar la vista rápidamente entre diferentes DSV

## <a name="dacfx-171"></a>DacFx 17.1
- Se ha corregido un problema al cifrar una columna con tablas optimizadas en memoria con otras columnas de identidad
- Compatibilidad con SQLDOM opción CATALOG_COLLATION para crear la base de datos

## <a name="dacfx-1701"></a>DacFx 17.0.1 
- Corrección para el problema con las bases de datos con una clave asimétrica HSM con un proveedor EKM [elemento Connect](https://connect.microsoft.com/SQLServer/feedback/details/3132749/sqlpackage-exe-fails-when-extracting-a-database-which-contains-an-asymmetric-key-using-an-ekm-provider)

## <a name="ssdt-170-supports-up-to-sql-server-2017"></a>SSDT 17,0 (admite hasta 2017 de SQL Server)
Número de compilación: 14.0.61704.140

### <a name="whats-new"></a>¿' S New?
**Proyectos de base de datos:**
- La modificación de un índice agrupado en una vista ya no se bloqueará la instalación
- Las cadenas de comparación de esquemas relacionadas con el cifrado de columnas usarán el nombre correcto en lugar del nombre de instancia.   
- Se agregó una nueva opción de la línea de comandos en SqlPackage: ModelFilePath.  Esto proporciona una opción para usuarios avanzados especificar un archivo externo model.xml para importar, publicar y las operaciones de scripting   
- La API de DacFx se ha ampliado para admitir la autenticación de Azure AD Universal y la autenticación multifactor (MFA)

**Proyectos de IS:**
- El origen OData de SSIS y el administrador de conexiones OData ahora admiten la conexión a fuentes de OData de Microsoft Dynamics AX Online y Microsoft Dynamics CRM Online.
- Proyecto de SSIS ahora es compatible con la versión de servidor de destino de "SQL Server 2017" 
- Compatibilidad con CDC Control Task, divisor CDC y origen de CDC cuando el destino es SQL Server 2017. 

**Proyectos de AS:**
- La integración de Analysis Services PowerQuery (modelos tabulares de nivel de compatibilidad de 1400):
    - DirectQuery está disponible para SQL de Oracle, Teradata y si el usuario ha instalado a controladores de fabricantes 3rd
    - Agregar columnas con un ejemplo en PowerQuery
    - Opciones de modelos de 1400 (propiedades de nivel de modelo utilizados por el motor de M) de acceso a datos
        - Habilitar combinación rápida (valor predeterminado es false; cuando se establece en true, el mashup motor omitirá niveles de privacidad del origen de datos al combinar datos)
        - Habilitar heredado redirige (valor predeterminado es false: cuando se establece en true, el motor de mashup seguirá redirecciones de HTTP que son potencialmente inseguras.  Por ejemplo, una redirección de HTTPS a un URI de HTTP)  
        - Devolver valores de Error como Null (valor predeterminado es false: cuando se establece en true, errores de nivel de celda se devolverán como null. Cuando sea false, se producirá una excepción es una celda contiene un error)  
    - Orígenes de datos adicionales (orígenes de datos de archivo) mediante PowerQuery
        - Excel 
        - Texto o CSV 
        - Xml 
        - JSON 
        - Carpeta 
        - Base de datos de Access 
        - Almacenamiento de blobs de Azure 
    - Interfaz de usuario localizada PowerQuery
- Ventana de herramientas del Editor de DAX
    - Editor asociado para expresiones de filas de detalles, disponibles a través de la vista, los menús de otras ventanas en SSDT, las columnas calculadas y medidas DAX mejorado
    - Mejoras en DAX parser\Intellisense


**Proyectos de RS:**
- El control RVC insertable ahora está disponible y es compatible con SSRS 2016.

### <a name="bug-fixes"></a>Correcciones de errores
**Proyectos de AS:**
- Se corrigió la prioridad de la plantilla de proyectos de BI para que no aparezcan en la parte superior de las categorías de proyectos nuevos en VS
- Se corrigió un bloqueo de VS que se puede producir en circunstancias excepcionales cuando se abre la solución de SSIS, SSAS o SSRS
- Tabular: diversas mejoras y correcciones de rendimiento para el análisis DAX y la barra de fórmulas.
- Tabular: el Explorador de modelos tabulares ya no será visible si no hay abierto ningún proyecto tabular de SSAS.
- Multidimensional: se ha corregido un problema que hacía que el cuadro de diálogo de procesamiento no se pudiese usar en máquinas con valores altos de PPP.
- Tabular: se ha corregido un problema que producía un error en SSDT al abrir cualquier proyecto de BI cuando SSMS ya estaba abierto. [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3100900/ssdt-faults-when-opening-any-bi-project-when-ssms-is-already-open)
- Tabular: se ha corregido un problema que hacía que las jerarquías no se guardasen correctamente en el archivo .bim en un modelo 1103. [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3105222/vs-2015-ssdt)
- Tabular: se ha corregido un problema que permitía el modo de área de trabajo integrada en máquinas de 32 bits aunque no fuese compatible.
- Tabular: se ha corregido un problema que podía causar bloqueos al hacer clic en cualquier elemento en el modo de selección parcial (por ejemplo, escribir una expresión DAX pero hacer clic en una medida).
- Tabular: se ha corregido un problema que hacía que el Asistente para implementación volviese a establecer la propiedad .Name del modelo en "Model". [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3107018/ssas-deployment-wizard-resets-modelname-to-model)
- Tabular: se ha corregido un problema que hacía que al seleccionar una jerarquía en TME se mostrasen las propiedades incluso si no estaba seleccionada la vista de diagrama.
- Tabular: se ha corregido un problema que hacía que al pegar desde determinadas aplicaciones en la barra de fórmulas DAX se pegasen imágenes u otro contenido en lugar de texto.
- Tabular: se ha corregido un problema que hacía que no se pudiesen abrir algunos modelos antiguos en la versión 1103 debido a la presencia de medidas con una definición específica.
- Tabular: se ha corregido un problema que hacía que las sesiones de XEvent no se pudiesen eliminar.
- Se corrigió un problema en que podría producirse un problema al intentar compilar archivos "smproj" de AS con devenv.com
- Se corrigió un problema que finalizaba con demasiada frecuencia los cambios de texto al usar Coreano IME en los títulos de las pestañas de hojas del modelo tabular de AS
- Se corrigió un problema en que IntelliSense para la función DAX Related() no funcionaba correctamente para mostrar las columnas de otras tablas
- Se mejoró la importación del proyecto tabular de AS desde el cuadro de diálogo de la base de datos al ordenar la lista de las bases de datos de AS
- Se corrigió un problema en la creación de tablas calculadas en el modelo tabular de AS en que las tablas no aparecían como objetos sugeridos en la expresión
- Se corrigió un problema al intentar abrir los modelos de AS 1400 de versión preliminar mediante el servidor de área de trabajo integrada después de ver el código
- Se corrigió un problema que impedía que algunos orígenes de datos (sin compatibilidad con el catálogo inicial) funcionaran correctamente en circunstancias determinadas 
- El Asistente para la implementación debe aplicar cambios a las particiones de tablas calculadas incluso cuando está habilitada la opción de mantener particiones
- Se corrigió un problema en que el cuadro de diálogo de propiedades avanzadas para la conexión de AS no mostraba la lista completa hasta que se volvía a seleccionar
- Se ha corregido una serie de problemas con recortado cadenas de interfaz de usuario que ha aparecido en algunas versiones localizadas
- Se ha corregido una serie de problemas con la integración de PowerQuery en el nivel de compatibilidad de 1400 como modelos tabulares
- Se ha corregido un problema con plantillas de estilo de Asistente para informes no aparecen correctamente
- Se ha corregido un problema con el Asistente para informes que podrían dar lugar a la configuración de origen de datos incorrectos cuando se cambia de SQL a AS
- Se corrigió un problema que produce el error de compilación del proyecto de Analysis Services (Tabular) desde la línea de comandos (devenv.com\exe)
- Se ha corregido un problema con el analizador de medida DAX para mostrar el color del texto resaltado y correcta cuando empiezan con las letras antes: =
- Se corrigió un problema desencadenar una ObjectRefException si las rutas de acceso tiene demasiados intenta mostrar todos los archivos de proyecto Tabular en el modo integrado de área de trabajo
- Se corrigió un problema con el Diseñador de origen de datos de proveedor de datos de Compact 4.0 cliente donde aparecía disponible
- Se corrigió un problema que produjo un error al intentar examinar como modelo de minería de datos en VS2017
- Se corrigió un problema en que el modelo multidimensional en VS2017 donde diagrama DSV detiene el procesamiento después de cambiar de vista y, a continuación, visita una excepción
- Se corrigió un problema vistas previas de informes con una conexión de AS que no se pudo VS2017
 

**Proyectos de RS:**
- Se corrigió un problema en el diseño de informes en SSDT en que la vista de árbol de los parámetros, los orígenes de datos y los conjuntos de datos se podría contraer cuando se hacen la mayoría de los datos 
- Se ha corregido un problema que hacía que la opción Guardar guardase la versión de RDL, no la versión más reciente.
- Se ha corregido un problema que hacía que RS de SSDT hiciese una copia de seguridad de los archivos cuando la copia de seguridad estaba desactivada y causase otros problemas.
- Se ha corregido un problema en el Generador de informes que hacía que se mostrase un error al hacer clic en "Dividir celdas". [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3101818/ssdt-2015-ssrs-designer-error-by-matrix-cell-split)
- Se ha corregido un problema que podía hacer que el almacenamiento en caché generase datos incorrectos en un informe. [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/3102158/ssdtbi-14-0-60812-report-preview-data-is-frequently-wrong-due-to-bad-caching)

**Proyectos de IS:**
- Se ha corregido un problema que hacía que la configuración de run64bitruntime no se conservase.
- Se ha corregido un problema que hacía que DataViewer no guardase las columnas mostradas.
- Se ha corregido un problema que hacía que los elementos del paquete ocultasen las anotaciones. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3106624/package-parts-hide-annotations)
- Se ha corregido un problema que hacía que los elementos del paquete descartasen las anotaciones y los diseños del flujo de datos. [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3109241/package-parts-discard-data-flow-layouts-and-annotations)
- Se ha corregido un problema que hacía que SSDT se bloquease al importar un proyecto de SQL Server.
- Corregido un problema no tiene valor predeterminado de TimeoutInMinutes de tarea de sistema de archivos de Hadoop a 10 después de guardar el paquete SSIS de apertura y en tiempo de ejecución.

**Proyectos de base de datos:**
- Configuración de incorporación e implementación de SSDT DACPAC para IgnoreColumnOrder [Artículo de Connect](https://connect.microsoft.com/SQLServer/feedback/details/1221587/ssdt-dacpac-deploy-add-setting-back-in-for-ignorecolumnorder)
- SSDT no se puede compilar si se usa STRING_SPLIT [Artículo de Connect](http://connect.microsoft.com/SQLServer/feedback/details/2906200/ssdt-failing-to-compile-if-string-split-is-used)
- Se corrige problema en que la propiedad DeploymentContributors tiene acceso al modelo público pero no se ha inicializado el esquema de respaldo [Problema de Github](https://github.com/Microsoft/DACExtensions/issues/8)
- Corrección temporal de DacFx para la ubicación de FILEGROUP
- Corrección del error "Referencia sin resolver" para sinónimos externos. 
- Always Encrypted: el cifrado en línea no deshabilita el seguimiento de cambios en la cancelación ni tampoco funciona correctamente si el seguimiento de cambios no se limpió antes de comenzar el cifrado


## <a name="ssdt-165-supports-up-to-sql-server-2016"></a>SSDT 16.5 (admite hasta SQL Server 2016)
Publicación: 20 de octubre de 2016

Número de compilación: 14.0.61021.0

**Novedades**


### <a name="connection-improvements"></a>Mejoras de conexión

* El nuevo cuadro de búsqueda de la pestaña **Examinar** le ayuda a filtrar los servidores locales, los servidores de red y las bases de datos SQL de Azure. Esto resulta útil si le aparecen un gran número de servidores o bases de datos en estas listas.
* La pestaña **Historial** tiene opciones de menú contextual para anclar y desanclar favoritos, y una nueva opción para quitar las conexiones de historial.

### <a name="sqlpackage-and-dacfx-api-improvements"></a>Mejoras de las API de SqlPackage y DacFx

Con las API de SqlPackage.exe y DacFx ahora puede generar un informe de implementación y un script de implementación, y publicar en una base de datos; todo en una sola acción. Esto supone un ahorro de tiempo para cualquier persona a que le gusta tener un informe de lo que se ha publicado durante una implementación. Otra ventaja es que se crean scripts independientes para la base de datos maestra y la base de datos de destino de la implementación en escenarios de Azure. Hasta ahora se creaba un único script que no resultaba útil para implementaciones repetidas.

Para las acciones Publish y Script de SqlPackage, se han agregado dos nuevos argumentos.

* DeployScriptPath (nombre corto: dsp). Se trata de una ruta opcional en la que escribir el script de implementación. Para la implementación de Azure, si hubiera comandos TSQL para crear o modificar la base de datos, se escribirá un script maestro en la misma ruta, pero con “Filename_Master.sql” como el nombre del archivo de salida.
* DeployReportPath (nombre corto: drp). Se trata de una ruta opcional en la que escribir el informe de implementación.

Tenga en cuenta que, para la acción Script, se deben usar los argumentos de la ruta de salida existentes o los nuevos argumentos específicos del script o informe, pero no ambos.

Ejemplo de uso:

**Acción Publish**

```Sqlpackage.exe /a:Publish /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

**Acción Script**

```Sqlpackage.exe /a:Script /tsn:(localdb)\ProjectsV13 /tdn:MyDatabase /deployscriptpath:”My\DeployScript.sql” /deployreportpath:”My\DeployReport.xml”```

En DacFx, se han agregado dos nuevas API: DacServices.Publish() y DacServices.Script(). Estas también permiten realizar acciones de publicación, scripts e informes en una única operación. Ejemplo de uso:

```
DacServices service = new DacServices(connectionString);
using(DacPackage package = DacPackage.Load(@"C:\My\db.dacpac")) {
var options = new PublishOptions() {
    GenerateDeploymentScript = true, // Should a deployment script be created?
    GenerateDeploymentReport = true, // Should an xml deploy report be created?
    DatabaseScriptPath = @"C:\My\OutputScript.sql", // optional path to save script to
    MasterDbScriptPath = @"C:\My\OutputScript_Master.sql", // optional path to save master script to
    DeployOptions = new DacDeployOptions()
};

// Call publish and receive deployment script & report in the results
PublishResult result = service.Publish(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);

// Call script and receive deployment script & report in results
result = service.Script(package, "TargetDb", options);
Console.WriteLine(result.DatabaseScript);
Console.WriteLine(result.MasterDbScript);
Console.WriteLine(result.DeploymentReport);
```

**Analysis Services y Reporting Services**

Se ha mejorado el rendimiento del analizador de DAX de diseñador de modelos tabulares de SSAS cuando se trabaja con expresiones de DAX de gran tamaño.
Para obtener más información, lea la [entrada de blog de Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/).

### <a name="fixed--improved-this-month"></a>Correcciones y mejoras de este mes

**Herramientas para bases de datos**

* [Error de Connect 3055711](https://connect.microsoft.com/SQLServer/feedback/details/3055711/columns-cannot-be-selected-from-cross-apply-openjson-with-explicit-schema): no se pueden seleccionar columnas desde CROSS APPLY OPENJSON con un esquema explícito.
* Corregido: problema con los índices de tablas de historial generados automáticamente, por el que DacFx eliminaba el índice al volver a implementar.
* Corregido: problema con el analizador por lotes de DAX, que no analizaba los caracteres de corchete con escape "]", lo que daba lugar a un error en la publicación.
* Mejorado: SqlPackage ahora incluye descripciones para cada acción en los resultados de la ayuda.
* Corregido: la opción “Recordar contraseña” del cuadro de diálogo de conexión no se conservaba cuando se editaban las opciones avanzadas y al modificar una cadena de conexión guardada en Publicar, Comparación de esquemas y otros archivos.
* Corregido: para las conexiones mostradas en la pestaña Historial con IntegratedAuthentication=true, el campo Autenticación de las propiedades de conexión se quedaba en blanco. Ahora muestra “Autenticación de Windows”, como estaba previsto.
* Corregido: no se conservaban los cambios realizados en la configuración de Intellisense de SQL Server Tools en Herramientas -> Opciones -> Editor de texto.
* Mejorado: el botón Anclar/Desanclar del cuadro de diálogo de conexión de la pestaña Historial es ahora más compacto, lo que reduce la probabilidad de que aparezca una barra de desplazamiento.
* Corregido: se han corregido varios problemas de accesibilidad en el cuadro de diálogo de conexión.

**Analysis Services y Reporting Services**

* Se ha corregido un problema en el diseñador de modelos tabulares de SSDT AS por el que al hacer clic en el control de la barra de desplazamiento en una cuadrícula de datos se producía un bloqueo en determinadas situaciones.
* Se ha corregido un problema por el que no estaba disponible la opción para suplantar la conexión como el usuario actual en el modelo tabular de SSDT AS.
* Se ha corregido un problema en el diseñador de modelos tabulares de SSDT AS por el que expandir la barra de fórmulas demasiado lejos podía hacer que no se pudiera volver a abrir el proyecto.
* Se ha corregido un bloqueo en el diseñador de modelos tabulares de SSDT AS que se producía al presionar una tecla si estaba seleccionada la pestaña de tabla.
* Se ha corregido un problema en los proyectos de SSDT AS por el que Analizar en Excel no se conectaba a versiones de servidores de AS de nivel inferior.

**Servicio de integración**

* Se ha corregido el error de Connect [1608896](https://connect.microsoft.com/SQLServer/feedback/details/1608896/move-multiple-integration-service-package-tasks): mover varias tareas de un paquete del servicio de integración.





## <a name="ssdt-164-for-sql-server-2016"></a>SSDT 16.4 (para SQL Server 2016)
Publicación: 20 de septiembre de 2016

Número de compilación: 14.0.60918

**Novedades**

Comparación de esquemas es ahora compatible con SqlPackage.exe y la API de Data-Tier Application Framework (DacFx). Para obtener más información, consulte [Schema Compare in SqlPackage and the Data-Tier Application Framework](https://blogs.msdn.microsoft.com/ssdt/2016/09/20/schema-compare-in-sqlpackage-and-the-data-tier-application-framework-dacfx/) (Comparación de esquemas en SqlPackage y Data-Tier Application Framework).

**Analysis Services: modo de área de trabajo integrada de SSDT Tabular (SSAS)**

SSDT Tabular ahora incluye una instancia de SSAS interna que SSDT Tabular inicia automáticamente en segundo plano si se habilita el modo de área de trabajo integrada para que pueda agregar y ver tablas, columnas y datos en el Diseñador de modelos sin tener que proporcionar una instancia del servidor de área de trabajo externa. El modo de área de trabajo integrada no cambia el funcionamiento de SSDT Tabular con un servidor y una base de datos de área de trabajo. Lo que cambia es la ubicación en la que SSDT Tabular hospeda la base de datos del área de trabajo. Para habilitar el modo de área de trabajo integrada, seleccione la opción Área de trabajo integrada en el cuadro de diálogo del Diseñador de modelos tabulares que aparece al crear un nuevo proyecto tabular. Para los proyectos tabulares existentes que usan actualmente un servidor de área de trabajo explícito, puede cambiar al modo de área de trabajo integrada estableciendo el parámetro Modo de Área de trabajo integrada en verdadero en la ventana Propiedades, que se muestra cuando selecciona el archivo Model.bim en el Explorador de soluciones. Para obtener más información, consulte la [entrada de blog de Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2016/09/20/introducing-integrated-workspace-mode-for-sql-server-data-tools-for-analysis-services-tabular-projects-ssdt-tabular/).

**Actualizaciones y correcciones de**
**herramientas para bases de datos:**

- [Problema de Connect 3087775](https://connect.microsoft.com/SQLServer/feedback/details/3087775): tablas temporales interrumpidas en la actualización de julio de VS Data Tools 14.0.60629.0, "El valor no puede ser nulo. Nombre de parámetro: reportedElement".
- [Problema de Connect 1026648](https://connect.microsoft.com/SQLServer/feedback/details/1026648): IsPersistedNullable se muestra como diferente en la comparación de SSDT.
- [Problema de Connect 2054735](https://connect.microsoft.com/SQLServer/feedback/details/2054735): la identidad se restablece al importar un BACPAC.
- [Problema de Connect 2900167](https://connect.microsoft.com/SQLServer/feedback/details/2900167): la ejecución de pruebas unitarias de SSDT deja archivos temporales.
- [Problema de Connect 1807712](https://connect.microsoft.com/SQLServer/feedback/details/1807712): interrupción de la compatibilidad con versiones anteriores: AppLocal e instalación de NuGet

**Analysis Services y Reporting Services**

* Se ha corregido un problema en SSDT por el que aparecían elementos emergentes de sugerencias de errores al editar DAX para columnas calculadas de DirectQuery.
* Se ha corregido un problema en la cuadrícula tabular de SSDT AS por el que el icono de KPI no se mostraba en la cuadrícula de medidas cuando el factor de escala de Windows se establecía en valores altos de PPP de 200 % o más.
* Se ha corregido un problema en SSDT AS por el que, al pegar un gran número de datos de tabla, el proyecto tabular no respondía.
* Se ha corregido un problema en el editor de modelos tabulares de SSDT AS para marcar que el modelo necesita guardar cambios al modificar el nombre descriptivo de la conexión.
* Se ha corregido un problema en los proyectos tabulares de SSDT AS por el que no se podía cambiar el tamaño del ancho de las columnas en el cuadro de diálogo Administrar relaciones.
* Se ha corregido un problema en los modelos de nivel 1200 tabulares de SSDT AS por el que al copiar datos de Excel con una configuración regional, por ejemplo, alemán, no se trataba la coma como el separador decimal correctamente.
* Se ha corregido un problema en los proyectos de SSDT AS con algunos conjuntos de iconos de KPI que podían producir un error "No se pueden recuperar los datos para este objeto visual".
* Se ha corregido un problema con el cuadro de diálogo de las propiedades del proyecto de SSDT AS para que se delimite correctamente cuando se cambie su tamaño en el ajuste con valores altos de PPP.
* Se ha corregido un problema en los proyectos SSDT AS que podría haber provocado un error al actualizar determinados modelos con las tablas pegadas.
* Se ha corregido un problema en SSDT AS por el que la acción de pegar filas de hojas completas desde Excel resultaba muy lenta y creaba muchas columnas no deseadas.
* Se ha corregido un problema en SSDT AS por el que analizar y resaltar grandes expresiones de DataTable resultaba muy lento o producía un bloqueo.
* Se ha corregido un problema en SSDT AS para agregar valores de KPI y medidas a la perspectiva actual seleccionada en el editor.
* Se ha corregido un problema en SSDT por el que la importación de datos en el proyecto de AS desde SQL Azure no admitía tipos de esquemas distintos a "dbo".



## <a name="ssdt-163-for-sql-server-2016"></a>SSDT 16.3 (para SQL Server 2016)
Publicación: 15 de agosto de 2016

Número de compilación: 14.0.60812.0  

**Novedades**

- **Numeración y control de versiones de lanzamientos:** las versiones ahora se etiquetan numéricamente en lugar de por mes. Esto es coherente con la nueva directiva SSMS y simplifica los casos en los que existen numerosas versiones o revisiones en un mes. Esta versión es 16.3, lo que significa que es la tercera actualización tras el lanzamiento de RTM. Las revisiones se identificarían como 16.3.1 y así sucesivamente. Nuestra próxima actualización será la 16.4 (prevista para el próximo mes).
- **Analysis Services: Explorador de modelos tabulares:** el Explorador de modelos tabulares le permite navegar fácilmente a través de los distintos objetos de metadatos en un modelo, como orígenes de datos, tablas, medidas y relaciones. Se implementa como una ventana de herramientas independiente que puede mostrar abriendo el menú Ver en Visual Studio, apuntando a Otras ventanas y haciendo clic luego en Explorador de modelos tabulares. El Explorador de modelos tabulares aparece de forma predeterminada en el área del Explorador de soluciones, en una pestaña independiente. El Explorador de modelos tabulares organiza los objetos de metadatos en una estructura de árbol muy similar al esquema de un modelo tabular 1200 y con muchas más características nuevas.
- **Herramientas para bases de datos: Always Encrypted:** esta versión proporciona nuevos cuadros de diálogo de [administración de claves de Always Encrypted](https://msdn.microsoft.com/library/mt708953.aspx) para agregar fácilmente claves maestras de columna o claves de cifrado de columna al proyecto de base de datos o una base de datos activa en el Explorador de objetos de SQL Server. Esta versión admite certificados en el almacén de certificados de Windows. En las próximas versiones, se admitirán Azure Key Vault y proveedores CNG.
    - Al crear la clave maestra de columna o la clave de cifrado de columna, es posible que experimente que los cambios no se reflejan en el Explorador de objetos de SQL Server inmediatamente después de hacer clic en Actualizar base de datos. Para solucionar este problema, actualice el nodo de base de datos en el Explorador de objetos de SQL Server.
    - Si intenta cifrar una columna en una tabla con datos del Explorador de objetos de SQL Server, puede experimentar un error. Actualmente, esta característica se admite únicamente en proyectos de base de datos de SSDT y SSMS. La compatibilidad con el Explorador de objetos de SQL Server se habilitará en una versión posterior.


**Actualizaciones y correcciones**
* **Herramientas para bases de datos:**
    - **SSDT:**
        - Error de Connect 1898001: [se ha corregido un problema de descripción de columna con una limitación de 128 caracteres](https://connect.microsoft.com/SQLServer/feedback/details/1898001/column-description-limited-to-128-characters).
        - Se ha corregido un problema por el que, al publicar una base de datos de VS, no se aplicaba la propiedad DatabaseServiceObjective en el xml de perfil de publicación.
        - Error de Connect 2900167: [se ha corregido un problema con las pruebas unitarias que dejaban incorrectamente archivos temporales](http://connect.microsoft.com/SQLServer/feedback/details/2900167/running-ssdt-unit-tests-leaves-temp-files-behind).
        - Se ha corregido un problema por el que se truncaba el cuadro combinado Período de retención en Configuración de la base de datos.
        - Se ha corregido un problema de ausencia de verificación de contraseñas antiguas vacías en las propiedades del proyecto CLR de SQL al cambiar la contraseña.
    - **DACFx:**
        - Se ha corregido un problema por el que el nivel de compatibilidad de DACFx no se actualizaba para el error SqlAzureV12.
        - Se ha corregido un problema por el que la propiedad IsAutoGeneratedHistoryTable se excluía incorrectamente de la comparación de modelos.

- **Analysis Services y Reporting Services**
    - **SSDT:**
        - Se ha corregido un problema de que el modelo tabular no se puede guardar cuando se pierde la conexión al servidor.
        - Se ha corregido un problema por el que SSDT no responde debido a un posible problema de un bucle infinito en AS.
        - Se ha corregido un problema de expresión de DAX que provocaba comportamientos incoherentes según cómo se confirmara la expresión.
        - Se ha corregido un problema de bloqueo de VS al crear KPI.
        - Se ha corregido un problema que generaba informes no válidos para SQL Server 2008 R2, 2012 y 2014.
        - Se ha corregido un problema de orden de jerarquía que provocaba un error de bucle infinito para proyectos de .dwpro.
        - Se ha corregido un problema de RDL de RS por el que, al cambiar RDL a una versión anterior, se requería una recompilación completa, lo que causaba confusión al usuario.
        - Se ha corregido un problema de KPI por el que Ocultar en herramientas cliente no tenía efecto.
        

 
  
## <a name="ssdt-july-for-sql-server-2016"></a>SSDT de julio (para SQL Server 2016)  
Publicación: 30 de junio de 2016  
  
Número de compilación: 14.0.60629.0  
  
**Novedades**  
* **Compatibilidad con Always Encrypted:** para bases de datos que contienen columnas de Always Encrypted, esta versión agrega compatibilidad completa con Always Encrypted mediante nuestras API de núcleo y la herramienta de la línea de comandos (SqlPackage.exe). Puede crear y publicar proyectos de base de datos con compatibilidad total con todas las características de Always Encrypted.  
* **Compatibilidad mejorada con tablas temporales:** se ha simplificado la experiencia desvinculando las tablas temporales antes de las modificaciones y volviéndolas a vincular una vez que estas se hayan completado. Esto significa que las tablas temporales tienen paridad con otros tipos de tabla (estándar, en memoria) en cuanto a las operaciones que se admiten. 
* **Cambios de instalación y SqlPackage.exe:** cambios para aislar SSDT del motor de SQL Server y las actualizaciones de SSMS. Para obtener más información, consulte [Changes to SSDT and SqlPackage.exe installation and updates](https://blogs.msdn.microsoft.com/ssdt/2016/06/30/changes-to-ssdt-and-sqlpackage-exe-installation-and-updates/) (Cambios en la instalación y las actualizaciones de SqlPackage.exe y SSDT).

 

**Actualizaciones y correcciones**
* **Herramientas para bases de datos:**
    * De ahora en adelante SSDT nunca deshabilitará el cifrado de datos transparente (TDE) en una base de datos. Previamente, cuando la opción de cifrado predeterminada de la configuración de la base de datos de un proyecto estaba deshabilitada, se desactivaba el cifrado. Con esta corrección, se puede habilitar el cifrado, pero nunca deshabilitar durante la publicación. 
    * Se ha aumentado el número de reintentos y la resistencia para las conexiones de base de datos de Azure SQL durante la conexión inicial.
    * Si el grupo de archivos predeterminado no es Principal, las acciones de importar y publicar en Azure V12 producían un error. Ahora, este valor se omite cuando se publica.
    * Se ha corregido un problema por el que, al exportar una base de datos con un objeto con identificador entre comillas, la validación de la exportación podía producir un error en algunas instancias.
    * Se ha corregido un problema por el que la opción TEXTIMAGE_ON se agregaba incorrectamente para creaciones de tabla de Hekaton cuando no está permitido.
    * Se ha corregido un problema por el que la opción Exportar tardaba mucho tiempo en exportar un gran número de datos debido a una escritura en el archivo model.xml después de que se completara la fase de datos, lo que provocaba la reescritura de los contenidos del archivo .bacpac.
    * Se ha corregido un problema por el que los usuarios no aparecían en la carpeta Seguridad de las conexiones APS y DW de Azure SQL.


 * **Analysis Services y Reporting Services:**
    * Se ha corregido un problema de SxS con un proveedor de MSOLAP OLEDB por el que se estaba instalando el proveedor de 32 bits, lo que afectaba a la conexión de Excel 2016 de 64 bits a SQL Server 2014 (no se reproducía con instalaciones de ClickOnce de Office365, solo con instalaciones de Excel de MSI).
    * Se ha corregido un problema para que un caso extremo sea más sólido al actualizar el modelo de AS con tablas pegadas desde 1103 hasta el modelo de compatibilidad 1200, que podía producir el error "Relationship uses an invalid column ID" (La relación usa un id. de columna no válido).
    * Se ha corregido un problema de SxS por el que SSDT-BI 2013 en la misma máquina no podía importar datos en un modelo de AS después de desinstalar SSDT 2015 (los cartuchos compartían la configuración del registro).
    * Se ha mejorado la potencia para abordar problemas o bloqueos cuando se pierde la conexión al motor de AS (es decir, SSDT se quedó abierto durante la noche y el servidor de AS se recicló, u otros casos en los que se pierde la conexión temporalmente). 
    * Se han corregido problemas con diálogos que se abrían en pantallas distintas a la de VS en los escenarios con varios monitores. 
    * Se ha corregido y habilitado la compatibilidad para pegar desde tablas HTML (datos de cuadrícula) en tablas pegadas del modelo de AS. 
    * Se ha corregido un problema por el que la actualización no actualizaba una tabla pegada vacía a 1200 (usada solo como tabla de contenedor para medidas). 
    * Se ha corregido un problema al actualizar el modelo tabular de AS con tablas pegadas a 1200 para solucionar un problema del motor de AS con CalcTables (que se usan para tablas pegadas en 1200), para realizar un proceso completo en las nuevas tablas de cálculo tras la actualización. 
    * Se ha corregido un problema por el que podría bloquearse la cancelación de la creación de una nueva tabla calculada del modelo 1200 con una expresión DAX incompleta. 
    * Se ha corregido un problema al importar el modelo 1200 del servidor de AS al proyecto de SSDT AS cuando el nombre de la base de datos y el de la tabla eran el mismo. 
    * Se ha corregido un problema con la edición de medidas de KPI en el modelo tabular 1103. 
    * Se ha corregido una excepción de referencia de objeto no establecida que se producía al pegar una medida de KPI en la cuadrícula para un modelo 1200 de AS. 
    * Se ha corregido un problema por el que no se podía eliminar una columna de una tabla calculada de la vista de diagrama en los modelos 1200. 
    * Se ha corregido una excepción de referencia de objeto no establecida que se producía al ver las propiedades del archivo de proyecto model.bim en la vista de código. 
    * Se ha corregido un problema por el que, al pegar datos en una cuadrícula de modelo de AS para crear una tabla pegada, se producían valores incorrectos en configuraciones regionales internacionales que usan la coma como separador decimal. 
    * Se ha corregido un problema que se producía al abrir un proyecto de 2008 RS en SSDT y elegir no actualizarlo. 
    * Se ha corregido un problema en la interfaz de usuario de la tabla calculada de los modelos del nivel de compatibilidad 1200 al usar el formato predeterminado del tipo de columna para permitir cambiar el tipo de formato desde la interfaz de usuario. 
    

## <a name="ssdt-june-for-sql-server-2016"></a>SSDT de junio (para SQL Server 2016)  
Publicación: 1 de junio de 2016  
  
Número de compilación: 14.0.60525.0 

Ya se ha publicado Disponibilidad general (GA) de SSDT. La actualización de SSDT GA para junio de 2016 agrega compatibilidad con las últimas actualizaciones de SQL Server 2016 RTM y varias correcciones de errores. Para obtener más información, consulte [SQL Server Data Tools GA update for June 2016](https://blogs.msdn.microsoft.com/ssdt/2016/06/01/sql-server-data-tools-ga-update-for-june-2016/) (Actualización de SQL Server Data Tools GA para junio de 2016).

      

## <a name="ssdt-april-for-sql-server-2016-rc3"></a>SSDT de abril (para SQL Server 2016 RC3)  
Publicación: 15 de abril de 2016  
  
Número de compilación: 14.0.60413.0  
  
**Base de datos de SQL Server**  
* **Compatibilidad con Always Encrypted:** para las bases de datos que contienen columnas de Always Encrypted, SSDT y DacFx permiten ver y editar esas bases de datos y publicar de un proyecto de base de datos en ellas. Tenga en cuenta que en una versión futura se agregará la compatibilidad con la modificación de columnas con cifrado de columna presente.  
* **Cuadro de diálogo de conexión y Explorador de objetos de SQL Server:** varias correcciones y mejoras.  
    * Se ha renovado la página Detalles en la que se indican las propiedades de conexión avanzadas para mostrar la cadena de conexión completa en un cuadro de varias líneas y para mejorar la compatibilidad en equipos con valores altos de PPP.  
    * Hemos vuelto a incluir el cuadro de diálogo de error tradicional con errores de conexión detallados. Esto ayuda a la hora de diagnosticar los problemas de inicio de sesión con mensajes de error más claros y un seguimiento de la pila, de forma que los DBA o CSS puedan obtener la información que necesitan para diagnosticar los problemas.  
    * Para los usuarios con permisos mínimos, hemos corregido diversos problemas relacionados con la creación de listas de bases de datos en el cuadro de diálogo de conexión y el Explorador de objetos de SQL Server y la consulta de la carpeta Seguridad, entre otros.  
    * Se ha mejorado el rendimiento de la base de datos de Azure SQL al expandir el nodo de las bases de datos para obtener una lista de todas las bases de datos.  
* **Instalador de SSDT:**  
    * Se ha corregido un problema por el que .Net se descargaba al desinstalar.  
    * El tamaño del instalador se ha establecido ahora correctamente en los equipos con valores altos de PPP.  
    * Se ha quitado la comprobación de versión que bloqueaba la instalación de SSDT si había una versión posterior de SQL Server presente.  
    * Comparación de esquemas: se ha corregido un problema de rendimiento por el que se tardaba mucho tiempo en activar y desactivar varios elementos en Visual Studio.  
    * Se ha agregado compatibilidad con LocalDB 2014 en equipos x86, puesto que no hay ninguna versión x86 de SQL Server 2016.  
* **Compilación e implementación:**  
    * Se ha corregido un problema por el que no se admitían columnas calculadas en tablas temporales.  
    * La opción “Ejecutar script de implementación en modo de usuario único” se omite cuando se implementa en Azure V12, ya que no se admite en escenarios de nube.  
  
  
## <a name="ssdt-hotfix-for-sql-server-2016-rc2"></a>Revisión de SSDT (para SQL Server 2016 RC2)  
Publicación: 5 de abril de 2016  
  
Número de compilación: 14.0.60329.0  
  
Esta compilación contiene una revisión para la versión de SSDT que proporciona características para SQL Server Integration Services. La compilación 14.0.60316.0 también puede usarse con Analysis Services y Reporting Services en SQL Server 2016.   
  
Para obtener esta revisión, use los [vínculos de descarga de esta entrada de blog](https://blogs.msdn.microsoft.com/ssdt/2016/04/05/ssdt-preview-update-rc2/).  
  
Si los desarrolladores de informes crean nuevos informes usando esta compilación de SSDT, [tienen que leer el problema conocido y la solución](https://blogs.msdn.microsoft.com/ssdt/2016/04/05/ssdt-preview-update-rc2/) sobre un problema temporal en los informes de SSRS que solo se encuentra presente en esta revisión.  
  
## <a name="ssdt-hotfix-for-sql-server-2016-rc0"></a>Revisión de SSDT (para SQL Server 2016 RC0)  
Publicación: 18 de marzo de 2016  
  
Número de compilación: 14.0.60316.0  
  
Esta compilación contiene una revisión para la versión de SSDT que proporciona características para SQL Server 2016 RC0. En este momento no hay ninguna versión RC1 de SSDT. La compilación 14.0.60316.0 puede usarse con las versiones RC0 o RC1 de SQL Server 2016.  
      
## <a name="ssdt-february-2016-preview-for-sql-server-2016-rc0"></a>Versión preliminar de febrero de 2016 de SSDT (para SQL Server 2016 RC0)  
Publicación: 7 de marzo de 2016  
  
Número de compilación: 14.0.60305.0  
  
-   **Plantillas de proyecto de SQL Server**  
  
    No hay ningún anuncio para esta versión preliminar de SSDT. Consulte [Novedades de SQL Server 2016 (motor de base de datos)](https://msdn.microsoft.com/library/bb510411.aspx) para obtener información sobre otras características de esta versión.  
  
-   **Plantillas de proyecto de paquetes SSIS**  
  
    El Diseñador SSIS crea y mantiene paquetes de SQL Server 2016, 2014 o 2012. Se ha cambiado el nombre de las nuevas plantillas por elementos. El conector de Hadoop de SSIS admite el formato ORC. Consulte [Novedades de Integration Services en SQL Server 2016](https://msdn.microsoft.com/library/bb522534.aspx) para obtener más información.  
  
-   **Plantillas de proyecto SSAS (proyectos de modelos tabulares)**  
  
    La actualización de este mes en Analysis Services ofrece compatibilidad con carpetas de visualización para modelos tabulares, y cualquier modelo creado con el nuevo nivel de compatibilidad de SQL Server 2016 es ahora compatible con paquetes SSIS. Para obtener más información, consulte la entrada de blog [What's New in Analysis Services](http://blogs.msdn.com/b/analysisservices/archive/2016/01/28/what-s-new-for-sql-server-2016-analysis-services-in-ctp3-3.aspx) (Novedades de Analysis Services).  
  
-   **Plantillas de proyecto de informes de SSRS**  
  
    No hay ningún anuncio para esta versión preliminar de SSDT. Consulte [Novedades de SQL Server Reporting Services (SSRS)](https://msdn.microsoft.com/library/ms170438.aspx) para obtener información sobre otras características de esta versión.  
  
## <a name="ssdt-january-2016-preview"></a>Versión preliminar de enero de 2016 de SSDT  
Publicación: 4 de febrero de 2016  
  
Número de compilación: 14.0.60203.0  
  
-   **Plantillas de proyecto de SQL Server**  
  
    No hay ningún anuncio para esta versión preliminar de SSDT. Consulte [Novedades de SQL Server 2016 (motor de base de datos)](https://msdn.microsoft.com/library/bb510411.aspx) para obtener información sobre otras características de esta CTP.  
  
-   **Plantillas de proyecto de paquetes SSIS**  
  
    Agrega compatibilidad con los componentes de origen y destino de ODBC, una tarea de control de CDC,  
      un componente de origen y divisor de CDC, un Microsoft Connector for SAP BW y un Feature Pack de Integration Services para Azure. Consulte [Novedades de Integration Services en SQL Server 2016](https://msdn.microsoft.com/library/bb522534.aspx) para obtener más información.  
  
-   **Plantillas de proyecto de SSAS**  
  
    Incorpora mejoras para los modelos tabulares en el nivel de compatibilidad 1200, columnas calculadas y seguridad de nivel de fila para modelos en el modo DirectQuery, traducciones de metadatos de modelos, ejecución de scripts de TMSL en la tarea Ejecutar DDL de Analysis Services de SSIS, y numerosas correcciones de errores.  
    Consulte [Novedades de Analysis Services](https://msdn.microsoft.com/library/bb522628.aspx) o la entrada de blog [What's New in Analysis Services](http://blogs.msdn.com/b/analysisservices/archive/2016/01/28/what-s-new-for-sql-server-2016-analysis-services-in-ctp3-3.aspx) (Novedades de Analysis Services) para obtener más información.  
  
-   **Plantillas de proyecto de informes de SSRS**  
  
    No hay ningún anuncio para esta versión preliminar de SSDT. Consulte [Novedades de SQL Server Reporting Services (SSRS)](https://msdn.microsoft.com/library/ms170438.aspx) para obtener información sobre otras características de esta CTP.  
  
## <a name="ssdt-december-2015-preview"></a>Vista previa de SSDT (diciembre de 2015)  
  
-   En las **plantillas de proyecto de SQL Server** se incluyen correcciones de errores del cuadro de diálogo Conexión, listas del historial reciente y el uso apropiado del conjunto de contextos de autenticación de la propiedad de conexión al cargar una lista de bases de datos.  
  
    -   El valor de tiempo de espera de la conexión de prueba se ha cambiado a 15 segundos.  
  
    -   Posibilidad de crear una regla de firewall del servidor de Base de datos SQL de Azure si la dirección IP de cliente no está registrada al cargar una lista de bases de datos.  
  
    -   Compatibilidad con programación de características de SQL Server 2016 CTP 3.2.  
  
-   Las **plantillas de proyecto de SSAS** agregan compatibilidad para crear tablas calculadas a partir de expresiones DAX y otros objetos ya definidos en el modelo.  
  
-   Entre las adiciones de las **plantillas de proyecto de paquetes SSIS** se incluye la compatibilidad con el conector de Hadoop de SSIS para el formato de archivo Avro y la autenticación Kerberos.   
    Tenga en cuenta que aún no se ha incluido en esta actualización la compatibilidad del diseñador de SSIS con SSIS 2012 y 2014.  
  
## <a name="ssdt-november-2015-preview"></a>Vista previa de SSDT (noviembre de 2015)  
  
-   **Plantillas de proyecto de SQL Server**. Versión de vista previa de la experiencia de conexión mejorada para SQL Server y Azure SQL Database.  
  
-   **Plantillas de proyecto de paquetes SSIS**. Mejora del rendimiento del catálogo de SSIS: se ha mejorado el rendimiento de la mayoría de las vistas del catálogo de SSIS para los usuarios que no son administradores de SSIS.  
  
-   Entre las **plantillas de proyecto de SSAS** se incluyen mejoras para proyectos de modelos tabulares en Analysis Services. Puede usar el comando **Ver código** para ver la definición de modelo en JSON. Necesitará una edición completa de Visual Studio 2015 para obtener el editor de JSON. Puede descargar gratis la [edición Visual Studio Community](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).  
  
## <a name="ssdt-october-2015-preview"></a>Vista previa de SSDT (octubre de 2015)  
  
-   Nuevas plantillas de proyecto de BI (modelos de Analysis Services, informes de Reporting Services y paquetes de Integration Services). Todas las plantillas de proyecto de SQL Server se encuentran ahora en una misma versión de SSDT.  
  
-   Nuevas características de SSIS, como el conector de Hadoop, la plantilla de flujo de control y el tamaño de búfer máximo flexible de la tarea Flujo de datos.  
  
-   Compatibilidad con características de SQL Server 2016 CTP 3.0 para proyectos de bases de datos relacionales.  
  
-   Varias correcciones de errores de SSIS y compatibilidad con el sistema operativo Windows 7.  
  
## <a name="ssdt-september-2015-preview"></a>Vista previa de SSDT (septiembre de 2015)  
  
-   Se ha agregado compatibilidad con varios idiomas en esta versión de vista previa.  
  
## <a name="ssdt-august-2015-preview"></a>Vista previa de SSDT (agosto de 2015)  
  
-   Nuevo programa Setup.exe independiente para instalar SSDT.  Ya no tendrá que utilizar una versión modificada del programa de instalación de SQL Server. Esta versión de SSDT incluye una plantilla de proyecto para crear bases de datos relacionales que se implementen en SQL Server o Azure SQL Database.  
  
## <a name="see-also"></a>Vea también  
[Descargar SQL Server Data Tools &#40;SSDT&#41;](../ssdt/download-sql-server-data-tools-ssdt.md)  
[Previous releases of SQL Server Data Tools &#40;SSDT and SSDT-BI&#41;](../ssdt/previous-releases-of-sql-server-data-tools-ssdt-and-ssdt-bi.md) (Versiones anteriores de SQL Server Data Tools [SSDT y SSDT-BI])  
[Novedades de SQL Server 2016 (motor de base de datos)](https://msdn.microsoft.com/library/bb510411.aspx)  
[Novedades de Analysis Services](https://msdn.microsoft.com/library/bb522628.aspx)  
[Novedades de Integration Services en SQL Server 2016](https://msdn.microsoft.com/library/bb522534.aspx)  
  

