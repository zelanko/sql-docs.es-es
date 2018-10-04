---
title: Creación de archivos de Script (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Script File Creation, Configuring Oracle Console Settings
- Script File Creation, Non-Configurable option
- Script File Creation, Script File Validation
ms.assetid: 55e5bc68-3040-4f07-bb00-0408a17c9821
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 879aaaf33365cb7453c1047c3f9b2408edee10f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47846783"
---
# <a name="creating-script-files-oracletosql"></a>Creación de archivos de script (OracleToSQL)
El primer paso antes de iniciar la aplicación de consola SSMA crear el archivo de script y si es necesario crear el archivo de valor de la variable y el archivo de conexión de servidor.  
  
El archivo de script puede dividirse en tres secciones viz..,:  
  
1.  **config:** permite al usuario establecer los parámetros de configuración para la aplicación de consola.  
  
2.  **servidores:** permite al usuario establecer el origen o destino de las definiciones de servidor. Esto también puede estar en un archivo de conexión de servidor independiente.  
  
3.  **secuencias de comandos:** permite al usuario ejecutar comandos de flujo de trabajo SSMA.  
  
Cada sección se describe en detalle a continuación:  
  
## <a name="configuring-oracle-console-settings"></a>Configuración de la consola de Oracle  
Las configuraciones de una secuencia de comandos se muestran en el archivo de script de la consola.  
  
Si cualquiera de los elementos se especifican en el nodo de configuración, se establecen como la configuración global, es decir, son aplicables a todos los comandos de script. Estos elementos de configuración también pueden establecerse dentro de cada comando en la sección de la secuencia de comandos si el usuario desea invalidar la configuración global.  
  
Las opciones configurables por el usuario incluyen:  
  
1.  **Proveedor de la ventana de salida:** si suprimir de mensajes está establecido en 'true', la específica del comando no se muestran mensajes en la consola. La descripción de los atributos se indica a continuación:  
  
    -   destino: Especifica si la salida se debe imprimir a un archivo o stdout. Se trata de un valor predeterminado es false.  
  
    -   nombre de archivo: la ruta de acceso del archivo (opcional).  
  
    -   Suprimir-messages: suprime los mensajes en la consola. Esto es 'false', de forma predeterminada.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <output-window  
  
        suppress-messages="<true/false>"   (optional)  
  
        destination="<file/stdout>"        (optional)  
  
        file-name="<file-name>"            (optional)  
  
       />  
  
    </output-providers>  
    ```  
    *O*  
  
    ```xml  
    <…All commands…>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </…All commands…>  
    ```  
  
2.  **Proveedor de conexión de la migración de datos:** Esto especifica que el servidor de origen o destino es para considerarse para la migración de datos.  Origen-use-último uso indica que se utiliza el último servidor de origen usados para la migración de datos. Del mismo modo destino-use-último uso indica que se utiliza el último servidor de destino usada para la migración de datos. El usuario también puede especificar el servidor (origen o destino) mediante el uso de los atributos de servidor de origen o el servidor de destino.  
  
    Puede usarse, es decir, solo uno o el otro atributo especificado:  
  
    -   origen-use-último uso = "true" (valor predeterminado) o servidor de origen = "source_servername"  
  
    -   destino-use-último uso = "true" (valor predeterminado) o servidor de destino = "target_servername"  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <data-migration-connection source-use-last-used="true"  
  
                                 target-server="<target-server-unique-name>"/>  
  
    </output-providers>  
    ```  
    *O*  
  
    ```xml  
    <migrate-data>  
  
      <data-migration-connection   source-server="<source-server-unique-name>"  
  
                                   target-use-last-used="true"/>  
  
    </migrate-data>  
    ```  
  
3.  **Menú emergente de entrada de usuario:** Esto permite el tratamiento de errores, cuando los objetos se cargan desde la base de datos. El usuario proporciona los modos de entrada y, si se produce un error, la consola continúa tal como especifica el usuario.  
  
    Los modos incluyen:  
  
    -   **formular-usuario -** pide al usuario que continue('yes') o error ('n').  
  
    -   **Error:** la consola mostrará un error y detiene la ejecución.  
  
    -   **continuar-** continúa de la consola con la ejecución.  
  
    El modo predeterminado es **error**.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </output-providers>  
    ```  
    *O*  
  
    ```xml  
    <!-- Connect to target database -->  
  
    <connect-target-database server="<target-server-unique-name>">  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </connect-target-database>  
    ```  
  
4.  **Volver a conectar el proveedor:** Esto permite al usuario establecer la reconexión configuración en caso de errores de conexión. Esto se puede establecer para servidores de origen y destino.  
  
    Los modos de reconexión son:  
  
    -   volver a conectarse a último-usar-servidor: si la conexión no está activa, intenta volver a conectarse hasta el último servidor que se usa como máximo 5 veces.  
  
    -   generar un error: si la conexión no está activa, se genera un error.  
  
    El modo predeterminado es **generar un error**.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <reconnect-manager on-source-reconnect="<reconnect-to-last-used-server/generate-an-error>"  
  
                         on-target-reconnect="<reconnect-to-last-used-server/generate-an-error>"/>  
  
    </output-providers>  
    ```  
    *O*  
  
    ```xml  
    <!--synchronization-->  
  
    <synchronize-target>  
  
      <reconnect-manager on-target-reconnect="reconnect-to-last-used-server"/>  
  
    </synchronize-target>  
    ```  
    *O*  
  
    ```xml  
    <!--data migration-->  
  
    <migrate-data server="<target-server-unique-name>">  
  
      <reconnect-manager  
  
        on-source-reconnect="reconnect-to-last-used-server"  
  
        on-target-reconnect="generate-an-error"/>  
  
    </migrate-data>  
    ```  
  
5.  **Proveedor de sobrescritura de convertidor:** Esto permite al usuario controlar los objetos que ya están presentes en el destino de la metabase. Las posibles acciones incluyen:  
  
    -   Error: la consola mostrará un error y detiene la ejecución.  
  
    -   sobrescribir: sobrescribe los valores de objeto existentes. Esta acción se realiza de forma predeterminada.  
  
    -   Omitir: la consola omite los objetos que ya existen en la base de datos  
  
    -   usuario preguntar: pide al usuario para la entrada ('Sí' / 'no')  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </output-providers>  
    ```  
    *O*  
  
    ```xml  
    <convert-schema object-name="<object-name>">  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </convert-schema>  
    ```  
  
6.  **Error de requisitos previos de proveedor:** Esto permite al usuario controlar los requisitos previos que son necesarios para procesar un comando. De forma predeterminada, el modo strict es 'false'. Si se establece en 'true', una excepción se genera si hay errores a cumplir los requisitos previos.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true/false>"/>  
  
    </output-providers>  
    ```  
  
7.  **Operación de detención:** durante la operación intermedio, si el usuario desea detener la operación, a continuación, **'Ctrl + C'** se puede usar la tecla de acceso rápido. SSMA para Oracle consola esperará a que se complete la operación y finaliza la ejecución de la consola.  
  
    Si el usuario desea detener la ejecución inmediatamente, a continuación, **'Ctrl + C'** pueden presionar teclas de acceso rápido nuevo para la terminación repentina de la aplicación de consola de SSMA.  
  
8.  **Proveedor de progreso:** informa del progreso de cada comando de la consola. Esta opción está deshabilitada de forma predeterminada. Constan de los atributos de informes de progreso:  
  
    -   off  
  
    -   cada 1%  
  
    -   una de las 2%  
  
    -   una de las 5%  
  
    -   una de las 10%  
  
    -   una de las 20%  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <progress-reporting enable="<true/false>"            (optional)  
  
                          report-messages="<true/false>"   (optional)  
  
                          report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off" (optional)/>  
  
    </output-providers>  
    ```  
    *O*  
  
    ```xml  
    <…All commands…>  
  
      <progress-reporting  
  
        enable="<true/false>"            (optional)  
  
        report-messages="<true/false>"   (optional)  
  
        report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off"     (optional)/>  
  
    </…All commands…>  
    ```  
  
9. **Nivel de detalle del registrador:** conjuntos de nivel de detalle de registro. Esto se corresponde con la opción de todas las categorías en la interfaz de usuario. De forma predeterminada, el nivel de detalle de registro es "error".  
  
    Las opciones de nivel de registrador incluyen:  
  
    -   error irrecuperable: se registran los mensajes solo error irrecuperable.  
  
    -   Error: se registran los mensajes de error y el error irrecuperable única.  
  
    -   Advertencia: se registran todos los niveles, excepto los mensajes de depuración e información.  
  
    -   Info: todos los niveles, salvo que se registran los mensajes de depuración.  
  
    -   depurar: todos los niveles de los mensajes registrados.  
  
    > [!NOTE]  
    > Se registran mensajes obligatorios en cualquier nivel.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </output-providers>  
    ```  
    *O*  
  
    ```xml  
    <…All commands…>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </…All commands…>  
    ```  
  
10. **Contraseña cifrada de invalidación:** si es 'true', la contraseña de texto no cifrado especificado en la sección de definición de servidor del archivo de conexión del servidor o en el archivo de script, invalidaciones de la contraseña cifrada almacenada en almacenamiento protegido, si ya existe. Si se especifica ninguna contraseña en texto no cifrado, se solicita al usuario que escriba la contraseña.  
  
    Aquí surgen dos casos:  
  
    1.  Si invalidar la opción es **false**, el orden de búsqueda estarán protegidos almacenamiento -&gt;archivo de Script -&gt;archivo de conexión de servidor -&gt; preguntar al usuario.  
  
    2.  Si invalidar la opción es **true**, será el orden de búsqueda de archivo de Script -&gt;archivo de conexión de servidor -&gt;preguntar al usuario.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
Es la opción que no es configurable:  
  
-   **Número máximo de intentos de reconexión:** cuando una conexión establecida se agota el tiempo o se interrumpe debida a errores de red, el servidor es necesario volver a conectarse. Se permiten los intentos de reconexión a un máximo de **5** reintentos después de eso, la consola realiza automáticamente la reconexión. La instalación de la reconexión automática reduce el esfuerzo de volver a ejecutar el script.  
  
## <a name="server-connection-parameters"></a>Parámetros de conexión del servidor  
Parámetros de conexión de servidor pueden definirse en el archivo de script o en el archivo de conexión de servidor. Consulte la [crear los archivos de conexión de servidor &#40;OracleToSQL&#41; ](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md) sección para obtener más detalles.  
  
## <a name="script-commands"></a>Comandos de script  
El archivo de script contiene una secuencia de comandos de flujo de trabajo de migración en formato XML. La aplicación de consola SSMA procesa la migración en el orden de los comandos que aparecen en el archivo de script.  
  
Por ejemplo, sigue a la jerarquía de una migración de datos típica de una tabla específica en una base de datos de Oracle: esquema -&gt; tabla.  
  
Cuando todos los comandos en el archivo de script se ejecuta correctamente, la aplicación de consola SSMA sale y devuelve el control al usuario. El contenido de un archivo de script es más o menos estático con información sobre las variable contenidas en un [crear archivos de valor Variable &#40;OracleToSQL&#41; ](../../ssma/oracle/creating-variable-value-files-oracletosql.md) o, en una sección independiente dentro del archivo de script para los valores de variable.  
  
**Ejemplo:**  
  
```xml  
<!--Sample of script file commands -->  
  
<ssma-script-file>  
  
  <script-commands>  
  
    <create-new-project project-folder="<project-folder>"  
  
                        project-name="<project-name>"  
  
                        overwrite-if-exists="<true/false>"/>  
  
    <connect-source-database server="<source-server-unique-name>"/>  
  
    <save-project/>  
  
    <close-project/>  
  
  </script-commands>  
  
</ssma-script-file>  
```  
Se proporcionan plantillas que consta de 3 archivos de script (para ejecutar varios escenarios), archivo de valores de variable y un archivo de conexión de servidor en la carpeta de Scripts de la consola de ejemplo del directorio del producto:  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
Puede ejecutar las plantillas (archivos) después de cambiar los parámetros que aparecen en ella por su gran relevancia.  
  
Encontrará una lista completa de comandos de script en [ejecutando la consola de SSMA &#40;OracleToSQL&#41;](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)  
  
## <a name="script-file-validation"></a>Validación del archivo de script  
El usuario puede validar fácilmente su archivo de script en el archivo de definición de esquema **'O2SSConsoleScriptSchema.xsd'** disponible en la carpeta "Esquemas".  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en el funcionamiento de la consola es [crear archivos de valor Variable &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md).  
  
## <a name="see-also"></a>Vea también  
[Creación de archivos de valor Variable &#40;OracleToSQL&#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  
