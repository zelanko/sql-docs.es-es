---
title: Ejecutar la consola SSMA (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Script file commands, Database connection commands
- Script file commands, Manageability commands
- Script file commands, Migration commands
- Script file commands, Migration preparation commands
- Script file commands, project commands
- Script file commands, Report commands
- Script file commands, Script generation commands
ms.assetid: e3e9f7e4-0619-4861-a202-3d5d39953b26
caps.latest.revision: 25
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a3af52acedfa86cc969e8c2ced508e30a5ddd1f5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="executing-the-ssma-console-mysqltosql"></a>Ejecutar la consola SSMA (MySQLToSQL)
Microsoft proporciona un conjunto robusto de script de comandos del archivo para ejecutar y controlar las actividades SSMA.  
  
La aplicación de consola utiliza ciertos comandos del archivo de secuencia de comandos estándar como enumerados en esta sección.  
  
## <a name="project--script-file-commands"></a>Comandos del archivo de Script de proyecto  
**Command**  
  
Crear-nuevo-proyecto:   
                   Crea un nuevo proyecto SSMA.  
  
Los comandos de proyectos controlan la creación de proyectos, abrir, guardar y salir de proyectos.  
  
**Script**  
  
1.  `project-folder` indica la carpeta del proyecto obtener creado.  
  
2.  `project-name` indica el nombre del proyecto. {cadena}  
  
3.  `overwrite-if-exists`Atributo opcional indica si se debe sobrescribir un proyecto existente. {valor} booleano  
  
4.  `project-type:`Atributo opcional. Indica "el tipo de proyecto, es decir,"sql-server-2005"proyecto proyecto"sql-server-2008"o sql-server-2012" o "sql-server-2014" proyecto o proyecto "sql azure". Valor predeterminado es "sql-server-2008".  
  
**Ejemplo de sintaxis:**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type==”<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>”   (optional)  
  
/>  
```  
Es el atributo 'sobrescribir-if-exists' **false** de forma predeterminada.  
  
El atributo 'tipo de proyecto' es **sql-server-2008** de forma predeterminada.  
  
**Command**  
  
proyecto de apertura:   
                  Abre un proyecto existente.  
  
**Script**  
  
1.  `project-folder` indica la carpeta del proyecto obtener creado. El comando produce un error si la carpeta especificada no existe.  {cadena}  
  
2.  `project-name` indica el nombre del proyecto. El comando produce un error si el proyecto especificado no existe.  {cadena}  
  
**Ejemplo de sintaxis:**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
> [!IMPORTANT]  
> SSMA para la aplicación de consola MySQL admite compatibilidad con versiones anteriores. Podrá abrir proyectos creados con una versión anterior de SSMA.  
  
**Command**  
  
Guardar proyecto: guarda el proyecto de migración.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<save-project/>  
```  
**Command**  
  
Cerrar proyecto  
                  : Cierra el proyecto de migración.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<save-project/>  
```  
**Command**  
  
Cerrar proyecto  
                  : Cierra el proyecto de migración.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
Atributo "if-modificado" es opcional, **omitir** de forma predeterminada.  
  
## <a name="database-connection-script-file-commands"></a>Comandos del archivo de Script de conexión de base de datos  
Los comandos de conexión de base de datos ayudan a conectar a la base de datos.  
  
1.  El **examinar** no se admite la característica de la interfaz de usuario en la consola.  
  
2.  El **autenticación de windows** y **puerto** parámetros no son aplicables al conectarse a SQL Azure.  
  
3.  Para obtener más información sobre 'Crear archivos de Script', vea [crear archivos de Script &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-script-files-mysqltosql.md).  
  
**Command**  
  
datos de origen conectarse  
  
-   Realiza la conexión a la base de datos de origen y carga los metadatos de nivel alto de la base de datos de origen, pero no todos los metadatos.  
  
-   Si no se puede establecer la conexión con el origen, se genera un error y la aplicación de consola detiene la ejecución  
  
**Script**  
  
Definición de servidor se recupera desde el atributo de nombre definido para cada conexión en la sección servidor del archivo de conexión de servidor o el archivo de script.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
forzar carga-origen/destino-bases de datos  
  
-   Carga los metadatos de origen.  
  
-   Resulta útil para trabajar en el proyecto de migración sin conexión.  
  
-   Si no se puede establecer la conexión con el origen o destino, se genera un error y la aplicación de consola detiene la ejecución  
  
**Script**  
  
Requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<force-load metabase="<source/target>"  
  
      <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Command**  
  
datos de origen volver a conectar  
  
1.  Vuelve a conectarse a la base de datos de origen pero no carga los metadatos a diferencia del comando de datos de origen de conexión.  
  
2.  Si no se puede establecer el volver a conectar con el origen, se genera un error y la aplicación de consola detiene la ejecución.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
datos de destino conectarse  
  
1.  Se conecta a la base de datos de SQL Server o SQL Azure de destino y carga los metadatos de nivel alto de la base de datos de destino pero no los metadatos por completo.  
  
2.  Si no se puede establecer la conexión con el destino, se genera un error y la aplicación de consola detiene la ejecución.  
  
**Script**  
  
Definición de servidor se recupera desde el atributo de nombre definido para cada conexión en la sección servidor del archivo de conexión de servidor o el archivo de script  
  
**Ejemplo de sintaxis:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Command**  
  
datos de destino volver a conectar  
  
1.  Vuelve a conectarse a la base de datos de destino pero no carga los metadatos, a diferencia del comando de conexión de datos de destino.  
  
2.  Si la (conexión con el destino re) no se puede establecer, se genera un error y la aplicación de consola detiene la ejecución.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>Comandos del archivo de Script de informe  
Los comandos de informes generan informes sobre el rendimiento de diversas actividades de consola SSMA.  
  
**Command**  
  
informe de evaluación generar  
  
1.  Genera informes de evaluación de la base de datos de origen.  
  
2.  Si no se realiza la conexión de base de datos de origen antes de ejecutar este comando, se genera un error y se cierra la aplicación de consola.  
  
3.  No se pudo conectar al servidor de base de datos de origen durante la ejecución del comando, también se produce en terminar la aplicación de consola.  
  
**Script**  
  
1.  `assessment-report-folder:` Especifica la carpeta donde el informe de evaluación puede almacenarse. (opcional) (atributo)  
  
2.  `object-name:` Especifica los objetos que tienen en cuenta para la generación de informes de evaluación (puede tener nombres de objeto individuales o un nombre de objeto de grupo).  
  
3.  `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
4.  `assessment-report-overwrite:` Especifica si se debe sobrescribir la carpeta de informes de evaluación si ya existe.  
  
    **Valor predeterminado:** false. (opcional) (atributo)  
  
5.  `write-summary-report-to:` Especifica la ruta de acceso donde se generará el informe de resumen.  
  
    Si solo se menciona la ruta de acceso de carpeta, archivo, a continuación, por nombre **AssessmentReport&lt;n&gt;. XML** se crea. (opcional) (atributo)  
  
    Creación de informes tiene dos categorías secundarias adicionales:  
  
    -   `report-errors` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
    -   `verbose` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
**Ejemplo de sintaxis:**  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
o bien  
  
```xml  
<generate-assessment-report  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
>  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration--script-file-commands"></a>Comandos del archivo de Script de migración  
Los comandos de migración convertir el esquema de base de datos de destino en el esquema de origen y migra los datos al servidor de destino.  
  
La salida de consola predeterminada para los comandos de migración es informe de salida 'Total' con ningún informe de error detallado: resumen sólo en el nodo de raíz del árbol de objeto de origen.  
  
**Command**  
  
convertir esquema  
  
1.  Realiza la conversión de esquema de origen al esquema de destino.  
  
2.  Si no se realiza la conexión de base de datos de origen o de destino antes de ejecutar este comando o se produce un error en la conexión con el servidor de base de datos de origen o de destino durante la ejecución del comando, se genera un error y se cierra la aplicación de consola.  
  
**Script**  
  
1.  `conversion-report-folder:` Especifica la carpeta donde el informe de evaluación puede almacenarse. (opcional) (atributo)  
  
2.  `object-name:` Especifica los objetos que tienen en cuenta para convertir un esquema (puede tener nombres de objeto de indivdual o un nombre de objeto de grupo).  
  
3.  `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
4.  `conversion-report-overwrite:` Especifica si se debe sobrescribir la carpeta de informes de evaluación si ya existe.  
  
    **Valor predeterminado:** false. (opcional) (atributo)  
  
5.  `write-summary-report-to:` Especifica la ruta de acceso donde se generará el informe de resumen.  
  
    Si solo se menciona la ruta de acceso de carpeta, archivo, a continuación, por nombre **SchemaConversionReport&lt;n&gt;. XML** se crea. (opcional) (atributo)  
  
    Creación de informes de resumen tiene dos categorías secundarias adicionales:  
  
    -   `report-errors` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
    -   `verbose` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
**Ejemplo de sintaxis:**  
  
```xml  
<convert-schema  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
o bien  
  
```xml  
<convert-schema  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
      <metabase-object object-name="<object-names>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Command**  
  
migrar datos  
  
1.  Migra los datos de origen al destino.  
  
**Script**  
  
1.  `object-name:` Especifica los objetos de origen que se tienen en cuenta para migrar datos (puede tener nombres de objeto de indivdual o un nombre de objeto de grupo).  
  
2.  `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
3.  `write-summary-report-to:` Especifica la ruta de acceso donde se generará el informe de resumen.  
  
    Si solo se menciona la ruta de acceso de carpeta, archivo, a continuación, por nombre **DataMigrationReport&lt;n&gt;. XML** se crea. (opcional) (atributo)  
  
    Creación de informes tiene dos categorías secundarias adicionales:  
  
    -   `report-errors` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
    -   `verbose` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
**Ejemplo de sintaxis:**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>”  
  
   report-errors="true" verbose="true">  
  
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
  
   write-summary-report-to="<file-name/folder-name>”  
  
   report-errors="true" verbose="true"/>  
```  
  
## <a name="migration-preparation-script-file-command"></a>Comando de archivo de secuencia de comandos de preparación de la migración  
El comando de preparación de la migración inicia la asignación de esquema entre las bases de datos de origen y de destino.  
  
**Command**  
  
esquema de asignación  
  
Asignación de esquema de base de datos de origen al esquema de destino.  
  
**Script**  
  
1.  `source-schema` Especifica el esquema de origen que se va a migrar.  
  
2.  `sql-server-schema` Especifica el esquema de destino donde los deseamos que desea migrar.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>Comandos del archivo de Script de facilidad de uso  
Los comandos de facilidad de uso ayudan a sincronizar los objetos de base de datos de destino con la base de datos de origen.  
  
> [!NOTE]  
> La salida de consola predeterminada para los comandos de migración es informe de salida 'Total' con ningún informe de error detallado: resumen sólo en el nodo de raíz del árbol de objeto de origen.  
  
**Command**  
  
destino sincronizar  
  
1.  Los objetos de destino se sincroniza con la base de datos de destino.  
  
2.  Si este comando se ejecuta en la base de datos de origen, se produce un error.  
  
3.  Si no se realiza la conexión de base de datos de destino antes de ejecutar este comando o se produce un error en la conexión con el servidor de base de datos de destino durante la ejecución del comando, se genera un error y se cierra la aplicación de consola.  
  
**Script**  
  
1.  `object-name:` Especifica los objetos que se consideran para la sincronización con la base de datos de destino (puede tener nombres de objeto de indivdual o un nombre de objeto de grupo).  
  
2.  `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
3.  `on-error:` Especifica si se debe especificar los errores de sincronización como advertencias o errores. Opciones disponibles en el error:  
  
    -   total de informes como advertencia  
  
    -   informes-each-como-advertencia  
  
    -   Error-script  
  
4.  `report-errors-to:` Especifica la ubicación del informe de errores para la operación de sincronización (atributo opcional) si solo se proporciona la ruta de acceso de carpeta, a continuación, de archivos por nombre **TargetSynchronizationReport.XML** se crea.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name>"   (optional)  
  
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
**Command**  
  
actualización de base de datos  
  
1.  Actualiza los objetos de origen de base de datos.  
  
2.  Si este comando se ejecuta en la base de datos de destino, se genera un error.  
  
**Script**  
  
1.  `object-name:` Especifica los objetos de origen que se consideran para actualizar desde la base de datos de origen (puede tener nombres de objeto de indivdual o un nombre de objeto de grupo).  
  
2.  `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
3.  `on-error:` Especifica si se debe especificar los errores de sincronización como advertencias o errores. Opciones disponibles en el error:  
  
    -   total de informes como advertencia  
  
    -   informes-each-como-advertencia  
  
    -   Error-script  
  
4.  `report-errors-to:` Especifica la ubicación del informe de errores para la operación de sincronización (atributo opcional) si solo se proporciona la ruta de acceso de carpeta, a continuación, de archivos por nombre **SourceDBRefreshReport.XML** se crea.  
  
Requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name>"   (optional)  
  
/>  
```  
o bien  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
o bien  
  
```xml  
<refresh-from-database>  
  
   <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>Comandos del archivo de Script de generación de script  
Los comandos de generación de Script realizan dos tareas: ayudan a guardar la salida en un archivo de script, en la consola y registre la salida de T-SQL en la consola o un archivo basado en el parámetro especificado.  
  
**Command**  
  
Guardar como secuencia de comandos  
  
Usado para guardar las secuencias de comandos de los objetos en un archivo que se ha mencionado cuando metabase = destino, ésta es una alternativa al comando de sincronización que se obtendrá las secuencias de comandos y ejecutar la misma base de datos de destino.  
  
**Script**  
  
Requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
1.  `object-name:` Especifica los objetos cuyos scripts son se guarden. (Puede tener nombres de objeto de indivdual o un nombre de objeto de grupo)  
  
2.  `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
3.  `metabase:` Especifica si es el origen o destino de la metabase.  
  
4.  `destination:` Especifica la ruta de acceso o la carpeta donde la secuencia de comandos debe guardarse, si el nombre de archivo no se proporciona, a continuación, un nombre de archivo en el formato (valor del atributo object_name) .out  
  
5.  `overwrite:` Si es true, a continuación, sobrescribe si existe el mismo nombre de archivo. Puede tener los valores (verdadero/falso).  
  
**Ejemplo de sintaxis:**  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   destination="<file-name/folder-name>”  
  
   overwrite="<true/false>"   (optional)  
  
/>  
```  
o bien  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file-name/folder-name>”  
  
      <metabase-object object-name="<object-name>"  
  
            object-type="<object-category>"/>  
  
</save-as-script>  
```  
**Command**  
  
instrucción de sql Convert  
  
1.  `context` Especifica el nombre del esquema.  
  
2.  `destination` Especifica si la salida debe almacenarse en un archivo.  
  
    Si no se especifica este atributo, la instrucción de T-SQL convertida se muestra en la consola. (opcional) (atributo)  
  
3.  `conversion-report-folder` Especifica la carpeta donde el informe de evaluación puede almacenarse. (opcional) (atributo)  
  
4.  `conversion-report-overwrite` Especifica si se debe sobrescribir la carpeta de informes de evaluación si ya existe.  
  
    **Valor predeterminado:** false. (opcional) (atributo)  
  
5.  `write-converted-sql-to` Especifica la ruta de acceso de carpeta donde se almacenará el T-SQL convertido de archivo (o). Cuando se especifica una ruta de acceso de carpeta junto con el `sql-files` atributo, cada archivo de código fuente tendrá un archivo de código T-SQL creado en la carpeta especificada de destino correspondiente. Cuando se especifica una ruta de acceso de carpeta junto con el `sql` atributo, el T-SQL convertido se escribe en un archivo denominado Result.out en la carpeta especificada.  
  
6.  `sql` Especifica las instrucciones de sql de MySQL que puede convertir una o varias instrucciones separadas pueden utilizar un ";"  
  
7.  `sql-files` Especifica la ruta de acceso de los archivos de sql que se tiene que convertir a código de T-SQL.  
  
8.  `write-summary-report-to` Especifica la ruta de acceso donde se generará el informe de resumen. Si solo se menciona la ruta de acceso de carpeta, archivo, a continuación, por nombre **ConvertSQLReport.XML** se crea. (opcional) (atributo)  
  
    Informe de creación tiene 2 más subcategorías, especialmente..,:  
  
    -   informe de errores (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales)).  
  
    -   verbose (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales)).  
  
**Script**  
  
Requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
**Ejemplo de sintaxis:**  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="stdout/file"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql="SELECT 1 FROM DUAL;">  
  
      <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
o bien  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="<stdout/file>"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql-files="<folder-name>\*.sql"  
  
/>  
```  
o bien  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-step"></a>Paso siguiente  
Para obtener información sobre las opciones de línea de comandos, consulte [opciones de línea de comandos en la consola de SSMA &#40;MySQLToSQL&#41; ](../../ssma/mysql/command-line-options-in-ssma-console-mysqltosql.md) .  
  
Para obtener más información sobre los archivos de secuencia de comandos de consola de ejemplo, vea [trabajar con los archivos de comandos de consola de ejemplo &#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-the-sample-console-script-files-mysqltosql.md)  
  
El paso siguiente depende de los requisitos del proyecto:  
  
1.  Para especificar una contraseña o la exportación / importación de contraseñas, vea [administrar contraseñas &#40;MySQLToSQL&#41;](../../ssma/mysql/managing-passwords-mysqltosql.md).  
  
2.  Para generar informes, consulte [generar informes &#40;MySQLToSQL&#41;](../../ssma/mysql/generating-reports-mysqltosql.md).  
  
3.  Para solucionar problemas en la consola, consulte [solución de problemas &#40;MySQLToSQL&#41;](../../ssma/mysql/troubleshooting-mysqltosql.md).  
  
