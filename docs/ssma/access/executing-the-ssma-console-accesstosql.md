---
title: Ejecutar la consola SSMA (AccessToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: aa1bf665-8dc0-4259-b36f-46ae67197a43
caps.latest.revision: 25
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4400ab959c61b23c3a98c817c03506631a4d61af
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="executing-the-ssma-console-accesstosql"></a>Ejecutar la consola SSMA (AccessToSQL)
Microsoft le ofrece un potente conjunto de comandos del archivo de secuencia de comandos y opciones de línea de comandos para ejecutar y controlar las actividades SSMA. Las secciones posteriores detallan los mismos.  
  
## <a name="project--script-file-commands"></a>Comandos del archivo de Script de proyecto  
Los comandos de proyectos controlan la creación de proyectos, abrir, guardar y salir de proyectos.  
  
**Command**  
  
Crear nueva-proyectos: crea un nuevo proyecto SSMA.  
  
**Script**  
  
-   `project-folder` indica la carpeta del proyecto obtener creado.  
  
-   `project-name` indica el nombre del proyecto. {string}  
  
-   `overwrite-if-exists`Atributo opcional indica si se debe sobrescribir un proyecto existente. {valor} booleano  
  
-   `project-type` es un atributo opcional.  Las siguientes opciones están disponibles para el tipo de proyecto:  
  
    -   sql-server-2005  
  
    -   sql-server-2008  
  
    -   sql-server-2012  
  
    -   sql-server-2014  
  
    -   sql-server-2016  
  
    -   sql-azure  
  
    Valor predeterminado es "sql-server-2008".  
  
**Ejemplo:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>"  
  
  project-type=”<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>”  
  
/>  
```  
Es el atributo 'sobrescribir-if-exists' **false** de forma predeterminada.  
  
El atributo 'tipo de proyecto' es **sql-server-2008** de forma predeterminada.  
  
**Command**  
  
proyecto de abrir: abre un proyecto existente.  
  
**Script**  
  
-   `project-folder` indica la carpeta del proyecto obtener creado. El comando produce un error si la carpeta especificada no existe.  {string}  
  
-   `project-name` indica el nombre del proyecto. El comando produce un error si el proyecto especificado no existe.  {string}  
  
**Ejemplo de sintaxis:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
**Nota:** aplicación de consola de SSMA para Access admite compatibilidad con versiones anteriores. Podrá abrir proyectos creados con una versión anterior de SSMA.  
  
**Command**  
  
Guardar proyecto: guarda el proyecto de migración.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<save-project/>  
```  
**Command**  
  
proyecto de cerrar: cierra el proyecto de migración.  
  
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
  
El **examinar** no se admite la característica de la interfaz de usuario en la consola.  
  
El **autenticación de windows** y **puerto** parámetros no son aplicables al conectarse a SQL Azure.  
  
Para obtener más información sobre 'Crear archivos de Script', vea [crear archivos de Script &#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md).  
  
**Command**  
  
connect-source-database  
  
-   Realiza la conexión a la base de datos de origen y carga los metadatos de nivel alto de la base de datos de origen, pero no todos los metadatos.  
  
-   Si no se puede establecer la conexión con el origen, se genera un error y la aplicación de consola detiene la ejecución  
  
**Script**  
  
Definición de servidor se recupera desde el atributo de nombre definido para cada conexión en la sección servidor del archivo de conexión de servidor o el archivo de script.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
acceso de carga-bases de datos: usados para cargar archivos de base de datos de access  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<load-access-database  database-file="<Access-database>"/>  
```  
o bien  
  
```xml  
<load-access-database>  
  
  <access-database database-file="<Access-database1>"/>  
  
  <access-database database-file="<Access-database2>"/>  
  
</load-access-database>  
```  
**Command**  
  
force-load-source/target-database  
  
-   Carga los metadatos de origen.  
  
-   Resulta útil para trabajar en el proyecto de migración sin conexión.  
  
-   Si no se puede establecer la conexión con el origen o destino, se genera un error y la aplicación de consola detiene la ejecución  
  
**Script**  
  
Requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<force-load  
  
  object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
o bien  
  
```xml  
<force-load>  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Command**  
  
reconnect-source-database  
  
-   Vuelve a conectarse a la base de datos de origen pero no carga los metadatos a diferencia del comando de datos de origen de conexión.  
  
-   Si no se puede establecer el volver a conectar con el origen, se genera un error y la aplicación de consola detiene la ejecución.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
connect-target-database  
  
-   Se conecta a la base de datos de SQL Server o SQL Azure de destino y carga los metadatos de nivel alto de la base de datos de destino pero no los metadatos por completo.  
  
-   Si no se puede establecer la conexión con el destino, se genera un error y la aplicación de consola detiene la ejecución.  
  
**Script**  
  
Definición de servidor se recupera desde el atributo de nombre definido para cada conexión en la sección servidor del archivo de conexión de servidor o el archivo de script  
  
**Ejemplo de sintaxis:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Command**  
  
reconnect-target-database  
  
-   Vuelve a conectarse a la base de datos de destino pero no carga los metadatos, a diferencia del comando de conexión de datos de destino.  
  
-   Si la (conexión con el destino re) no se puede establecer, se genera un error y la aplicación de consola detiene la ejecución.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>Comandos del archivo de Script de informe  
Los comandos de informes generan informes sobre el rendimiento de diversas actividades de consola SSMA.  
  
**Command**  
  
generate-assessment-report  
  
-   Genera informes de evaluación de la base de datos de origen.  
  
-   Si no se realiza la conexión de base de datos de origen antes de ejecutar este comando, se genera un error y se cierra la aplicación de consola.  
  
-   No se pudo conectar al servidor de base de datos de origen durante la ejecución del comando, también se produce en terminar la aplicación de consola.  
  
**Script**  
  
-   `assessment-report-folder:` Especifica la carpeta donde el informe de evaluación puede almacenarse. (opcional) (atributo)  
  
-   `object-name:` Especifica los objetos que tienen en cuenta para la generación de informes de evaluación (puede tener nombres de objeto de indivdual o un nombre de objeto de grupo).  
  
-   `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `assessment-report-overwrite:` Especifica si se debe sobrescribir la carpeta de informes de evaluación si ya existe.  
  
    **Valor predeterminado:** false. (opcional) (atributo)  
  
-   `write-summary-report-to:` Especifica la ruta de acceso donde se generará el informe.  
  
    Si solo se menciona la ruta de acceso de carpeta, archivo, a continuación, por nombre **AssessmentReport&lt;n&gt;. XML** se crea. (opcional) (atributo)  
  
    Creación de informes tiene dos categorías secundarias adicionales:  
  
    -   `report-errors` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
    -   `verbose` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
**Ejemplo de sintaxis:**  
  
```xml  
<generate-assessment-report  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  
  write-summary-report-to="<file>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  conversion-report-folder="<folder>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
o bien  
  
```xml  
<generate-assessment-report  
  
  conversion-report-folder="<folder>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
    <metabase-object object-name="ssma.Procedures"  
  
        object-type="category"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>Comandos del archivo de Script de migración  
Los comandos de migración convertir el esquema de base de datos de destino en el esquema de origen y migra los datos al servidor de destino.  
  
La salida de consola predeterminada para los comandos de migración es informe de salida 'Total' con ningún informe de error detallado: resumen sólo en el nodo de raíz del árbol de objeto de origen.  
  
**Command**  
  
convert-schema  
  
-   Realiza la conversión de esquema de origen al esquema de destino.  
  
-   Si no se realiza la conexión de base de datos de origen o de destino antes de ejecutar este comando o se produce un error en la conexión con el servidor de base de datos de origen o de destino durante la ejecución del comando, se genera un error y se cierra la aplicación de consola.  
  
**Script**  
  
-   `conversion-report-folder:` Especifica la carpeta donde se puede almacenar el informe de evaluación. (opcional) (atributo)  
  
-   `object-name:` Especifica los objetos de origen que se consideran para la conversión de esquema (puede tener nombres de objeto de indivdual o un nombre de objeto de grupo).  
  
-   `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `conversion-report-overwrite:` Especifica si se debe sobrescribir la carpeta de informes de evaluación si ya existe.  
  
    **Valor predeterminado:** false. (opcional) (atributo)  
  
-   `write-summary-report-to:` Especifica la ruta de acceso donde se generará el informe.  
  
    Si solo se menciona la ruta de acceso de carpeta, archivo, a continuación, por nombre **SchemaConversionReport&lt;n&gt;. XML** se crea. (opcional) (atributo)  
  
    Creación de informes tiene dos categorías secundarias adicionales:  
  
    -   `report-errors` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
    -   `verbose` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
**Ejemplo de sintaxis:**  
  
```xml  
<convert-schema  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  write-summary-report-to="<filepath/folder>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
o bien  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder>"         (optional)  
  
  conversion-report-overwrite="<true/false>"  (optional)  
  
  <metabase-object object-name="ssma.Procedures"  
  
    object-type="category"/>  
  
</convert-schema>  
```  
**Command**  
  
migrar datos  
  
1.  Migra los datos de origen al destino.  
  
**Script**  
  
-   `object-name:` Especifica los objetos de origen que se tienen en cuenta para migrar datos (puede tener nombres de objeto de indivdual o un nombre de objeto de grupo).  
  
-   `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `write-summary-report-to:` Especifica la ruta de acceso donde se generará el informe.  
  
    Si solo se menciona la ruta de acceso de carpeta, archivo, a continuación, por nombre **DataMigrationReport&lt;n&gt;. XML** se crea. (opcional) (atributo)  
  
    Creación de informes tiene dos categorías secundarias adicionales:  
  
    -   `report-errors` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
    -   `verbose` (= "true/false", no tiene valor predeterminado como "false" (atributos opcionales))  
  
**Ejemplo de sintaxis:**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true">  
  
    <metabase-object object-name="ssma.TT1"/>  
  
    <metabase-object object-name="ssma.TT2"/>  
  
    <metabase-object object-name="ssma.TT3"/>  
  
    <data-migration-connection  
  
      source-use-last-used="true"/source-server="<server-unique-name>"  
  
      target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
o bien  
  
```xml  
<migrate-data  
  
  object-name="ssma.Tables"  
  
  object-type="category"  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true"/>  
```  
**Command**  
  
Vincular tablas: este comando vincula la tabla de origen (Access) a la tabla de destino.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</link-tables>  
```  
o bien  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</link-tables>  
```  
**Command**  
  
tablas desvincular: este comando desvincula la tabla de origen (acceso) de la tabla de destino.  
  
**Script**  
  
**Ejemplos de sintaxis:**  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</unlink-tables>  
```  
o bien  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</unlink-tables>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>Comandos del archivo de secuencia de comandos de preparación de migración  
El comando de preparación de la migración inicia la asignación de esquema entre las bases de datos de origen y de destino.  
  
**Command**  
  
esquema de asignación: asignación del esquema de base de datos de origen al esquema de destino.  
  
**Script**  
  
-   `source-schema` Especifica el esquema de origen que se va a migrar.  
  
-   `sql-server-schema` Especifica el esquema de destino donde los deseamos que desea migrar.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<map-schema source-schema="source-schema"  
  
            sql-server-schema="target-schema"/>  
```  
  
## <a name="manageability-commands"></a>Comandos de facilidad de uso  
Los comandos de facilidad de uso ayudan a sincronizar los objetos de base de datos de destino con la base de datos de origen.  
  
La salida de consola predeterminada para los comandos de migración es informe de salida 'Total' con ningún informe de error detallado: resumen sólo en el nodo de raíz del árbol de objeto de origen.  
  
**Command**  
  
destino sincronizar  
  
1.  Los objetos de destino se sincroniza con la base de datos de destino.  
  
2.  Si este comando se ejecuta en la base de datos de origen, se produce un error.  
  
3.  Si no se realiza la conexión de base de datos de destino antes de ejecutar este comando o se produce un error en la conexión con el servidor de base de datos de destino durante la ejecución del comando, se genera un error y se cierra la aplicación de consola.  
  
**Script**  
  
1.  `object-name:` Especifica los objetos de destino que se consideran para la sincronización con la base de datos de destino (puede tener nombres de objeto de indivdual o un nombre de objeto de grupo).  
  
2.  `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
3.  `on-error:` Especifica si se debe especificar los errores de sincronización como advertencias o errores. Opciones disponibles en el error:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   Error-script  
  
4.  `report-errors-to:` Especifica la ubicación del informe de errores para la operación de sincronización (atributo opcional) si solo se proporciona la ruta de acceso de carpeta, a continuación, de archivos por nombre **TargetSynchronizationReport.XML** se crea.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<synchronize-target  
  
  object-name="ots_triggers.dbo"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```  
o bien  
  
```xml  
<synchronize-target  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"/>  
```  
o bien  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="ssma.dbo.TT1"/>  
  
  <metabase-object object-name="ssma.dbo.TT2"/>  
  
  <metabase-object object-name="ssma.dbo.TT3"/>  
  
</synchronize-target>  
```  
**Command**  
  
actualización de base de datos  
  
-   Actualiza los objetos de origen de base de datos.  
  
-   Si este comando se ejecuta en la base de datos de destino, se genera un error.  
  
**Script**  
  
Requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
1.  `object-name:` Especifica los objetos de origen que se consideran para actualizar desde la base de datos de origen (puede tener nombres de objeto de indivdual o un nombre de objeto de grupo).  
  
2.  `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
3.  `on-error:` Especifica si se debe especificar la actualización de errores como advertencias o errores. Opciones disponibles en el error:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   Error-script  
  
4.  `report-errors-to:` Especifica la ubicación del informe de errores para la operación de actualización (atributo opcional) si solo se proporciona la ruta de acceso de carpeta, a continuación, de archivos por nombre **SourceDBRefreshReport.XML** se crea.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.TT1"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```  
o bien  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.Procedures"  
  
  object-type="category"/>  
```  
o bien  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="ssma.TT_1"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>Comandos del archivo de Script de generación de script  
La generación del Script comandos ayudan a guardar la salida de la consola en un archivo de script.  
  
**Command**  
  
save-as-script  
  
Usado para guardar las secuencias de comandos de los objetos en un archivo que se ha mencionado cuando metabase = destino, ésta es una alternativa al comando de sincronización que se obtendrá las secuencias de comandos y ejecutar la misma base de datos de destino.  
  
**Script**  
  
Requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
-   `object-name:` Especifica los objetos cuyos scripts son se guarden. (Puede tener nombres de objeto individuales o un nombre de objeto de grupo)  
  
-   `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `metabase:` Especifica si es el origen o destino de la metabase.  
  
-   `destination:` Especifica la ruta de acceso o la carpeta donde la secuencia de comandos debe guardarse, si el nombre de archivo no se proporciona, a continuación, un nombre de archivo en el formato (valor del atributo object_name) .out  
  
-   `overwrite:` Si es true, a continuación, sobrescribe si existe el mismo nombre de archivo. Puede tener los valores (verdadero/falso).  
  
**Ejemplo de sintaxis:**  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"  
  
  destination="<file/folder>"  
  
  overwrite="<true/false>"             (optional)  
  
/>  
```  
o bien  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file/folder>"  
  
    <metabase-object object-name="ssma.dbo.Procedures"  
  
                     object-type="category"/>  
  
</save-as-script>  
```  
  
## <a name="next-step"></a>Paso siguiente  
Para obtener información sobre las opciones de línea de comandos, consulte [opciones de línea de comandos en la consola de SSMA &#40;AccessToSQL&#41; ](../../ssma/access/command-line-options-in-ssma-console-accesstosql.md) .  
  
Para obtener información sobre los archivos de secuencia de comandos de consola de ejemplo, vea [trabajar con el FilesExecuting de secuencia de comandos de consola de ejemplo de la consola SSMA &#40;AccessToSQL&#41;](../../ssma/access/working-sample-console-script-filesexecuting-ssma-console-accesstosql.md)  
  
El paso siguiente depende de los requisitos del proyecto:  
  
-   Para especificar una contraseña o la exportación / importación de contraseñas, vea [administrar contraseñas &#40;AccessToSQL&#41;](../../ssma/access/managing-passwords-accesstosql.md).  
  
-   Para generar informes, consulte [generar informes &#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md).  
  
-   Para solucionar problemas en la consola, consulte [solución de problemas &#40;AccessToSQL&#41;](../../ssma/access/troubleshooting-accesstosql.md).  
  
