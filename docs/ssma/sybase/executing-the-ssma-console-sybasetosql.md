---
title: Ejecutar la consola SSMA (SybaseToSQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: "22"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 998f882c0cd351f1df95cb8177ce93d6b06ed09a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="executing-the-ssma-console-sybasetosql"></a>Ejecutar la consola SSMA (SybaseToSQL)
Microsoft proporciona un conjunto robusto de script de comandos del archivo para ejecutar y controlar las actividades SSMA. Las secciones posteriores detallan los mismos.  
  
## <a name="script-file-commands"></a>Comandos del archivo de script  
La aplicación de consola utiliza ciertos comandos del archivo de secuencia de comandos estándar como enumerados en esta sección.  
  
## <a name="project-commands"></a>Comandos de proyecto  
Los comandos de proyectos controlan la creación de proyectos, abrir, guardar y salir de proyectos.  
  
### <a name="create-new-project"></a>Crear nueva-proyectos  
Este comando crea un nuevo proyecto SSMA.  
  
-   `project-folder`indica la carpeta del proyecto obtener creado.  
  
-   `project-name`indica el nombre del proyecto. {cadena}  
  
-   `overwrite-if-exists`Atributo opcional indica si se debe sobrescribir un proyecto existente. {valor} booleano  
  
-   `project-type:`Atributo opcional. Indica el tipo de proyecto, que es el proyecto "sql-server-2005" o "sql-server-2008" proyecto o proyecto "sql-server-2012" o "sql-server-2014" proyecto o proyecto "sql azure". Valor predeterminado es "sql-server-2008".  
  
**Ejemplo de sintaxis:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>" (optional)  
  
   project-type=”<sql-server-2008/sql-server-2005/sql-server-2012/sql-server-2014/sql-azure>”  
/>  
```  
Es el atributo 'sobrescribir-if-exists' **false** de forma predeterminada.  
  
El atributo 'tipo de proyecto' es **sql-server-2008** de forma predeterminada.  
  
### <a name="open-project"></a>Abrir proyecto  
Este comando abre el proyecto.

-   `project-folder`indica la carpeta del proyecto obtener creado. El comando produce un error si la carpeta especificada no existe.  {cadena}  
  
-   `project-name`indica el nombre del proyecto. El comando produce un error si el proyecto especificado no existe.  {cadena}  
  
**Ejemplo de sintaxis:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
> [!NOTE]  
> SSMA para la aplicación de consola de SAP ASE admite compatibilidad con versiones anteriores. Puede usarlo para abrir proyectos creados con una versión anterior de SSMA.  
  
### <a name="save-project"></a>Guardar proyecto  
Este comando guarda el proyecto de migración.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<save-project/>  
```  
  
### <a name="close-project"></a>Cerrar proyecto  
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
> - Para obtener más información sobre 'Crear archivos de Script', vea [crear archivos de Script &#40; SybaseToSQL &#41; ](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
### <a name="connect-source-database"></a>datos de origen conectarse  
Este comando realiza la conexión a la base de datos de origen y carga los metadatos de alto nivel de la base de datos de origen, pero no todos los metadatos.
  
Si no se puede establecer la conexión con el origen, se genera un error y la aplicación de consola detiene la ejecución.
  
La definición del servidor se recupera desde el atributo de nombre definido para cada conexión en la sección servidor del archivo de conexión de servidor o el archivo de script.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="force-load-sourcetarget-database"></a>forzar carga-origen/destino-bases de datos  
Este comando carga los metadatos de origen, y resulta útil para trabajar en el proyecto de migración sin conexión.  
  
Si no se puede establecer la conexión con el origen o destino, se genera un error y la aplicación de consola detiene la ejecución.  
  
Este comando requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<force-load metabase=”<source/target>” >  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
  
### <a name="reconnect-source-database"></a>datos de origen volver a conectar  
Este comando vuelve a conectarse a la base de datos de origen pero no carga los metadatos a diferencia del comando de datos de origen de conexión.  
  
Si no se puede establecer el volver a conectar con el origen, se genera un error y la aplicación de consola detiene la ejecución.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="connect-target-database"></a>datos de destino conectarse  
Este comando se conecta a la base de datos de SQL Server de destino y carga los metadatos de alto nivel de la base de datos de destino pero no los metadatos por completo.  
  
Si no se puede establecer la conexión con el destino, se genera un error y la aplicación de consola detiene la ejecución.  
  
La definición del servidor se recupera desde el atributo de nombre definido para cada conexión en la sección servidor del archivo de conexión de servidor o el archivo de script.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
  
### <a name="reconnect-target-database"></a>datos de destino volver a conectar  
  
Este comando vuelve a conectarse a la base de datos de destino pero no carga los metadatos, a diferencia del comando de conexión de datos de destino.  
  
Si la (conexión con el destino re) no se puede establecer, se genera un error y la aplicación de consola detiene la ejecución.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-commands"></a>Comandos de informe  
Los comandos de informes generan informes sobre el rendimiento de diversas actividades de consola SSMA.  
  
### <a name="generate-assessment-report"></a>informe de evaluación generar  
  
Este comando genera informes de evaluación de la base de datos de origen.  
  
Si no se realiza la conexión de base de datos de origen antes de ejecutar este comando, se genera un error y se cierra la aplicación de consola.  
  
No se pudo conectar al servidor de base de datos de origen durante la ejecución del comando, también se produce en terminar la aplicación de consola.  
  
-   `conversion-report-folder:`Especifica la carpeta en la que se puede almacenar el informe de evaluación. (opcional) (atributo)  
  
-   `object-name:`Especifica los objetos que se consideran para la generación de informes de evaluación (admite nombres de objeto individual o un nombre de objeto de grupo).  
  
-   `object-type:`Especifica el tipo del objeto mencionado en el atributo de nombre de objeto (si se especifica la categoría de objeto, tipo de objeto será "categoría").  
  
-   `conversion-report-overwrite:`Especifica si se debe sobrescribir la carpeta de informes de evaluación si ya existe.  
  
    **Valor predeterminado:** false. (opcional) (atributo)  
  
-   `write-summary-report-to:`Especifica la ruta de acceso a la que se generará el informe.  
  
    Si solo se menciona la ruta de acceso de carpeta, archivo, a continuación, por nombre **AssessmentReport&lt;n&gt;. XML** se crea. (opcional) (atributo)  
  
    Creación de informes tiene dos subcategorías adicionales:  
  
    -   `report-errors`(= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
    -   `verbose`(= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
**Ejemplo de sintaxis:**  
  
```xml  
<generate-assessment-report  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>”             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  assessment-report-folder="<folder-name>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
o bien  
  
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
Los comandos de migración convertir el esquema de base de datos de destino en el esquema de origen y migración los datos al servidor de destino.  
  
### <a name="convert-schema"></a>convertir esquema  
Este comando realiza la conversión de esquema de origen al esquema de destino.  
  
Si no se realiza la conexión de base de datos de origen o de destino antes de ejecutar este comando o se produce un error en la conexión con el servidor de base de datos de origen o de destino durante la ejecución del comando, se genera un error y se cierra la aplicación de consola.  
  
-   `conversion-report-folder:`Especifica la carpeta en el que se puede almacenar el informe de evaluación. (opcional) (atributo)  
  
-   `object-name:`Especifica los objetos de origen que se consideran para la conversión de esquema (admite nombres de objeto individual o un nombre de objeto de grupo).  
  
-   `object-type:`Especifica el tipo del objeto mencionado en el atributo de nombre de objeto (si se especifica la categoría de objeto, tipo de objeto será "categoría").  
  
-   `conversion-report-overwrite:`Especifica si se debe sobrescribir la carpeta de informes de evaluación si ya existe.  
  
    **Valor predeterminado:** false. (opcional) (atributo)  
  
-   `write-summary-report-to:`Especifica la ruta de acceso a la que se generará el informe de resumen.  
  
    Si solo se menciona la ruta de acceso de carpeta, archivo, a continuación, por nombre **SchemaConversionReport&lt;n&gt;. XML** se crea. (opcional) (atributo)  
  
    Creación de informes tiene dos subcategorías adicionales:  
  
    -   `report-errors`(= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
    -   `verbose`(= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
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
o bien  
  
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
  
-   `object-name:`Especifica los objetos de origen que se tienen en cuenta para migrar datos (admite nombres de objeto individual o un nombre de objeto de grupo).  
  
-   `object-type:`Especifica el tipo del objeto mencionado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `write-summary-report-to:`Especifica la ruta de acceso a la que se generará el informe.  
  
    Si solo se menciona la ruta de acceso de carpeta, archivo, a continuación, por nombre **DataMigrationReport&lt;n&gt;. XML** se crea. (opcional) (atributo)  
  
    Creación de informes tiene dos subcategorías adicionales:  
  
    -   `report-errors`(= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
    -   `verbose`(= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
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
o bien  
  
```xml  
<migrate-data  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-command"></a>Comandos de preparación de la migración  
El comando de preparación de la migración inicia la asignación de esquema entre las bases de datos de origen y de destino.  
  
> [!NOTE]  
> La salida de consola predeterminada para los comandos de migración es informe de salida 'Total' con ningún informe de error detallado: resumen sólo en el nodo de raíz del árbol de objeto de origen.  
  
### <a name="map-schema"></a>esquema de asignación  
Este comando proporciona la asignación de esquema de la base de datos de origen al esquema de destino.  
  
-   `source-schema`Especifica el esquema de origen para migrar.  
  
-   `sql-server-schema`Especifica el esquema de destino al que se migrará el esquema de origen.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<map-schema source-schema="<source-schema>"  
  
sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-commands"></a>Comandos de facilidad de uso  
Los comandos de facilidad de uso ayudan a sincronizar los objetos de base de datos de destino con la base de datos de origen.  
  
> [!NOTE]  
> La salida de consola predeterminada para los comandos de migración es informe de salida 'Total' con ningún informe de error detallado: resumen sólo en el nodo de raíz del árbol de objeto de origen.  
  
### <a name="synchronize-target"></a>destino sincronizar  
Este comando sincroniza los objetos de destino con la base de datos de destino.  
 
Si este comando se ejecuta en la base de datos de origen, se produce un error.  
  
Si no se realiza la conexión de base de datos de destino antes de ejecutar este comando o se produce un error en la conexión con el servidor de base de datos de destino durante la ejecución del comando, se genera un error y se cierra la aplicación de consola.  
  
-   `object-name:`Especifica los objetos de destino que se consideran para la sincronización con la base de datos de destino (admite nombres de objeto individual o un nombre de objeto de grupo).  
  
-   `object-type:`Especifica el tipo del objeto mencionado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `on-error:`Especifica si se debe especificar los errores de sincronización como advertencias o errores. Opciones disponibles en el error:  
  
    -   total de informes como advertencia  
  
    -   informes-each-como-advertencia  
  
    -   Error-script  
  
-   `report-errors-to:`Especifica la ubicación del informe de error para la operación de sincronización (atributo opcional). Si solo se proporciona la ruta de acceso de carpeta, archivo, a continuación, por nombre **TargetSynchronizationReport.XML** se crea.  
  
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
o bien  
  
```xml  
<synchronize-target  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"/>  
```  
o bien  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
  
### <a name="refresh-from-database"></a>actualización de base de datos  
Este comando actualiza los objetos de origen de base de datos.  
  
Si este comando se ejecuta en la base de datos de destino, se genera un error.  
  
Este comando requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
-   `object-name:`Especifica los objetos de origen que se consideran para actualizar desde la base de datos de origen (admite nombres de objeto individual o un nombre de objeto de grupo).  
  
-   `object-type:`Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `on-error:`Especifica si se debe llamar a los errores de actualización como advertencias o errores. Opciones disponibles en el error:  
  
    -   total de informes como advertencia  
  
    -   informes-each-como-advertencia  
  
    -   Error-script  
  
-   `report-errors-to:`Especifica la ubicación del informe de error para la operación de actualización (atributo opcional). Si solo se proporciona la ruta de acceso de carpeta, archivo, a continuación, por nombre **SourceDBRefreshReport.XML** se crea.  
  
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
o bien  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  object-type="<object-category>" />  
```  
o bien  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-commands"></a>Secuencias de comandos de generación  
Los comandos de generación de Script realizan dos tareas: ayudan a guardar la salida en un archivo de script en la consola y registre la salida de T-SQL en la consola o un archivo basado en el parámetro especificado.  
  
### <a name="save-as-script"></a>Guardar como secuencia de comandos  
Este comando se utiliza para guardar las secuencias de comandos de los objetos en un archivo se ha mencionado cuando metabase = destino. Esto es una alternativa al comando de sincronización en que se obtenga las secuencias de comandos y ejecutar la misma base de datos de destino.  
  
Este comando requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
-   `object-name:`Especifica los objetos cuyos scripts son guardarse (admite nombres de objeto individual o un nombre de objeto de grupo).  
  
-   `object-type:`Especifica el tipo del objeto mencionado en el atributo de nombre de objeto (si se especifica la categoría de objeto, tipo de objeto será "categoría").  
  
-   `metabase:`Especifica si es el origen o destino de la metabase.  
  
-   `destination:`Especifica la ruta de acceso o la carpeta en la que se debe guardar el script. Si no se proporciona el nombre de archivo, se proporcionará un nombre de archivo en el formato (valor del atributo object_name) .out.
  
-   `overwrite:`Si es true, a continuación, sobrescribe el mismo nombre de archivo si existe. Puede tener los valores (verdadero/falso).  
  
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
o bien  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file-name/folder-name>"  
  
    <metabase-object object-name="<object-name>"  
  
                     object-type="<object-category>"/>  
  
</save-as-script>  
```  
  
### <a name="convert-sql-statement"></a>instrucción de sql Convert
Este comando convierte la instrucción SQL.  
  
-   `context`Especifica el nombre del esquema.  
  
-   `destination`Especifica si la salida debe almacenarse en un archivo.  
  
    Si no se especifica este atributo, la instrucción de T-SQL convertida se muestra en la consola. (opcional) (atributo)  
  
-   `conversion-report-folder`Especifica la carpeta en la que se puede almacenar el informe de evaluación. (opcional) (atributo)  
  
-   `conversion-report-overwrite`Especifica si se debe sobrescribir la carpeta de informes de evaluación si ya existe.  
  
    **Valor predeterminado:** false. (opcional) (atributo)  
  
-   `write-converted-sql-to`Especifica la ruta de acceso de archivo (o) que debe almacenarse el T-SQL convertido. Cuando se especifica una ruta de acceso de carpeta junto con el `sql-files` atributo, cada archivo de origen tiene un destino correspondiente archivo de código T-SQL creado en la carpeta especificada. Cuando se especifica una ruta de acceso de carpeta junto con el `sql` atributo, el T-SQL convertido se escribe en un archivo denominado Result.out en la carpeta especificada.  
  
-   `sql`Especifica las instrucciones de sql de Sybase se convierta, una o varias instrucciones pueden estar separadas por un ";"  
  
-   `sql-files`Especifica la ruta de acceso de los archivos de sql que se tiene que convertir a código de T-SQL.  
  
-   `write-summary-report-to`Especifica la ruta de acceso donde se generará el informe de resumen. Si solo se menciona la ruta de acceso de carpeta, archivo, a continuación, por nombre **ConvertSQLReport.XML** se crea. (opcional) (atributo)  
  
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
o bien  
  
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
o bien  
  
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
  
Para obtener información sobre un archivo de secuencia de comandos de consola de ejemplo, vea [trabajar con los archivos de comandos de consola de ejemplo &#40; SybaseToSQL &#41;](../../ssma/sybase/working-with-the-sample-console-script-files-sybasetosql.md)  
  
El paso siguiente depende de los requisitos del proyecto:  
  
-   Para especificar una contraseña o la exportación / importación de contraseñas, vea [administrar contraseñas &#40; SybaseToSQL &#41; ](../../ssma/sybase/managing-passwords-sybasetosql.md).  
  
-   Para generar informes, vea [generación de informes &#40; SybaseToSQL &#41; ](../../ssma/sybase/generating-reports-sybasetosql.md).  
  
-   Para solucionar problemas en la consola, consulte [Troubleshooting &#40; SybaseToSQL &#41; ](../../ssma/sybase/troubleshooting-sybasetosql.md).  
  
