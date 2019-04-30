---
title: Ejecución de la consola SSMA (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Database Connection Commands
- Sybase Console,Manageability Commands
- Sybase Console,Migration Commands
- Sybase Console,Migration Preparation Command
- Sybase Console,Project Commands
- Sybase Console,Report Commands
- Sybase Console,Script File Commands
- Sybase Console,Script Generation Commands
ms.assetid: ea8950b7-fabc-4aa4-89f8-9573a2617d70
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6cbdd0a1394114e3fdef0511c7ed14658f7dd9b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126308"
---
# <a name="executing-the-ssma-console-sybasetosql"></a>Ejecución de la consola de SSMA (SybaseToSQL)
Microsoft proporciona un sólido conjunto de script de comandos del archivo para ejecutar y controlar las actividades SSMA. Las secciones que detallan la misma.  
  
## <a name="script-file-commands"></a>Comandos del archivo de script  
La aplicación de consola utiliza ciertos comandos del archivo de script estándar como enumerados en esta sección.  
  
## <a name="project-commands"></a>Comandos de proyecto  
Los comandos de proyecto controlan la creación de proyectos, abrir, guardar y salir de proyectos.  
  
### <a name="create-new-project"></a>create-new-project  
Este comando crea un nuevo proyecto SSMA.  
  
-   `project-folder` indica la carpeta del proyecto que se crean.  
  
-   `project-name` indica el nombre del proyecto. {string}  
  
-   `overwrite-if-exists`Atributo opcional indica si se debe sobrescribir un proyecto existente. {boolean}  
  
-   `project-type:`Atributo opcional. Indica el tipo de proyecto, que es "sql-server-2005" proyecto o proyecto de "sql-server-2008" o "sql-server-2012" proyecto "sql-server-2014" proyecto o proyecto "sql azure". Valor predeterminado es "sql-server-2008".  
  
**Ejemplo de sintaxis:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>" (optional)  
  
   project-type="<sql-server-2008/sql-server-2005/sql-server-2012/sql-server-2014/sql-azure>"  
/>  
```  
Es el atributo 'sobrescribir-if-exists' **false** de forma predeterminada.  
  
Atributo de tipo de proyecto es **sql-server-2008** de forma predeterminada.  
  
### <a name="open-project"></a>open-project  
Este comando abre el proyecto.

-   `project-folder` indica la carpeta del proyecto que se crean. El comando produce un error si la carpeta especificada no existe.  {string}  
  
-   `project-name` indica el nombre del proyecto. El comando produce un error si el proyecto especificado no existe.  {string}  
  
**Ejemplo de sintaxis:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
> [!NOTE]  
> SSMA para la aplicación de consola de SAP ASE admite la compatibilidad con versiones anteriores. Puede usarlo para abrir proyectos creados con una versión anterior de SSMA.  
  
### <a name="save-project"></a>save-project  
Este comando guarda el proyecto de migración.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<save-project/>  
```  
  
### <a name="close-project"></a>close-project  
Este comando cierra el proyecto de migración.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<close-project   
  if-modified="<save/error/ignore>"   (optional)  
/>  
```  
Atributo "if-modificado" es opcional, **omitir** de forma predeterminada.  
  
## <a name="database-connection-commands"></a>Comandos de conexión de base de datos  
Los comandos de conexión de base de datos ayudan a conectar a la base de datos.  
  
> [!NOTE]  
> - El **examinar** no se admite la característica de la interfaz de usuario en la consola.  
> - Para obtener más información en "Crear archivos de Script", consulte [crear archivos de Script &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
### <a name="connect-source-database"></a>connect-source-database  
Este comando realiza la conexión a la base de datos de origen y carga los metadatos de alto nivel de la base de datos de origen, pero no todos los metadatos.
  
Si no se puede establecer la conexión al origen, se genera un error y la aplicación de consola detiene la ejecución.
  
El atributo de nombre definido para cada conexión en la sección servidor de archivo de conexión de servidor o el archivo de script se recupera la definición del servidor.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="force-load-sourcetarget-database"></a>force-load-source/target-database  
Este comando carga los metadatos de origen, y resulta útil para trabajar en el proyecto de migración sin conexión.  
  
Si no se puede establecer la conexión con el origen o destino, se genera un error y la aplicación de consola detiene la ejecución.  
  
Este comando requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<force-load metabase="<source/target>" >  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
  
### <a name="reconnect-source-database"></a>reconnect-source-database  
Este comando vuelve a conectarse a la base de datos de origen, pero no carga los metadatos a diferencia del comando de base de datos connect-origen.  
  
Si no puede establecerse (la conexión con el origen re), se genera un error y la aplicación de consola detiene la ejecución.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="connect-target-database"></a>connect-target-database  
Este comando se conecta a la base de datos de SQL Server de destino y carga los metadatos de alto nivel de la base de datos de destino pero no los metadatos por completo.  
  
Si no se puede establecer la conexión con el destino, se genera un error y la aplicación de consola detiene la ejecución.  
  
El atributo de nombre definido para cada conexión en la sección servidor de archivo de conexión de servidor o el archivo de script se recupera la definición del servidor.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
  
### <a name="reconnect-target-database"></a>reconnect-target-database  
  
Este comando vuelve a conectarse a la base de datos de destino pero no carga los metadatos, a diferencia del comando de base de destino de connect.  
  
Si no puede establecerse (re) de la conexión con el destino, se genera un error y la aplicación de consola detiene la ejecución.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-commands"></a>Comandos de informes  
Los comandos de informe generan informes sobre el rendimiento de diversas actividades de la consola SSMA.  
  
### <a name="generate-assessment-report"></a>generate-assessment-report  
  
Este comando genera informes de evaluación de la base de datos de origen.  
  
Si no se realiza la conexión de base de datos de origen antes de ejecutar este comando, se genera un error y se cierra la aplicación de consola.  
  
No se puede conectar al servidor de base de datos de origen durante la ejecución del comando, también produce la finalización de la aplicación de consola.  
  
-   `conversion-report-folder:` Especifica la carpeta en la que se puede almacenar el informe de evaluación. (atributo opcional)  
  
-   `object-name:` Especifica los objetos que tienen en cuenta para la generación de informes de evaluación (admite nombres de objeto individuales o un nombre de objeto de grupo).  
  
-   `object-type:` Especifica el tipo del objeto que se mencionan en el atributo de nombre de objeto (si se especifica la categoría de objeto, tipo de objeto será "categoría").  
  
-   `conversion-report-overwrite:` Especifica si se debe sobrescribir la carpeta de informes de evaluación si ya existe.  
  
    **Valor predeterminado:** false. (atributo opcional)  
  
-   `write-summary-report-to:` Especifica la ruta de acceso a la que se generará el informe.  
  
    Si solo se menciona la ruta de acceso de carpeta, a continuación, archivos por nombre **AssessmentReport&lt;n&gt;. XML** se crea. (atributo opcional)  
  
    Creación de informes tiene dos subcategorías adicionales:  
  
    -   `report-errors` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
    -   `verbose` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
**Ejemplo de sintaxis:**  
  
```xml  
<generate-assessment-report  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  assessment-report-folder="<folder-name>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
o Administrador de configuración de  
  
```xml  
<generate-assessment-report  
  
  assessment-report-folder="<folder-name>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
<metabase-object object-name="<object-name>"  
  
        object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-commands"></a>Comandos de migración  
Los comandos de migración conversión el esquema de base de datos de destino en el esquema de origen y migración datos al servidor de destino.  
  
### <a name="convert-schema"></a>convert-schema  
Este comando realiza la conversión de esquema de origen al esquema de destino.  
  
Si no se realiza la conexión de base de datos de origen o de destino antes de ejecutar este comando o se produce un error en la conexión con el servidor de base de datos de origen o destino durante la ejecución del comando, se genera un error y se cierra la aplicación de consola.  
  
-   `conversion-report-folder:` Especifica la carpeta en la que se puede almacenar el informe de evaluación. (atributo opcional)  
  
-   `object-name:` Especifica los objetos de origen que se consideran para la conversión de esquema (admite nombres de objeto individuales o un nombre de objeto de grupo).  
  
-   `object-type:` Especifica el tipo del objeto que se mencionan en el atributo de nombre de objeto (si se especifica la categoría de objeto, tipo de objeto será "categoría").  
  
-   `conversion-report-overwrite:` Especifica si se debe sobrescribir la carpeta de informes de evaluación si ya existe.  
  
    **Valor predeterminado:** false. (atributo opcional)  
  
-   `write-summary-report-to:` Especifica la ruta de acceso a la que se generará el informe de resumen.  
  
    Si solo se menciona la ruta de acceso de carpeta, a continuación, archivos por nombre **SchemaConversionReport&lt;n&gt;. XML** se crea. (atributo opcional)  
  
    Creación de informes tiene dos subcategorías adicionales:  
  
    -   `report-errors` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
    -   `verbose` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
**Ejemplo de sintaxis:**  
  
```xml  
<convert-schema  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  write-summary-report-to="<file-name/folder-name>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder-name>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
o Administrador de configuración de  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder-name>"         (optional)  
  
  conversion-report-overwrite="<true/false>"> (optional)  
  
  <metabase-object object-name="<object-name>"  
  
    object-type="<object-category>"/>  
  
</convert-schema>  
```  
  
### <a name="migrate-data"></a>migrar datos  
Este comando migra los datos de origen al destino.  
  
-   `object-name:` Especifica los objetos de origen tienen en cuenta para migrar datos (admite nombres de objeto individuales o un nombre de objeto de grupo).  
  
-   `object-type:` Especifica el tipo del objeto que se mencionan en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `write-summary-report-to:` Especifica la ruta de acceso a la que se generará el informe.  
  
    Si solo se menciona la ruta de acceso de carpeta, a continuación, archivos por nombre **DataMigrationReport&lt;n&gt;. XML** se crea. (atributo opcional)  
  
    Creación de informes tiene dos subcategorías adicionales:  
  
    -   `report-errors` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
    -   `verbose` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
**Ejemplo de sintaxis:**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>">  
  
    <metabase-object object-name="<object-name>"/>  
  
    <metabase-object object-name="<object-name>"/>  
  
    <metabase-object object-name="<object-name>"/>  
  
    <data-migration-connection  
  
      source-use-last-used="true"/source-server="<server-unique-name>"  
  
      target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
o Administrador de configuración de  
  
```xml  
<migrate-data  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-command"></a>Comando de preparación de migración  
El comando de preparación de la migración inicia la asignación de esquema entre las bases de datos de origen y de destino.  
  
> [!NOTE]  
> La salida de consola predeterminada para los comandos de migración es el informe de salida 'Full' con ningún informe de error detallado: Resumen solo al nodo raíz del árbol de objeto de origen.  
  
### <a name="map-schema"></a>map-schema  
Este comando proporciona la asignación de esquema de la base de datos de origen al esquema de destino.  
  
-   `source-schema` Especifica el esquema de origen para migrar.  
  
-   `sql-server-schema` Especifica el esquema de destino al que se migrará el esquema de origen.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<map-schema source-schema="<source-schema>"  
  
sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-commands"></a>Comandos de facilidad de uso  
Los comandos de facilidad de uso ayudan a sincronizar los objetos de base de datos de destino con la base de datos de origen.  
  
> [!NOTE]  
> La salida de consola predeterminada para los comandos de migración es el informe de salida 'Full' con ningún informe de error detallado: Resumen solo al nodo raíz del árbol de objeto de origen.  
  
### <a name="synchronize-target"></a>sincronizar de destino  
Este comando sincroniza los objetos de destino con la base de datos de destino.  
 
Si este comando se ejecuta en la base de datos de origen, se produce un error.  
  
Si no se realiza la conexión de base de datos de destino antes de ejecutar este comando o se produce un error en la conexión al servidor de base de datos de destino durante la ejecución del comando, se genera un error y se cierra la aplicación de consola.  
  
-   `object-name:` Especifica los objetos de destino que se consideran para la sincronización con la base de datos de destino (admite nombres de objeto individuales o un nombre de objeto de grupo).  
  
-   `object-type:` Especifica el tipo del objeto que se mencionan en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `on-error:` Especifica si se debe especificar los errores de sincronización como advertencias o errores. Opciones disponibles para en caso de error:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
-   `report-errors-to:` Especifica la ubicación del informe de errores para la operación de sincronización (atributo opcional). Si solo se proporciona la ruta de acceso de carpeta, a continuación, archivos por nombre **TargetSynchronizationReport.XML** se crea.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<synchronize-target  
  
object-name="<object-name>"  
  
on-error="<report-total-as-warning/  
  
report-each-as-warning/  
  
fail-script>" (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
o Administrador de configuración de  
  
```xml  
<synchronize-target  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"/>  
```  
o Administrador de configuración de  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
  
### <a name="refresh-from-database"></a>refresh-from-database  
Este comando actualiza los objetos de base de datos de origen.  
  
Si este comando se ejecuta en la base de datos de destino, se genera un error.  
  
Este comando requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
-   `object-name:` Especifica los objetos de origen que se consideran para la actualización de base de datos de origen (admite nombres de objeto individuales o un nombre de objeto de grupo).  
  
-   `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `on-error:` Especifica si se debe llamar a los errores de actualización como advertencias o errores. Opciones disponibles para en caso de error:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   fail-script  
  
-   `report-errors-to:` Especifica la ubicación del informe de errores para la operación de actualización (atributo opcional). Si solo se proporciona la ruta de acceso de carpeta, a continuación, archivos por nombre **SourceDBRefreshReport.XML** se crea.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  on-error="<report-total-as-warning/  
  
             report-each-as-warning/  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
o Administrador de configuración de  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  object-type="<object-category>" />  
```  
o Administrador de configuración de  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-commands"></a>Secuencias de comandos de generación  
Los comandos de generación de scripts realizan dos tareas: ayudan a guardar la salida en un archivo de script en la consola y registran la salida de T-SQL en la consola o un archivo basado en el parámetro especificado.  
  
### <a name="save-as-script"></a>Guardar como secuencia de comandos  
Este comando se utiliza para guardar los Scripts de los objetos en un archivo se ha mencionado cuando metabase = target. Esta es una alternativa al comando de sincronización en que se obtención de las secuencias de comandos y ejecutar la misma base de datos de destino.  
  
Este comando requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
-   `object-name:` Especifica los objetos cuyas secuencias de comandos son para guardarse (admite nombres de objeto individuales o un nombre de objeto de grupo).  
  
-   `object-type:` Especifica el tipo del objeto que se mencionan en el atributo de nombre de objeto (si se especifica la categoría de objeto, tipo de objeto será "categoría").  
  
-   `metabase:` Especifica si es el origen o destino de la metabase.  
  
-   `destination:` Especifica la ruta de acceso o la carpeta en la que se debe guardar el script. Si no se especifica el nombre de archivo, se proporcionará un nombre de archivo en el .out formato (valor del atributo object_name).
  
-   `overwrite:` Si es true, a continuación, sobrescribe el mismo nombre de archivo si existe. Puede tener los valores (true/false).  
  
**Ejemplo de sintaxis:**  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  destination="<file-name/folder-name>"  
  
  overwrite="<true/false>"   (optional)  
  
/>  
```  
o Administrador de configuración de  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file-name/folder-name>"  
  
    <metabase-object object-name="<object-name>"  
  
                     object-type="<object-category>"/>  
  
</save-as-script>  
```  
  
### <a name="convert-sql-statement"></a>convert-sql-statement
Este comando convierte la instrucción SQL.  
  
-   `context` Especifica el nombre del esquema.  
  
-   `destination` Especifica si la salida debe almacenarse en un archivo.  
  
    Si no se especifica este atributo, la instrucción T-SQL convertida se muestra en la consola. (atributo opcional)  
  
-   `conversion-report-folder` Especifica la carpeta en la que se puede almacenar el informe de evaluación. (atributo opcional)  
  
-   `conversion-report-overwrite` Especifica si se debe sobrescribir la carpeta de informes de evaluación si ya existe.  
  
    **Valor predeterminado:** false. (atributo opcional)  
  
-   `write-converted-sql-to` Especifica la ruta de acceso de carpeta de archivo (o) que debe almacenarse el T-SQL convertido. Cuando se especifica una ruta de acceso de carpeta junto con el `sql-files` atributo, cada archivo de origen tiene un destino correspondiente archivo de Transact-SQL creado en la carpeta especificada. Cuando se especifica una ruta de acceso de carpeta junto con el `sql` atributo, el T-SQL convertido se escribe en un archivo denominado Result.out en la carpeta especificada.  
  
-   `sql` Especifica las instrucciones sql de Sybase a convertirse, una o varias instrucciones se pueden separar con un ";"  
  
-   `sql-files` Especifica la ruta de acceso de los archivos de sql que se va a convertir en el código de T-SQL.  
  
-   `write-summary-report-to` Especifica la ruta de acceso donde se generará el informe de resumen. Si solo se menciona la ruta de acceso de carpeta, a continuación, archivos por nombre **ConvertSQLReport.XML** se crea. (atributo opcional)  
  
    Creación de informes de resumen tiene dos subcategorías adicionales, a saber:  
  
    -   informe de errores (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales)).  
  
    -   verbose (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales)).  
  
Este comando requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
**Ejemplo de sintaxis:**  
  
```  
<convert-sql-statement  
  
       context="<database-name>.<schema-name>"  
  
        conversion-report-folder="<folder-name>"  
  
        conversion-report-overwrite="<true/false>"  
  
        write-summary-report-to="<file-name/folder-name>"   (optional)  
  
        verbose="<true/false>"   (optional)  
  
        report-errors="<true/false>"   (optional)  
  
        destination="<stdout/file>"   (optional)  
  
        write-converted-sql-to ="<file-name/folder-name>"  
  
        sql="SELECT 1 FROM DUAL;">  
  
    <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
o Administrador de configuración de  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         write-summary-report-to="<file-name/folder-name>"   (optional)  
  
         verbose="<true/false>"   (optional)  
  
         report-errors="<true/false>"   (optional)  
  
         destination="<stdout/file>"   (optional)  
  
         write-converted-sql-to ="<file-name/folder-name>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
o Administrador de configuración de  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-steps"></a>Pasos siguientes  
Para obtener información sobre las opciones de línea de comandos, consulte [opciones de línea de comandos en la consola de SSMA (AccessToSQL)](../access/command-line-options-in-ssma-console-accesstosql.md).  
  
Para obtener información sobre un archivo de script de la consola de ejemplo, vea [trabajar con los archivos de Script de la consola de ejemplo &#40;SybaseToSQL&#41;](../../ssma/sybase/working-with-the-sample-console-script-files-sybasetosql.md)  
  
El paso siguiente depende de los requisitos del proyecto:  
  
-   Para especificar una contraseña o la exportación / importación de contraseñas, vea [administrar contraseñas &#40;SybaseToSQL&#41;](../../ssma/sybase/managing-passwords-sybasetosql.md).  
  
-   Para generar informes, vea [generar informes &#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md).  
  
-   Para solucionar problemas en la consola, consulte [Troubleshooting &#40;SybaseToSQL&#41;](../../ssma/sybase/troubleshooting-sybasetosql.md).  
  
