---
title: "Opciones de línea de comandos en la consola SSMA (AccessToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 08/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c1f3b3f0-0f3e-4e07-b745-2fbdde85c67e
caps.latest.revision: "11"
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: Inactive
ms.openlocfilehash: 7a7f1612f8947a67ec454a4fcc25c7e155d9f23e
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="command-line-options-in-the-ssma-console-accesstosql"></a>Opciones de línea de comandos en la consola de SSMA (AccessToSQL)
Microsoft le ofrece un potente conjunto de opciones de línea de comandos para ejecutar y controlar las actividades SSMA. En las secciones posteriores se proporcionan detalles adicionales.  
  
## <a name="command-line-options-in-the-ssma-console"></a>Opciones de línea de comandos en la consola de SSMA  
Descritos en este documento es la consola de opciones de comando.  
  
Con el propósito de esta sección, el término 'opción' también se conoce como 'switch'.  
  
Opciones no distinguen mayúsculas de minúsculas y puede comenzar por la '**-**'o'**/**' caracteres.  
  
Si se especifican opciones, es obligatorio especificar los parámetros de opción correspondientes.  
  
Parámetros de opción deben estar separados de lo caracteres de la opción por espacio en blanco.  
  
**Ejemplos de sintaxis:**  
  
`C:\> SSMAforAccessConsole.EXE -s scriptfile`  
  
`C:\> SSMAforAccessConsole.EXE -s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\AssessmentReportGenerationSample.xml” –v “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\VariableValueFileSample.xml” –c “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ServersConnectionFileSample.xml”`  
  
Nombres de un archivo o carpeta que contienen espacios deben especificarse entre comillas dobles.  
  
La salida de entradas de línea de comandos y mensajes de error se almacena en STDOUT o en un archivo especificado.  
  
### <a name="script-file-option-sscript"></a>Opción de archivo de script: – s/script  
Un conmutador obligatorio, la ruta de acceso y nombre de archivo de script especifica la secuencia de comandos de secuencias de comando que ejecutará SSMA.  
  
**Ejemplos de sintaxis:**  
  
`C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="variable-value-file-option-vvariable"></a>Opción de archivo de valor de la variable: – v o la variable  
El archivo de valores de variable consta de las variables utilizadas en el archivo de script. El modificador es opcional. Si las variables no están declaradas en el archivo de variables y usar en el archivo de script, la aplicación genera un error y finaliza la ejecución de la consola.  
  
**Ejemplos de sintaxis:**  
  
-   Variables definidas en varios archivos de valor de la variable, por ejemplo, uno con un valor predeterminado y otro con un valor específico de la instancia cuando sea aplicable. El último archivo de variable especificado en los argumentos de línea de comandos toma la preferencia, en caso de que hay una duplicación de variables:  
  
    `C:\>SSMAforAccessConsole.EXE -s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml” –v c:\migration`  
  
    `projects\global_variablevaluefile.xml –v “c:\migrationprojects\instance_variablevaluefile.xml”`  
  
### <a name="server-connection-file-option-cserverconnection"></a>Opción de archivo de conexión de servidor: – c/serverconnection  
Este archivo contiene información de conexión de servidor para cada servidor. Cada definición de servidor se identifica mediante un identificador de servidor único. Los identificadores de servidor se hace referencia en el archivo de script para los comandos relacionados con la conexión.  
  
Definición de servidor puede ser una parte del archivo de conexión de servidor o un archivo de script. Id. de servidor en el archivo de script tiene prioridad sobre el archivo de conexión de servidor, en caso de que hay una duplicación de Id. de servidor.  
  
**Ejemplos de sintaxis:**  
  
-   Id. de servidor se utiliza en el archivo de script. Se definen en un archivo de conexión de servidor independiente. Este archivo usa las variables que se definen en el archivo de valor de la variable:  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –v`  
  
    `c:\SsmaProjects\myvaluefile1.xml –c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   Definición de servidor se incrusta en el archivo de script:  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>Opción de salida de XML: - x / xmloutput [xmloutputfile]  
Este comando se usa para generar los mensajes de salida del comando en un formato xml en consola o en un archivo xml.  
  
Hay dos opciones disponibles para xmloutput, a saber:  
  
-   Si no se proporciona la ruta del archivo después del modificador xmloutput, se redirige la salida al archivo.  
  
    **Ejemplo de sintaxis:**  
  
    `C:\>SSMAforAccessConsole.EXE –s`  
  
    `“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –x d:\xmloutput\project1output.xml`  
  
-   Si no se proporciona ningún filepath después del modificador xmloutput, el xmlout se muestra en la consola en Sí.  
  
    **Ejemplo de sintaxis:**  
  
    `C:\>SSMAforAccessConsole.EXE –s “C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –xmloutput`  
  
### <a name="log-file-option-llog"></a>Opción de archivo de registro: – l/registro  
Todas las operaciones de SSMA en la aplicación de consola se registran en un archivo de registro y el modificador es opcional. Si se especifican un archivo de registro y su ruta de acceso en la línea de comandos, obtiene genera el registro en la ubicación especificada. En caso contrario, se genera en su ubicación predeterminada.  
  
**Ejemplo de sintaxis:**  
  
`C:\>SSMAforAccessConsole.EXE`  
  
`“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option-eprojectenvironment"></a>Opción de carpeta de entorno del proyecto: – e/projectenvironment  
Este modificador opcional indica la carpeta de configuración del entorno de proyecto para el proyecto SSMA actual.  
  
**Ejemplo de sintaxis:**  
  
`C:\>SSMAforAccessConsole.EXE –s`  
  
`“C:\Program Files\Microsoft SQL Server Migration Assistant for Access\Sample Console Scripts\ConversionAndDataMigrationSample.xml”  –e c:\SsmaProjects\CommonEnvironment`  
  
||  
|-|  
||  
  
### <a name="secure-password-option-psecurepassword"></a>Proteger la opción password: – p/securepassword  
Esta opción indica que la contraseña cifrada para las conexiones de servidor. Difiere de todas las demás opciones en cuanto no ejecutar cualquier secuencia de comandos o ayuda en las actividades relacionadas con la migración, pero ayuda a administrar el cifrado de contraseña para las conexiones de servidor utilizado en el proyecto de migración.  
  
No puede especificar cualquier otra opción o contraseña como el parámetro de línea de comandos. En caso contrario, produce un error. Para obtener más información, consulte el [administrar contraseñas](http://msdn.microsoft.com/b099d0f9-dd37-4c87-8b6f-ed0177881ea4) sección.  
  
Las subopciones siguientes se admiten para `–p/securepassword`:  
  
-   Para agregar una contraseña o actualizar una contraseña existente, en el almacenamiento protegido para un identificador de servidor especificado o para todos los identificadores de servidor definidos en el archivo de conexión de servidor:  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
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
  
### <a name="help-option-help"></a>Help (opción)::? / Help  
Muestra el resumen de la sintaxis de las opciones de la consola SSMA:  
  
`C:\>SSMAforAccessConsole.EXE -?`  
  
Para una vista tabular de las opciones de línea de comandos de consola SSMA, consulte [apéndice - 1 &#40; AccessToSQL &#41; ](../../ssma/access/appendix-1-accesstosql.md).  
  
### <a name="securepassword-help-option-securepassword--help"></a>Opción de ayuda SecurePassword: – securepassword-? / Help  
Muestra el resumen de la sintaxis de las opciones de la consola SSMA:  
  
`C:\>SSMAforAccessConsole.EXE -securepassword -?`  
  
Para una vista tabular de las opciones de línea de comandos de consola SSMA, consulte [apéndice - 1 &#40; AccessToSQL &#41;](../../ssma/access/appendix-1-accesstosql.md)  
  
### <a name="next-steps"></a>Pasos siguientes  
El paso siguiente depende de los requisitos del proyecto:  
  
1.  Para especificar una contraseña o la exportación / importación de contraseñas, vea [administrar contraseñas &#40; AccessToSQL &#41; ](../../ssma/access/managing-passwords-accesstosql.md).  
  
2.  Para generar informes, vea [generación de informes &#40; AccessToSQL &#41; ](../../ssma/access/generating-reports-accesstosql.md).  
  
3.  Para solucionar problemas en la consola, consulte [Troubleshooting &#40; AccessToSQL &#41; ](../../ssma/access/troubleshooting-accesstosql.md).  
  
