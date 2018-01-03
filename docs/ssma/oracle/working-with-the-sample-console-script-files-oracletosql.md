---
title: Trabajar con los archivos de comandos de consola de ejemplo (OracleToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Sample Console Script Files, ServersConnectionFileSample.xml
- Sample Console Script Files, SqlStatementConversionSample.xml
- Sample Console Script Files,VariableValueFileSample.xml
ms.assetid: c6202dcc-b994-457b-9b2f-0cd89e79792d
caps.latest.revision: "9"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: ed17f63dedb91eb41eea2cc991771daf35af48fc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="working-with-the-sample-console-script-files-oracletosql"></a>Trabajar con los archivos de comandos de consola de ejemplo (OracleToSQL)
Algunos de los archivos de ejemplo se han proporcionado junto con el producto para la referencia de usuario y el uso. Esta sección describe la forma de personalizar fácilmente estos scripts para ajustarse a las necesidades del usuario final.  
  
## <a name="sample-console-script-files"></a>Archivos de secuencia de comandos de consola de ejemplo  
Se han proporcionado los archivos de comandos de consola de ejemplo siguientes que tratan escenarios diferentes para referencia de usuario:  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   **ServersConnectionFileSample.xml:**  
  
    -   Este ejemplo proporciona los diferentes modos de conexión disponible a la base de datos de origen y de destino y el usuario puede seleccionar cualquier modo según el requisito. Este ejemplo contiene las definiciones de servidor.  
  
    -   El usuario puede conectarse a la base de datos requiere cambiando simplemente los valores para el origen necesarios y las definiciones de servidores de destino. En el ejemplo proporcionado todos los valores se han proporcionado valores como variables que están disponibles en la **VariableValueFileSample.xml**.  Todos los demás parámetros de conexión se pueden quitar del archivo de conexión de servidor de trabajo del usuario.  
  
    -   Para obtener más información sobre cómo conectarse al servidor de origen y de destino, vea [crear los archivos de conexión de servidor &#40; OracleToSQL &#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md) .  
  
-   **VariableValueFileSample.xml:** archivos de script de todas las variables que se han usado en la consola de ejemplo y `ServersConnectionFileSample.xml` han se intercalan en este archivo. Para ejecutar las secuencias de comandos de consola de ejemplo que tiene el usuario simplemente reemplazar la variable de ejemplo valores con el usuario los define y pasan este archivo como un argumento de línea de comandos adicionales junto con el archivo de script.  
  
    Para obtener más información sobre el archivo de valores de variables, consulte [crear archivos de valores Variable &#40; OracleToSQL &#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md).  
  
-   **AssessmentReportGenerationSample.xml:** este ejemplo permite al usuario generar un informe de evaluación de xml que se puede usar por el usuario para el análisis antes de que empiece a convertir y migrar los datos.  
  
    En el `generate-assessment-report` el usuario debe cambiar obligatoriamente el valor de la variable de comandos (consulte **VariableValueFileSample.xml**) en el `object-name` de atributo para el nombre de base de datos está en uso por el usuario. Según el tipo de objeto especificado, la `object-type` valor también deba cambiarse.  
  
    Si el usuario tiene que evaluar varios objetos / bases de datos puede especificar varios `metabase-object` nodos como se muestra en el `generate-assessment-report` de ejemplo 4 del comando del archivo de comandos de consola de ejemplo.  
  
    Para obtener más información sobre la generación de informes, consulte [generar informes &#40; OracleToSQL &#41;](../../ssma/oracle/generating-reports-oracletosql.md).  
  
    > [!NOTE]  
    > -   Asegúrese de que el argumento de línea de comandos del archivo de valor de la variable se pasa a la aplicación de consola y VariableValueFileSample.xml se actualiza con el usuario especificado valores.  
    > -   Asegúrese de que el argumento de línea de comandos de archivo de conexión de servidor se pasa a la aplicación de consola y el ServersConnectionFileSample.xml se actualiza con los valores de parámetro de servidor correcto.  
  
-   **SqlStatementConversionSample.xml:**  
    Este ejemplo permite al usuario generar la correspondiente `t-sql` secuencia de comandos para la base de datos de origen `sql` comando proporcionado como entrada.  
  
    En el `convert-sql-statement` el usuario debe cambiar obligatoriamente el valor de la variable de comandos (consulte **VariableValueFileSample.xml**) en el `context` de atributo con el nombre de base de datos que se está en uso por el usuario. El usuario también deberán cambiar la `sql` valor del atributo a la base de datos de origen `sql` comandos requeridos por éste va a convertir.  
  
    El usuario también puede proporcionar los archivos de sql que se va a convertir. Esto se han mostrado en el `convert-sql-statement` de ejemplo 4 del comando del archivo de comandos de consola de ejemplo.  
  
    > [!NOTE]  
    > Asegúrese de que el argumento de línea de comandos del archivo de valor de la variable se pasa a la aplicación de consola y VariableValueFileSample.xml se actualiza con el usuario especificado valores.  
  
-   **ConversionAndDataMigrationSample.xml:**  
     Este ejemplo permite al usuario realizar una migración de extremo a extremo de la conversión a la migración de datos. La lista de valores de atributo obligatorio que será necesario cambiar se menciona a continuación:  
  
    **Nombre de comando**  
  
    `map-schema`  
  
    Asignación de esquema de base de datos de origen al esquema de destino.  
  
    **Atributo**  
  
    -   `source-schema:`Especifica la base de datos de origen que requiere que para se va a convertir.  
  
    -   `sql-server-schema`: Especifica la base de datos de destino que se pueden migrar a  
  
    **Nombre de comando**  
  
    `convert-schema`  
  
    -   Realiza la conversión de esquema de origen al esquema de destino.  
  
    -   Si el usuario tiene que evaluar varios objetos / bases de datos puede especificar varios `metabase-object` nodos como se muestra en el `convert-schema` de ejemplo 4 del comando del archivo de comandos de consola de ejemplo.  
  
    **Atributo**  
  
    `object-name`: Especifique la base de datos de origen / objeto nombre que requiere que para se va a convertir. Asegúrese de que la correspondiente `object-type` se cambia en función del tipo de objeto que se especifica en el`object-name`  
  
    **Nombre de comando**  
  
    `synchronize-target`  
  
    -   Los objetos de destino se sincroniza con la base de datos de destino.  
  
    -   Si el usuario tiene que evaluar varios objetos / bases de datos puede especificar varios `metabase-object` nodos como se muestra en el `synchronize-target` de ejemplo 3 del comando del archivo de comandos de consola de ejemplo.  
  
    **Atributo**  
  
    `object-name:`Especifique la base de datos de sql server / objeto nombre que requiere para crearse. Asegúrese de que la correspondiente `object-type` se cambia en función del tipo de objeto que se especifica en el`object-name`  
  
    **Nombre de comando**  
  
    `migrate-data`  
  
    -   Migra los datos de origen al destino.  
  
    -   Si el usuario tiene que evaluar varios objetos / bases de datos puede especificar varios `metabase-object` nodos como se muestra en el `migrate-data` de ejemplo 2 del comando del archivo de comandos de consola de ejemplo.  
  
    **Atributo**  
  
    `object-name:`Especifica la base de datos de origen / tablas nombre que requiere para la migración. Asegúrese de que la correspondiente `object-type` se cambia en función del tipo de objeto que se especifica en el`object-name`  
  
## <a name="see-also"></a>Vea también  
[Crear archivos de valor de la Variable &#40; OracleToSQL &#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
[Crear los archivos de conexión de servidor &#40; OracleToSQL &#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
[Generación de informes &#40; OracleToSQL &#41;](../../ssma/oracle/generating-reports-oracletosql.md)  
  
