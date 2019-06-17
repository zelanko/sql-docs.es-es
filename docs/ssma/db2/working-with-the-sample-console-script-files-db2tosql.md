---
title: Trabajar con los archivos de secuencia de comandos de consola de ejemplo (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5c3080c3-d074-4f99-a5f5-219ebeddc474
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: dc7976fae322dddc24eda7cf6ef84ef20a7a9e61
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63259010"
---
# <a name="working-with-the-sample-console-script-files-db2tosql"></a>Trabajar con los archivos de secuencia de comandos de consola de ejemplo (DB2ToSQL)
Se han proporcionado algunos archivos de ejemplo junto con el producto para la referencia de usuario y el uso. Esta sección describe la manera de personalizar fácilmente estos scripts para satisfacer las necesidades del usuario final.  
  
## <a name="sample-console-script-files"></a>Archivos de secuencia de comandos de consola de ejemplo  
Los siguientes archivos de secuencia de comandos de consola de ejemplo que abarcan distintos escenarios se han proporcionado para la referencia de usuario:  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
1.  **ServersConnectionFileSample.xml:**  
  
    -   Este ejemplo proporciona los diferentes modos de conexión disponible a la base de datos de origen y de destino y el usuario puede seleccionar cualquier modo según los requisitos. Este ejemplo contiene las definiciones de servidor.  
  
    -   El usuario puede conectarse a la base de datos necesario con solo cambiar los valores para el origen necesarios y las definiciones de servidor de destino. En el ejemplo proporcionado se han proporcionado todos los valores de variables como valores que están disponibles en el **VariableValueFileSample.xml**.  Todos los demás parámetros de conexión se pueden quitar del archivo de conexión de servidor de trabajo del usuario.  
  
    -   Para obtener más información acerca de cómo conectarse al servidor de origen y destino, consulte [crear los archivos de conexión de servidor &#40;DB2ToSQL&#41; ](../../ssma/db2/creating-the-server-connection-files-db2tosql.md) .  
  
2.  **VariableValueFileSample.xml:** Archivos de script de todas las variables que se han usado en la consola de ejemplo y `ServersConnectionFileSample.xml` ha sido intercalan en este archivo. Para ejecutar las secuencias de comandos de consola muestra que el usuario tiene que reemplazar simplemente la variable del ejemplo valores con el usuario las definen y pasan este archivo como un argumento de línea de comandos adicionales junto con el archivo de script.  
  
    Para obtener más información sobre el archivo de valores variables, consulte [crear archivos de valor Variable &#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md).  
  
3.  **AssessmentReportGenerationSample.xml:** Este ejemplo permite al usuario generar un informe de evaluación de xml que se puede usar por el usuario para el análisis antes de que empiece a convertir y migrar los datos.  
  
    En el `generate-assessment-report` el usuario debe cambiar obligatoriamente el valor de la variable de comando (consulte **VariableValueFileSample.xml**) en el `object-name` atributo por el nombre de la base de datos está en uso por el usuario. Según el tipo de objeto especificado, el `object-type` valor también debe cambiarse.  
  
    Si el usuario tiene que evaluar varios objetos de bases de datos y puede especificar varios `metabase-object` nodos como se muestra en el `generate-assessment-report` de ejemplo 4 del comando del archivo de script de la consola de ejemplo.  
  
    Para obtener más información sobre la generación de informes, vea [generar informes &#40;DB2ToSQL&#41;](../../ssma/db2/generating-reports-db2tosql.md).  
  
    **Notas:**  
  
    Asegúrese de que el argumento de línea de comandos del archivo de valor de la variable se pasa a la aplicación de consola y VariableValueFileSample.xml se actualiza con el usuario especificado valores.  
  
    Asegúrese de que el argumento de línea de comandos de archivo de conexión de servidor se pasa a la aplicación de consola y el ServersConnectionFileSample.xml se actualiza con los valores de parámetro de servidor correcto.  
  
4.  **SqlStatementConversionSample.xml:** Este ejemplo permite al usuario generar la correspondiente `t-sql` secuencia de comandos de la base de datos de origen `sql` comando proporcionado como entrada.  
  
    En el `convert-sql-statement` el usuario debe cambiar obligatoriamente el valor de la variable de comando (consulte **VariableValueFileSample.xml**) en el `context` de atributo en el nombre de base de datos que se está en uso por el usuario. También le pedirá al usuario cambiar la `sql` valor del atributo a la base de datos de origen `sql` comando que requieren que para se va a convertir.  
  
    El usuario también puede proporcionar los archivos de sql que se va a convertir. Esto se ha mostrado en el `convert-sql-statement` de ejemplo 4 del comando del archivo de script de la consola de ejemplo.  
  
    > [!NOTE]  
    > Asegúrese de que el argumento de línea de comandos del archivo de valor de la variable se pasa a la aplicación de consola y VariableValueFileSample.xml se actualiza con el usuario especificado valores.  
  
5.  **ConversionAndDataMigrationSample.xml:** Este ejemplo permite al usuario realizar una migración de extremo a extremo de la conversión a la migración de datos. A continuación se enumera la lista de valores de atributo obligatorio que tendrán que cambiar:  
  
    |Nombre de comando|Descripción|Attribute|  
    |----------------|---------------|-------------|  
    |`map-schema`|Asignación de esquema de base de datos de origen al esquema de destino.|`source-schema:` Especifica la base de datos de origen que requiere que para se va a convertir.<br /><br />`sql-server-schema`: Especifica la base de datos de destino que se pueden migrar a|  
    |`convert-schema`|Realiza la conversión de esquema de origen al esquema de destino.<br /><br />Si el usuario tiene que evaluar varios objetos de bases de datos y puede especificar varios `metabase-object` nodos como se muestra en el `convert-schema` de ejemplo 4 del comando del archivo de script de la consola de ejemplo.|`object-name`: Especificar la base de datos de origen / objeto de nombre que requiere que para se va a convertir. Asegúrese de que el correspondiente `object-type` se cambia en función del tipo de objeto que se especifica en el `object-name`|  
    |`synchronize-target`|Los objetos de destino se sincroniza con la base de datos de destino.<br /><br />Si el usuario tiene que evaluar varios objetos de bases de datos y puede especificar varios `metabase-object` nodos como se muestra en el `synchronize-target` 3 de ejemplo del comando del archivo de script de la consola de ejemplo.|`object-name:` Especificar la base de datos de sql server / objeto de nombre que requiere que para se va a crear. Asegúrese de que el correspondiente `object-type` se cambia en función del tipo de objeto que se especifica en el `object-name`|  
    |`migrate-data`|Migra los datos de origen al destino.<br /><br />Si el usuario tiene que evaluar varios objetos de bases de datos y puede especificar varios `metabase-object` nodos como se muestra en el `migrate-data` de ejemplo 2 del comando del archivo de script de la consola de ejemplo.|`object-name:` Especifica la base de datos de origen / tables nombre que requiere para la migración. Asegúrese de que el correspondiente `object-type` se cambia en función del tipo de objeto que se especifica en el `object-name`|  
  
## <a name="see-also"></a>Vea también  
[Creación de archivos de valor Variable &#40;DB2ToSQL&#41;](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
[Creación de los archivos de conexión de servidor &#40;DB2ToSQL&#41;](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
[Generación de informes &#40;DB2ToSQL&#41;](../../ssma/db2/generating-reports-db2tosql.md)  
  
