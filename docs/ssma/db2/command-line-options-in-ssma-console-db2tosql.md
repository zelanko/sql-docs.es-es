---
title: "Opciones de línea de comandos en la consola SSMA (DB2ToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 237354e9-25c4-4386-9d1f-ca0618d4a9a0
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4a48daba17ddb4695f362414037615789ce8509b
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="command-line-options-in-ssma-console-db2tosql"></a>Opciones de línea de comandos en la consola SSMA (DB2ToSQL)
Microsoft le proporciona un opciones de línea de comandos de conjunto robusto para ejecutar y controlar las actividades SSMA. Las secciones posteriores detallan los mismos.  
  
## <a name="command-line-options-in-ssma-console"></a>Opciones de línea de comandos en la consola SSMA  
Descritos en este documento es la consola de opciones de comando.  
  
Con el propósito de esta sección, el término 'opción' también se conoce como 'switch'.  
  
Opciones no distinguen mayúsculas de minúsculas y puede comenzar por '**-**'or',**/**' caracteres.  
  
Si se especifican opciones, es obligatorio especificar los parámetros de opción correspondiente.  
  
Parámetros de opción deben estar separados de lo caracteres de la opción por espacio en blanco.  
  
**Ejemplos de sintaxis:**  
  
`C:\> SSMAforDB2Console.EXE -s scriptfile`  
  
`C:\> SSMAforDB2Console.EXE -s “C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \AssessmentReportGenerationSample.xml” –v “C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \VariableValueFileSample.xml” –c “C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ServersConnectionFileSample.xml”`  
  
Nombres de un archivo o carpeta que contienen espacios deben especificarse entre comillas dobles.  
  
La salida de las entradas de la línea de comandos y mensajes de error se almacenan en STDOUT o en un archivo especificado.  
  
### <a name="script-file-option-sscript"></a>Opción de archivo de script: – s/script  
Un conmutador obligatorio, la ruta de acceso y nombre de archivo de script especifica la secuencia de comandos de secuencias de comando que ejecutará SSMA.  
  
**Ejemplos de sintaxis:**  
  
`C:\>SSMAforDB2Console.EXE –s “C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”`  
  
### <a name="variable-value-file-option-vvariable"></a>Opción de archivo de valor de variable: la variable o – v  
Este archivo consta de las variables utilizadas en el archivo de script. Se trata de un modificador opcional. Si las variables no están declaradas en el archivo de variables y usar en el archivo de script, la aplicación genera un error y finaliza la ejecución de la consola.  
  
**Ejemplos de sintaxis:**  
  
-   Variables definidas en varios archivos de valor de la variable, por ejemplo, uno con un valor predeterminado y otro con un valor específico de instancia cuando sea aplicable. El último archivo de variable especificado en los argumentos de línea de comandos toma la preferencia, en caso de que hay una duplicación de variables:  
  
    `C:\>SSMAforDB2Console.EXE -s`  
  
    `“C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml” –v c:\migration`  
  
    `projects\global_variablevaluefile.xml –v “c:\migrationprojects\instance_variablevaluefile.xml”`  
  
### <a name="server-connection-file-option-cserverconnection"></a>Opción de archivo de conexión de servidor: – c/serverconnection  
Este archivo contiene información de conexión de servidor para cada servidor. Cada definición de servidor se identifica mediante un identificador de servidor único. Los identificadores de servidor se hace referencia en el archivo de secuencia de comandos para conexión comandos relacionados con.  
  
Definición de servidor puede ser una parte del archivo de conexión de servidor o un archivo de script. Id. de servidor en el archivo de script tiene prioridad sobre el archivo de conexión de servidor, en caso de que hay una duplicación de Id. de servidor.  
  
**Ejemplos de sintaxis:**  
  
-   Id. de servidor se utiliza en el archivo de script y se definen en un archivo de conexión de servidor independiente, el archivo de conexión de servidor utiliza las variables que se definen en el archivo de valor de la variable:  
  
    `C:\>SSMAforDB2Console.EXE –s “C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –v`  
  
    `c:\SsmaProjects\myvaluefile1.xml –c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   Definición de servidor se incrusta en el archivo de script:  
  
    `C:\>SSMAforDB2Console.EXE –s “C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>Opción de salida XML: - x / xmloutput [xmloutputfile]  
Este comando se usa para generar los mensajes de salida del comando en un formato xml en consola o en un archivo xml.  
  
Existen dos opciones para xmloutput, especialmente..,:  
  
-   Si no se proporciona la ruta del archivo después del modificador xmloutput se redirige la salida al archivo.  
  
    **Ejemplo de sintaxis:**  
  
    `C:\>SSMAforDB2Console.EXE –s`  
  
    `“C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –x d:\xmloutput\project1output.xml`  
  
-   Si no se proporciona ningún filepath después del modificador xmloutput el xmlout se muestra en la consola en Sí.  
  
    **Ejemplo de sintaxis:**  
  
    `C:\>SSMAforDB2Console.EXE –s “C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –xmloutput`  
  
### <a name="log-file-option-llog"></a>Opción de archivo de registro: – l y registro de  
Todas las operaciones de SSMA en la aplicación de consola se graben en un archivo de registro. Se trata de un modificador opcional. Si se especifican un archivo de registro y su ruta de acceso en la línea de comandos, obtiene genera el registro en la ubicación especificada. En caso contrario, se genera en su ubicación predeterminada.  
  
**Ejemplo de sintaxis:**  
  
`C:\>SSMAforDB2Console.EXE`  
  
`“C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option-eprojectenvironment"></a>Opción de carpeta de entorno de proyecto: – e/projectenvironment  
Esto indica que la carpeta de configuración del entorno de proyecto para el proyecto SSMA actual. Este parámetro es opcional.  
  
**Ejemplo de sintaxis:**  
  
`C:\>SSMAforDB2Console.EXE –s`  
  
`“C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml”  –e c:\SsmaProjects\CommonEnvironment`  
  
### <a name="secure-password-option-psecurepassword"></a>Opción de contraseña segura: – p/securepassword  
Esta opción indica que la contraseña cifrada para las conexiones de servidor. Difiere de todas las demás opciones: la opción, ejecuta cualquier secuencia de comandos ni ayuda a las actividades relacionadas con la migración, pero ayuda a administrar el cifrado de contraseña para las conexiones de servidor utilizado en el proyecto de migración.  
  
No puede especificar cualquier otra opción o contraseña como el parámetro de línea de comandos. En caso contrario, produce un error. Para obtener más información, consulte el [administrar contraseñas](http://msdn.microsoft.com/en-us/56d546e3-8747-4169-aace-693302667e94) sección.  
  
Se admiten las siguientes opciones secundarias para `–p/securepassword`:  
  
-   Para agregar la contraseña para almacenamiento protegido para un identificador de servidor especificado o para todos los identificadores de servidor definidos en el archivo de conexión de servidor. -Opción de sobrescritura, a continuación, las actualizaciones de la contraseña si ya existe:  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}` `-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   Para quitar la contraseña cifrada desde el almacenamiento protegido del identificador de servidor especificado o para todos los Id. de servidor:  
  
    `–p/securepassword –r/remove {<server_id> [, …n] | all}`  
  
-   Para mostrar una lista de identificadores de servidor para el que se cifra la contraseña:  
  
    `–p/securepassword –l/list`  
  
-   Para exportar las contraseñas almacenadas en almacenamiento protegido a un archivo cifrado. Este archivo se cifra con la frase de contraseña especificada por el usuario.  
  
    `–p/securepassword –e/export {<server-id> [, …n] | all} <encrypted-password -file>`  
  
-   El cifrado archivo que se exportó anteriormente se importa en almacenamiento protegido local con la frase de contraseña especificada por el usuario. Una vez que el archivo se descifra, se almacena en un archivo nuevo, que a su vez, se cifra en el equipo local.  
  
    `–p/securepassword –i/import {<server-id> [, …n] | all} <encrypted-password -file>`  
  
    Varios identificadores de servidor puede especificarse mediante separadores de millares.  
  
### <a name="help-option-help"></a>Opción de ayuda::? / Help  
Muestra el resumen de la sintaxis de las opciones de la consola SSMA:  
  
`C:\>SSMAforDB2Console.EXE -?`  
  
Para una vista tabular de las opciones de línea de comandos de consola SSMA, consulte [apéndice - 1 &#40; DB2ToSQL &#41;](../../ssma/db2/appendix-1-db2tosql.md).  
  
### <a name="securepassword-help-option-securepassword--help"></a>Opción de ayuda SecurePassword: – securepassword-? / Help  
Muestra el resumen de la sintaxis de las opciones de la consola SSMA:  
  
`C:\>SSMAforDB2Console.EXE -securepassword -?`  
  
Para una vista tabular de las opciones de línea de comandos de consola SSMA, consulte [apéndice - 1 &#40; DB2ToSQL &#41;](../../ssma/db2/appendix-1-db2tosql.md)  
  
### <a name="next-step"></a>Paso siguiente  
El paso siguiente depende de los requisitos del proyecto:  
  
1.  Para especificar una contraseña o la exportación / importación de contraseñas, vea [administrar contraseñas &#40; DB2ToSQL &#41;](../../ssma/db2/managing-passwords-db2tosql.md).  
  
2.  Para generar informes, consulte [generar informes &#40; DB2ToSQL &#41;](../../ssma/db2/generating-reports-db2tosql.md).  
  
3.  Para solucionar problemas en la consola, consulte [Troubleshooting &#40; DB2ToSQL &#41;](../../ssma/db2/troubleshooting-db2tosql.md).  
  

