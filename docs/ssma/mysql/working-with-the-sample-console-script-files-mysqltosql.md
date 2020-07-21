---
title: Trabajar con los archivos de script de la consola de ejemplo (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sample console script files
ms.assetid: 7e6aaa8a-5f5c-414d-9fb8-21e56b9ffaef
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6dacba33ecbaa7bdeb51d0a31438c3cbdb21969f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67904896"
---
# <a name="working-with-the-sample-console-script-files-mysqltosql"></a>Trabajar con los archivos de script de la consola de ejemplo (MySQLToSQL)
Se han proporcionado algunos archivos de ejemplo junto con el producto para la referencia de usuario y el uso. En esta sección se describe la manera de personalizar fácilmente estos scripts para ajustarse a las necesidades del usuario final.  
  
## <a name="sample-console-script-files"></a>Archivos de script de la consola de ejemplo  
Se han proporcionado los siguientes archivos de script de la consola de ejemplo que abarcan distintos escenarios para la referencia del usuario:  
  
-   ServersConnectionFileSample. XML  
  
-   VariableValueFileSample. XML  
  
-   AssessmentReportGenerationSample. XML  
  
-   SqlStatementConversionSample. XML  
  
-   ConversionAndDataMigrationSample. XML  
  
-   **ServersConnectionFileSample. xml:**  
  
    -   Este ejemplo proporciona los diferentes modos de conexión disponibles para la base de datos de origen y de destino, y el usuario puede seleccionar cualquier modo según el requisito. Este ejemplo contiene las definiciones de servidor.  
  
    -   El usuario puede conectarse a la base de datos requerida simplemente cambiando los valores a las definiciones de servidor de origen y de destino necesarias. En el ejemplo se proporcionan todos los valores que se han proporcionado como valores de variable que están disponibles en **VariableValueFileSample. XML**.  El resto de parámetros de conexión se pueden quitar del archivo de conexión del servidor de trabajo del usuario.  
  
    -   Para obtener más información sobre cómo conectarse a los servidores de origen y de destino, vea [crear archivos de conexión de servidor &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md) .  
  
-   **VariableValueFileSample. xml:** Todas las variables que se han usado en los archivos de script de `ServersConnectionFileSample.xml` la consola de ejemplo y se han intercalado en este archivo. Para ejecutar los scripts de la consola de ejemplo, el usuario tiene que reemplazar simplemente los valores de la variable de ejemplo por los definidos por el usuario y pasar este archivo como un argumento de línea de comandos adicional junto con el archivo de script.  
  
    Para obtener más información sobre el archivo de valores de variable, vea [crear archivos de valor variable &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md).  
  
-   **AssessmentReportGenerationSample. xml:** Este ejemplo permite al usuario generar un informe de evaluación de XML que el usuario puede usar para el análisis antes de empezar a convertir y migrar los datos.  
  
    En el `generate-assessment-report` comando, el usuario tiene que cambiar el valor de la variable (consulte **VariableValueFileSample. XML**) `object-name` en el atributo con el nombre de la base de datos que está usando el usuario. Dependiendo del tipo de objeto especificado, el `object-type` valor también tendrá que cambiarse.  
  
    Si el usuario tiene que evaluar varios objetos o bases de datos, puede especificar varios `metabase-object` nodos, tal como se `generate-assessment-report` muestra en el ejemplo 4 del comando del archivo de script de la consola de ejemplo.  
  
    Para obtener más información sobre la generación de informes, consulte [generación de informes &#40;MySQLToSQL&#41;](../../ssma/mysql/generating-reports-mysqltosql.md).  
  
    **Notas:**  
  
    -   Asegúrese de que el argumento de la línea de comandos del archivo de valores de variable se pasa a la aplicación de consola y VariableValueFileSample. XML se actualiza con los valores especificados por el usuario.  
  
    -   Asegúrese de que el argumento de la línea de comandos del archivo de conexión de servidor se pasa a la aplicación de consola y ServersConnectionFileSample. XML se actualiza con los valores de parámetro de servidor correctos.  
  
-   **SqlStatementConversionSample. xml:**  
    Este ejemplo permite al usuario generar el script correspondiente `t-sql` para el comando de base `sql` de datos de origen proporcionado como entrada.  
  
    En el `convert-sql-statement` comando, el usuario tiene que cambiar el valor de la variable (consulte **VariableValueFileSample. XML**) `context` en el atributo con el nombre de la base de datos que está usando el usuario. También se requerirá al usuario que cambie el `sql` valor del atributo al comando de `sql` la base de datos de origen que necesite convertir.  
  
    El usuario también puede proporcionar los archivos SQL que se van a convertir. Esto se ilustra en el `convert-sql-statement` ejemplo 4 del comando del archivo de script de la consola de ejemplo.  
  
    > [!NOTE]  
    > Asegúrese de que el argumento de la línea de comandos del archivo de valores de variable se pasa a la aplicación de consola y VariableValueFileSample. XML se actualiza con los valores especificados por el usuario.  
  
-   **ConversionAndDataMigrationSample. xml:**  
     Este ejemplo permite al usuario realizar una migración de un extremo a otro de la conversión a la migración de datos. A continuación se muestra la lista de valores de atributo obligatorios que tendrán que cambiar:  
  
    **Nombre de comando**  
  
    `map-schema`  
  
    Asignación de esquema de la base de datos de origen al esquema de destino.  
  
    **Atributo**  
  
    -   `source-schema:`Especifica la base de datos de origen que requiere que se convierta.  
  
    -   `sql-server-schema`: Especifica la base de datos de destino que se va a migrar a  
  
    **Nombre de comando**  
  
    `convert-schema`  
  
    1.  Realiza la conversión del esquema del origen al esquema de destino.  
  
    2.  Si el usuario tiene que evaluar varios objetos o bases de datos, puede especificar varios `metabase-object` nodos, tal como se `convert-schema` muestra en el ejemplo 4 del comando del archivo de script de la consola de ejemplo.  
  
    **Atributo**  
  
    `object-name`: Especifique el nombre de objeto o base de datos de origen que requiere la conversión. Asegúrese de que se `object-type` cambia el correspondiente según el tipo de objeto que se especifica en el`object-name`  
  
    **Nombre de comando**  
  
    `synchronize-target`  
  
    1.  Sincroniza los objetos de destino con la base de datos de destino.  
  
    2.  Si el usuario tiene que evaluar varios objetos o bases de datos, puede especificar varios `metabase-object` nodos, tal como se `synchronize-target` muestra en el ejemplo 3 del comando del archivo de script de la consola de ejemplo.  
  
    **Atributo**  
  
    `object-name:`Especifique el nombre de objeto o base de datos de SQL Server que requiere que se cree. Asegúrese de que se `object-type` cambia el correspondiente según el tipo de objeto que se especifica en el`object-name`  
  
    **Nombre de comando**  
  
    `migrate-data`  
  
    1.  Migra los datos de origen al destino.  
  
    2.  Si el usuario tiene que evaluar varios objetos o bases de datos, puede especificar varios `metabase-object` nodos, tal como se `migrate-data` muestra en el ejemplo 2 del comando del archivo de script de la consola de ejemplo.  
  
    **Atributo**  
  
    `object-name:`Especifica el nombre de la base de datos o de las tablas de origen que requiere la migración. Asegúrese de que se `object-type` cambia el correspondiente según el tipo de objeto que se especifica en el`object-name`  
  
## <a name="see-also"></a>Consulte también  
[Crear archivos de valores de variable &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
[Crear los archivos de conexión del servidor &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
[Generar informes &#40;MySQLToSQL&#41;](../../ssma/mysql/generating-reports-mysqltosql.md)  
  
