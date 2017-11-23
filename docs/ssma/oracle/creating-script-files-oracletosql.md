---
title: Crear archivos de Script (OracleToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Script File Creation, Configuring Oracle Console Settings
- Script File Creation, Non-Configurable option
- Script File Creation, Script File Validation
ms.assetid: 55e5bc68-3040-4f07-bb00-0408a17c9821
caps.latest.revision: "37"
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 29a445d0392c77b0773f612636eeca08597c47c2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="creating-script-files-oracletosql"></a>Crear archivos de Script (OracleToSQL)
El primer paso antes de iniciar la aplicación de consola SSMA consiste en crear el archivo de script y si es necesario crear el archivo de valor de la variable y el archivo de conexión de servidor.  
  
El archivo de script puede dividirse en tres secciones, especialmente..,:  
  
1.  **config:** permite al usuario establecer los parámetros de configuración para la aplicación de consola.  
  
2.  **servidores:** permite al usuario establecer las definiciones de servidores de origen o destino. Esto también puede estar en un archivo de conexión de servidor independiente.  
  
3.  **comandos de script:** permite al usuario ejecutar comandos de flujo de trabajo SSMA.  
  
Cada sección se describe en detalle a continuación:  
  
## <a name="configuring-oracle-console-settings"></a>Configuración de la consola de Oracle  
Las configuraciones de una secuencia de comandos se muestran en el archivo de secuencia de comandos de consola.  
  
Si cualquiera de los elementos se especifican en el nodo de configuración, se establecen como la configuración global, es decir, son aplicables para todos los comandos de script. Estos elementos de configuración también pueden establecerse en cada comando en la sección de la secuencia de comandos si el usuario desea invalidar la configuración global.  
  
Las opciones configurables por el usuario incluyen:  
  
1.  **Proveedor de la ventana de salida:** si mensajes suprimir atributo está establecido en 'true', la específica de un comando no se muestren mensajes en la consola. La descripción de atributos se indica a continuación:  
  
    -   destino: Especifica si el resultado es necesario obtener imprime en un archivo o stdout. Se trata de un valor predeterminado es false.  
  
    -   nombre de archivo: la ruta de acceso del archivo (opcional).  
  
    -   mensajes suprimir: suprime los mensajes en la consola. Esto es 'false' de forma predeterminada.  
  
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
    *o*  
  
    ```xml  
    <…All commands…>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </…All commands…>  
    ```  
  
2.  **Proveedor de la conexión de migración de datos:** especifica que el servidor de origen o destino es considerarse para la migración de datos.  Origen-use-utilizó por última vez, se indica que se usa el último servidor de origen usados para la migración de datos. De forma similar al destino-use-utilizó por última vez se indica que se utiliza el último servidor de destino utilizado para la migración de datos. El usuario también puede especificar el servidor (origen o destino) mediante el uso de los atributos de servidor de origen o el servidor de destino.  
  
    Puede usarse, es decir, solo uno o el otro atributo especificado:  
  
    -   origen: use-utilizó por última vez = "true" (valor predeterminado) o servidor de origen = "source_servername"  
  
    -   destino-use-utilizó por última vez = "true" (valor predeterminado) o servidor de destino = "target_servername"  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <data-migration-connection source-use-last-used="true"  
  
                                 target-server="<target-server-unique-name>"/>  
  
    </output-providers>  
    ```  
    *o*  
  
    ```xml  
    <migrate-data>  
  
      <data-migration-connection   source-server="<source-server-unique-name>"  
  
                                   target-use-last-used="true"/>  
  
    </migrate-data>  
    ```  
  
3.  **Elemento emergente de entrada de usuario:** Esto permite el tratamiento de errores, cuando los objetos se cargan desde la base de datos. El usuario proporciona los modos de entrada, y si se produce un error, la consola continúa tal y como especifica el usuario.  
  
    Los modos son:  
  
    -   **pida-usuario -** pide al usuario que continue('yes') o error ('n').  
  
    -   **error -** la consola mostrará un error y detiene la ejecución.  
  
    -   **continuar-** la consola continúa con la ejecución.  
  
    El modo predeterminado es **error**.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </output-providers>  
    ```  
    *o*  
  
    ```xml  
    <!-- Connect to target database -->  
  
    <connect-target-database server="<target-server-unique-name>">  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </connect-target-database>  
    ```  
  
4.  **Volver a conectar el proveedor:** Esto permite al usuario establecer la reconexión proporcionar configuración de errores de conexión. Esto se puede establecer para servidores de origen y destino.  
  
    Los modos de reconexión son:  
  
    -   volver a conectarse-a-última-usa-server: si la conexión no está activa, intenta volver a conectarse hasta el último servidor que se usa al menos 5 veces.  
  
    -   generar un error: si la conexión no está activa, se genera un error.  
  
    El modo predeterminado es **generar un error**.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <reconnect-manager on-source-reconnect="<reconnect-to-last-used-server/generate-an-error>"  
  
                         on-target-reconnect="<reconnect-to-last-used-server/generate-an-error>"/>  
  
    </output-providers>  
    ```  
    *o*  
  
    ```xml  
    <!--synchronization-->  
  
    <synchronize-target>  
  
      <reconnect-manager on-target-reconnect="reconnect-to-last-used-server"/>  
  
    </synchronize-target>  
    ```  
    *o*  
  
    ```xml  
    <!--data migration-->  
  
    <migrate-data server="<target-server-unique-name>">  
  
      <reconnect-manager  
  
        on-source-reconnect="reconnect-to-last-used-server"  
  
        on-target-reconnect="generate-an-error"/>  
  
    </migrate-data>  
    ```  
  
5.  **Proveedor de sobrescritura de convertidor:** Esto permite al usuario controlar los objetos que ya están presentes en el destino de la metabase. Las acciones posibles incluyen:  
  
    -   Error: la consola mostrará un error y detiene la ejecución.  
  
    -   sobrescribir: sobrescribe los valores de objeto existentes. Esta acción se realiza de forma predeterminada.  
  
    -   Omitir: la consola omite los objetos que ya existen en la base de datos  
  
    -   usuario pida: pide al usuario para la entrada ('Sí' / 'no')  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </output-providers>  
    ```  
    *o*  
  
    ```xml  
    <convert-schema object-name="<object-name>">  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </convert-schema>  
    ```  
  
6.  **Error de requisitos previos de proveedor:** Esto permite al usuario controlar todos los requisitos previos necesarios para procesar un comando. De forma predeterminada, el modo strict es 'false'. Si se establece en 'true', una excepción se genera para que si no se cumplen los requisitos previos.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true/false>"/>  
  
    </output-providers>  
    ```  
  
7.  **Operación de detención:** durante la operación intermedia, si el usuario desea detener la operación, a continuación, **'Ctrl + C'** se puede utilizar la tecla de acceso rápido. SSMA para la consola de Oracle se va a esperar a que finalice la operación y finaliza la ejecución de la consola.  
  
    Si el usuario desea detener la ejecución inmediatamente, a continuación, **'Ctrl + C'** teclas de acceso rápido pueden presionarse nuevo para la terminación repentina de la aplicación de consola SSMA.  
  
8.  **Proveedor de progreso:** informa del progreso de cada comando de la consola. Esto está deshabilitada de forma predeterminada. Los atributos de informes de progreso comprenden:  
  
    -   off  
  
    -   cada 1%  
  
    -   cada 2%  
  
    -   cada 5%  
  
    -   cada 10%  
  
    -   cada 20%  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <progress-reporting enable="<true/false>"            (optional)  
  
                          report-messages="<true/false>"   (optional)  
  
                          report-progress="every-1%/every-2%/every-5%/every-10%/every-20%/off" (optional)/>  
  
    </output-providers>  
    ```  
    *o*  
  
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
  
    -   Error: se registran solo los mensajes de error y error irrecuperable.  
  
    -   Advertencia: se registran todos los niveles excepto los mensajes de depuración y la información.  
  
    -   Info: todos los niveles salvo que se registran los mensajes de depuración.  
  
    -   depurar: todos los niveles de los mensajes registrados.  
  
    > [!NOTE]  
    > Obligatorios mensajes se registran en cualquier nivel.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </output-providers>  
    ```  
    *o*  
  
    ```xml  
    <…All commands…>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </…All commands…>  
    ```  
  
10. **Contraseña de cifrado de invalidación:** si es 'true', la contraseña de texto no cifrado especificado en la sección de definición de servidor del archivo de conexión del servidor o en el archivo de script, invalida la contraseña cifrada que se almacenan en el almacenamiento protegido si ya existe. Si se especifica ninguna contraseña en texto no cifrado, se solicita al usuario que escriba la contraseña.  
  
    Aquí surgen dos casos:  
  
    1.  Si invalidar la opción es **false**, el orden de búsqueda estarán protegidos almacenamiento -&gt;archivo de Script -&gt;archivo de conexión de servidor -&gt; preguntar al usuario.  
  
    2.  Si reemplaza la opción es **true**, será el orden de búsqueda de archivo de Script -&gt;archivo de conexión de servidor -&gt;preguntar al usuario.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
La opción no configurable es:  
  
-   **Número máximo de intentos de reconexión:** cuando una conexión establecida se agota el tiempo o se interrumpe deba a errores de red, el servidor es necesario volver a conectarse. Se permiten los intentos de reconexión hasta un máximo de **5** reintentos transcurrido ese período, la consola realiza automáticamente la reconexión. La funcionalidad de reconexión automática reduce el esfuerzo de volver a ejecutar la secuencia de comandos.  
  
## <a name="server-connection-parameters"></a>Parámetros de conexión de servidor  
Parámetros de conexión de servidor pueden definirse en el archivo de script o en el archivo de conexión de servidor. Consulte la [crear los archivos de conexión de servidor &#40; OracleToSQL &#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md) sección para obtener más detalles.  
  
## <a name="script-commands"></a>Comandos de script  
El archivo de script contiene una secuencia de comandos de flujo de trabajo de migración en el formato XML. La aplicación de consola SSMA procesa la migración en el orden de los comandos que aparecen en el archivo de script.  
  
Por ejemplo, una migración típica de datos de una tabla específica en una base de datos de Oracle sigue la jerarquía de: esquema -&gt; tabla.  
  
Cuando todos los comandos en el archivo de script se ejecuta correctamente, la aplicación de consola SSMA sale y devuelve el control al usuario. El contenido de un archivo de script es más o menos estático con información sobre las variable contenidas en una [crear archivos de valores de Variable &#40; OracleToSQL &#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md) o, en una sección independiente dentro del archivo de script para los valores de las variables.  
  
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
Se proporcionan plantillas que consta de 3 archivos de script (para la ejecución de varios escenarios), archivo de valores de variable y un archivo de conexión de servidor en la carpeta de secuencias de comandos de consola de ejemplo del directorio del producto:  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
Puede ejecutar las plantillas (archivos) después de cambiar los parámetros que aparecen en él para relevancia.  
  
Lista completa de los comandos de script puede encontrarse en [ejecutando la consola SSMA &#40; OracleToSQL &#41;](../../ssma/oracle/executing-the-ssma-console-oracletosql.md)  
  
## <a name="script-file-validation"></a>Validación del archivo de script  
El usuario puede validar fácilmente su archivo de script en el archivo de definición de esquema **'O2SSConsoleScriptSchema.xsd'** disponible en la carpeta 'Esquemas'.  
  
## <a name="next-step"></a>Paso siguiente  
El siguiente paso en la utilización de la consola es [crear archivos de valores Variable &#40; OracleToSQL &#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md).  
  
## <a name="see-also"></a>Vea también  
[Crear archivos de valor de la Variable &#40; OracleToSQL &#41;](../../ssma/oracle/creating-variable-value-files-oracletosql.md)  
  
