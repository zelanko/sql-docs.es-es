---
title: Ejecución de la consola SSMA (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aa1bf665-8dc0-4259-b36f-46ae67197a43
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 97425a6795889f72b329280ff70f9638378e7799
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006570"
---
# <a name="executing-the-ssma-console-accesstosql"></a>Ejecución de la consola SSMA (AccessToSQL)
Microsoft le proporciona un sólido conjunto de comandos del archivo de secuencia de comandos y opciones de línea de comandos para ejecutar y controlar las actividades SSMA. Las secciones que detallan la misma.  
  
## <a name="project--script-file-commands"></a>Comandos de archivo de Script de proyecto  
Los comandos de proyecto controlan la creación de proyectos, abrir, guardar y salir de proyectos.  
  
**Command**  
  
create-new-project: Crea un nuevo proyecto SSMA.  
  
**Script**  
  
-   `project-folder` indica la carpeta del proyecto que se crean.  
  
-   `project-name` indica el nombre del proyecto. {string}  
  
-   `overwrite-if-exists`Atributo opcional indica si se debe sobrescribir un proyecto existente. {boolean}  
  
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
  
  project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>"  
  
/>  
```  
Es el atributo 'sobrescribir-if-exists' **false** de forma predeterminada.  
  
Atributo de tipo de proyecto es **sql-server-2008** de forma predeterminada.  
  
**Command**  
  
open-project: Abre un proyecto existente.  
  
**Script**  
  
-   `project-folder` indica la carpeta del proyecto que se crean. El comando produce un error si la carpeta especificada no existe.  {string}  
  
-   `project-name` indica el nombre del proyecto. El comando produce un error si el proyecto especificado no existe.  {string}  
  
**Ejemplo de sintaxis:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
**Nota:** Aplicación de consola de SSMA para Access admite compatibilidad con versiones anteriores. Podrá abrir proyectos creados con una versión anterior de SSMA.  
  
**Command**  
  
Guardar proyecto: Guarda el proyecto de migración.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<save-project/>  
```  
**Command**  
  
proyecto de cierre: Cierra el proyecto de migración.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<close-project  
  
  if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
Atributo "if-modificado" es opcional, **omitir** de forma predeterminada.  
  
## <a name="database-connection-script-file-commands"></a>Comandos de archivo de Script de conexión de base de datos  
Los comandos de conexión de base de datos ayudan a conectar a la base de datos.  
  
El **examinar** no se admite la característica de la interfaz de usuario en la consola.  
  
El **autenticación de windows** y **puerto** parámetros no son aplicables al conectarse a SQL Azure.  
  
Para obtener más información en "Crear archivos de Script", consulte [crear archivos de Script &#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md).  
  
**Command**  
  
datos de origen conectarse  
  
-   Realiza la conexión a la base de datos de origen y carga los metadatos de nivel alto de la base de datos de origen, pero no todos los metadatos.  
  
-   Si no se puede establecer la conexión al origen, se genera un error y la aplicación de consola detiene la ejecución  
  
**Script**  
  
Definición de servidor se recupera el atributo de nombre definido para cada conexión en la sección servidor de archivo de conexión de servidor o el archivo de script.  
  
**Ejemplo de sintaxis:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
carga-access-database: Utilizado para cargar archivos de base de datos de access  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<load-access-database  database-file="<Access-database>"/>  
```  
o Administrador de configuración de  
  
```xml  
<load-access-database>  
  
  <access-database database-file="<Access-database1>"/>  
  
  <access-database database-file="<Access-database2>"/>  
  
</load-access-database>  
```  
**Command**  
  
Force-load-origen/destino-database  
  
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
o Administrador de configuración de  
  
```xml  
<force-load>  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Command**  
  
datos de origen volver a conectar  
  
-   Vuelve a conectarse a la base de datos de origen pero no carga los metadatos a diferencia del comando de base de datos connect-origen.  
  
-   Si no puede establecerse (la conexión con el origen re), se genera un error y la aplicación de consola detiene la ejecución.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Command**  
  
base de destino conectarse  
  
-   Se conecta a la base de datos de SQL Server o SQL Azure de destino y carga los metadatos de nivel alto de la base de datos de destino pero no los metadatos por completo.  
  
-   Si no se puede establecer la conexión con el destino, se genera un error y la aplicación de consola detiene la ejecución.  
  
**Script**  
  
Definición de servidor se recupera desde el atributo de nombre definido para cada conexión en la sección servidor de archivo de conexión de servidor o el archivo de script  
  
**Ejemplo de sintaxis:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Command**  
  
base de destino vuelva a conectar  
  
-   Vuelve a conectarse a la base de datos de destino pero no carga los metadatos, a diferencia del comando de base de destino de connect.  
  
-   Si no puede establecerse (re) de la conexión con el destino, se genera un error y la aplicación de consola detiene la ejecución.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>Comandos de archivo de Script de informe  
Los comandos de informe generan informes sobre el rendimiento de diversas actividades de la consola SSMA.  
  
**Command**  
  
informe de evaluación generar  
  
-   Genera informes de evaluación de la base de datos de origen.  
  
-   Si no se realiza la conexión de base de datos de origen antes de ejecutar este comando, se genera un error y se cierra la aplicación de consola.  
  
-   No se puede conectar al servidor de base de datos de origen durante la ejecución del comando, también produce la finalización de la aplicación de consola.  
  
**Script**  
  
-   `assessment-report-folder:` Especifica la carpeta donde el informe de evaluación puede almacenarse. (atributo opcional)  
  
-   `object-name:` Especifica los objetos que tienen en cuenta para la generación de informes de evaluación (puede tener nombres de objeto de la emisora o un nombre de objeto de grupo).  
  
-   `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `assessment-report-overwrite:` Especifica si se debe sobrescribir la carpeta de informes de evaluación si ya existe.  
  
    **Valor predeterminado:** false. (atributo opcional)  
  
-   `write-summary-report-to:` Especifica la ruta de acceso donde se generará el informe.  
  
    Si solo se menciona la ruta de acceso de carpeta, a continuación, archivos por nombre **AssessmentReport&lt;n&gt;. XML** se crea. (atributo opcional)  
  
    Creación de informes tiene dos categorías adicionales:  
  
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
o Administrador de configuración de  
  
```xml  
<generate-assessment-report  
  
  conversion-report-folder="<folder>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
    <metabase-object object-name="ssma.Procedures"  
  
        object-type="category"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>Comandos de archivo de Script de migración  
Los comandos de migración conversión el esquema de base de datos de destino en el esquema de origen y migra los datos al servidor de destino.  
  
La salida de consola predeterminada para los comandos de migración es el informe de salida 'Full' con ningún informe de error detallado: Resumen solo al nodo raíz del árbol de objeto de origen.  
  
**Command**  
  
convertir esquema  
  
-   Realiza la conversión de esquema de origen al esquema de destino.  
  
-   Si no se realiza la conexión de base de datos de origen o de destino antes de ejecutar este comando o se produce un error en la conexión con el servidor de base de datos de origen o destino durante la ejecución del comando, se genera un error y se cierra la aplicación de consola.  
  
**Script**  
  
-   `conversion-report-folder:` Especifica la carpeta donde se puede almacenar el informe de evaluación. (atributo opcional)  
  
-   `object-name:` Especifica los objetos de origen tienen en cuenta para convertir un esquema (puede tener nombres de objeto de la emisora o un nombre de objeto de grupo).  
  
-   `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `conversion-report-overwrite:` Especifica si se debe sobrescribir la carpeta de informes de evaluación si ya existe.  
  
    **Valor predeterminado:** false. (atributo opcional)  
  
-   `write-summary-report-to:` Especifica la ruta de acceso donde se generará el informe.  
  
    Si solo se menciona la ruta de acceso de carpeta, a continuación, archivos por nombre **SchemaConversionReport&lt;n&gt;. XML** se crea. (atributo opcional)  
  
    Creación de informes tiene dos categorías adicionales:  
  
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
o Administrador de configuración de  
  
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
  
-   `object-name:` Especifica los objetos de origen tienen en cuenta para migrar datos (puede tener nombres de objeto de la emisora o un nombre de objeto de grupo).  
  
-   `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `write-summary-report-to:` Especifica la ruta de acceso donde se generará el informe.  
  
    Si solo se menciona la ruta de acceso de carpeta, a continuación, archivos por nombre **DataMigrationReport&lt;n&gt;. XML** se crea. (atributo opcional)  
  
    Creación de informes tiene dos categorías adicionales:  
  
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
o Administrador de configuración de  
  
```xml  
<migrate-data  
  
  object-name="ssma.Tables"  
  
  object-type="category"  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true"/>  
```  
**Command**  
  
tablas de vínculos: Este comando vincula la tabla de origen (acceso) a la tabla de destino.  
  
**Script**  
  
**Ejemplo de sintaxis:**  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</link-tables>  
```  
o Administrador de configuración de  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</link-tables>  
```  
**Command**  
  
Desvincular: tablas: Este comando desvincula la tabla de origen (acceso) de la tabla de destino.  
  
**Script**  
  
**Ejemplos de sintaxis:**  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</unlink-tables>  
```  
o Administrador de configuración de  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</unlink-tables>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>Comandos de archivo de Script de preparación de migración  
El comando de preparación de la migración inicia la asignación de esquema entre las bases de datos de origen y de destino.  
  
**Command**  
  
esquema de asignación: Asignación de esquema de base de datos de origen al esquema de destino.  
  
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
  
La salida de consola predeterminada para los comandos de migración es el informe de salida 'Full' con ningún informe de error detallado: Resumen solo al nodo raíz del árbol de objeto de origen.  
  
**Command**  
  
sincronizar de destino  
  
1.  Los objetos de destino se sincroniza con la base de datos de destino.  
  
2.  Si este comando se ejecuta en la base de datos de origen, se produce un error.  
  
3.  Si no se realiza la conexión de base de datos de destino antes de ejecutar este comando o se produce un error en la conexión al servidor de base de datos de destino durante la ejecución del comando, se genera un error y se cierra la aplicación de consola.  
  
**Script**  
  
1.  `object-name:` Especifica los objetos de destino que se consideran para la sincronización con la base de datos de destino (puede tener nombres de objeto de la emisora o un nombre de objeto de grupo).  
  
2.  `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
3.  `on-error:` Especifica si se debe especificar los errores de sincronización como advertencias o errores. Opciones disponibles para en caso de error:  
  
    -   report-total-as-warning  
  
    -   informes-each-como-warning  
  
    -   Error de script  
  
4.  `report-errors-to:` Especifica la ubicación del informe de errores para la operación de sincronización (atributo opcional) si solo se proporciona la ruta de acceso de carpeta, a continuación, archivos por nombre **TargetSynchronizationReport.XML** se crea.  
  
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
o Administrador de configuración de  
  
```xml  
<synchronize-target  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"/>  
```  
o Administrador de configuración de  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="ssma.dbo.TT1"/>  
  
  <metabase-object object-name="ssma.dbo.TT2"/>  
  
  <metabase-object object-name="ssma.dbo.TT3"/>  
  
</synchronize-target>  
```  
**Command**  
  
actualización de base de datos  
  
-   Actualiza los objetos de base de datos de origen.  
  
-   Si este comando se ejecuta en la base de datos de destino, se genera un error.  
  
**Script**  
  
Requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
1.  `object-name:` Especifica los objetos de origen que se consideran para la actualización de base de datos de origen (puede tener nombres de objeto de la emisora o un nombre de objeto de grupo).  
  
2.  `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
3.  `on-error:` Especifica si se debe especificar la actualización de errores como advertencias o errores. Opciones disponibles para en caso de error:  
  
    -   report-total-as-warning  
  
    -   informes-each-como-warning  
  
    -   Error de script  
  
4.  `report-errors-to:` Especifica la ubicación del informe de errores para la operación de actualización (atributo opcional) si solo se proporciona la ruta de acceso de carpeta, a continuación, archivos por nombre **SourceDBRefreshReport.XML** se crea.  
  
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
o Administrador de configuración de  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.Procedures"  
  
  object-type="category"/>  
```  
o Administrador de configuración de  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="ssma.TT_1"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>Comandos de archivo de Script de generación de script  
La generación de Script de comandos ayudan a guardar la salida de consola en un archivo de script.  
  
**Command**  
  
Guardar como secuencia de comandos  
  
Usado para guardar los Scripts de los objetos en un archivo se ha mencionado cuando metabase = destino, esta es una alternativa al comando de sincronización donde en obtener los scripts y ejecutar la misma base de datos de destino.  
  
**Script**  
  
Requiere uno o varios nodos de la metabase como parámetro de línea de comandos.  
  
-   `object-name:` Especifica los objetos cuyas secuencias de comandos son para guardarse. (Puede tener nombres de objeto individuales o un nombre de objeto de grupo)  
  
-   `object-type:` Especifica el tipo del objeto especificado en el atributo de nombre de objeto (si se especifica la categoría de objeto de tipo de objeto será "categoría").  
  
-   `metabase:` Especifica si es el origen o destino de la metabase.  
  
-   `destination:` Especifica la ruta de acceso o la carpeta donde la secuencia de comandos debe guardarse, si el nombre de archivo no se proporciona, a continuación, un nombre de archivo en el .out formato (valor del atributo object_name)  
  
-   `overwrite:` Si es true, a continuación, sobrescribe si existe el mismo nombre de archivo. Puede tener los valores (true/false).  
  
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
o Administrador de configuración de  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file/folder>"  
  
    <metabase-object object-name="ssma.dbo.Procedures"  
  
                     object-type="category"/>  
  
</save-as-script>  
```  
  
## <a name="next-step"></a>Paso siguiente  
Para obtener información sobre las opciones de línea de comandos, consulte [opciones de línea de comandos en la consola SSMA &#40;AccessToSQL&#41; ](../../ssma/access/command-line-options-in-ssma-console-accesstosql.md) .  
  
Para obtener información sobre los archivos de secuencia de comandos de consola de ejemplo, vea [trabajar con el FilesExecuting de secuencia de comandos de consola de ejemplo de la consola de SSMA &#40;AccessToSQL&#41;](../../ssma/access/working-sample-console-script-filesexecuting-ssma-console-accesstosql.md)  
  
El paso siguiente depende de los requisitos del proyecto:  
  
-   Para especificar una contraseña o la exportación / importación de contraseñas, vea [administrar contraseñas &#40;AccessToSQL&#41;](../../ssma/access/managing-passwords-accesstosql.md).  
  
-   Para generar informes, vea [generar informes &#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md).  
  
-   Para solucionar problemas en la consola, consulte [Troubleshooting &#40;AccessToSQL&#41;](../../ssma/access/troubleshooting-accesstosql.md).  
  
