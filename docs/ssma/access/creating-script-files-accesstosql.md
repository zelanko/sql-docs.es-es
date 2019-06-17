---
title: Creación de archivos de Script (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 64dfe192-965c-49d4-a3ea-848fbc5f619f
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 5258a95b713da0ec1fe526e94ce11c6e5e0b595c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63138777"
---
# <a name="creating-script-files-accesstosql"></a>Creación de archivos de script (AccessToSQL)
El primer paso antes de iniciar la aplicación de consola SSMA crear el archivo de script y si es necesario crear el archivo de valor de la variable y el archivo de conexión de servidor.  
  
El archivo de script puede dividirse en tres secciones viz..,:  
  
1.  **config:** Permite al usuario establecer los parámetros de configuración para la aplicación de consola.  
  
2.  **servers:** Permite al usuario establecer el origen o destino de las definiciones de servidor. Esto también puede estar en un archivo de conexión de servidor independiente.  
  
3.  **script-commands:** Permite al usuario ejecutar comandos de flujo de trabajo SSMA.  
  
Cada sección se describe en detalle a continuación:  
  
## <a name="configuring-access-console-settings"></a>Configuración de la consola de acceso  
Las configuraciones de una secuencia de comandos se muestran en el archivo de script de la consola.  
  
Si cualquiera de los elementos se especifican en el nodo de configuración, se establecen como la configuración global, es decir, son aplicables a todos los comandos de script. Estos elementos de configuración también pueden establecerse dentro de cada comando en la sección de la secuencia de comandos si el usuario desea invalidar la configuración global.  
  
Las opciones configurables por el usuario incluyen:  
  
1.  **Proveedor de la ventana de salida:** Si los mensajes suprimir está establecido en 'true', la específica del comando no se muestran mensajes en la consola. La descripción de los atributos se indica a continuación:  
  
    -   destino: Especifica si la salida se debe imprimir a un archivo o stdout. Se trata de un valor predeterminado es false.  
  
    -   file-name: La ruta de acceso del archivo (opcional).  
  
    -   Suprimir-messages: Suprime los mensajes en la consola. Esto es 'false', de forma predeterminada.  
  
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
    *o Administrador de configuración de*  
  
    ```xml  
    <...All commands...>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </...All commands...>  
    ```  
  
2.  **Proveedor de conexión de la migración de datos:** Esto especifica que el servidor de origen o destino es para considerarse para la migración de datos.  Origen-use-último uso indica que se utiliza el último servidor de origen usados para la migración de datos. Del mismo modo destino-use-último uso indica que se utiliza el último servidor de destino usada para la migración de datos. El usuario también puede especificar el servidor (origen o destino) mediante el uso de los atributos de servidor de origen o el servidor de destino.  
  
    Puede usarse, es decir, solo uno o el otro atributo especificado:  
  
    - origen-use-último uso = "true" (valor predeterminado) o servidor de origen = "source_servername"  
  
    - destino-use-último uso = "true" (valor predeterminado) o servidor de destino = "target_servername"  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <data-migration-connection   source-use-last-used="true"  
  
                                   target-server="target_1"/>  
  
    </output-providers>  
    ```  
    *o Administrador de configuración de*  
  
    ```xml  
    <migrate-data>  
  
      <data-migration-connection   source-server="source_1"  
  
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
    *o Administrador de configuración de*  
  
    ```xml  
    <!-- Connect to target database -->  
  
    <connect-target-database server="target_0">  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </connect-target-database>  
    ```  
  
4.  **Volver a conectar el proveedor:** Esto permite al usuario establecer la configuración de reconexión en el caso de errores de conexión. Esto se puede establecer para servidores de origen y destino.  
  
    Los modos de reconexión son:  
  
    -   reconnect-to-last-used-server: Si la conexión no está activa, intenta volver a conectarse hasta el último servidor que se usa como máximo 5 veces.  
  
    -   generar una-error: Si la conexión no está activa, se genera un error.  
  
    El modo predeterminado es **generar un error**.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
     <reconnect-manager on-source-reconnect="<reconnect-to-last-used-server/generate-an-error>"  
  
                        on-target-reconnect="<reconnect-to-last-used-server/generate-an-error>"/>  
  
    </output-providers>  
    ```  
    *o Administrador de configuración de*  
  
    ```xml  
    <!--synchronization-->  
  
    <synchronize-target>  
  
      <reconnect-manager on-target-reconnect="reconnect-to-last-used-server"/>  
  
    </synchronize-target>  
    ```  
    *o Administrador de configuración de*  
  
    ```xml  
    <!--data migration-->  
  
    <migrate-data server="target_0">  
  
      <reconnect-manager  
  
        on-source-reconnect="reconnect-to-last-used-server"  
  
        on-target-reconnect="generate-an-error"/>  
  
    </migrate-data>  
    ```  
  
5.  **Convertidor de sobrescritura proveedor:** Esto permite al usuario controlar los objetos que ya están presentes en el destino de la metabase. Las posibles acciones incluyen:  
  
    -   error: La consola muestra un error y detiene la ejecución.  
  
    -   overwrite: Sobrescribe los valores de objeto existentes. Esta acción se realiza de forma predeterminada.  
  
    -   Omitir: La consola omite los objetos que ya existen en la base de datos  
  
    -   ask-user: Pide al usuario para la entrada ("Sí" o "no")  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <object-overwrite action="<error|skip|overwrite|ask-user>"/>  
  
    </output-providers>  
    ```  
    *o Administrador de configuración de*  
  
    ```xml  
    <convert-schema object-name="ssma.TT1">  
  
      <object-overwrite action="<error|skip|overwrite|ask-user>"/>  
  
    </convert-schema>  
    ```  
  
6.  **Proveedor con errores de requisitos previos:** Esto permite al usuario controlar los requisitos previos que son necesarios para procesar un comando. De forma predeterminada, el modo strict es 'false'. Si se establece en 'true', una excepción se genera si hay errores a cumplir los requisitos previos.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true|false>"/>  
  
    </output-providers>  
    ```  
  
7.  **Detener la operación:** Durante la operación intermedio, si el usuario desea detener la operación, a continuación, **'Ctrl + C'** se puede usar la tecla de acceso rápido. SSMA para Access consola esperará a que se complete la operación y finaliza la ejecución de la consola.  
  
    Si el usuario desea detener la ejecución inmediatamente, a continuación, **'Ctrl + C'** pueden presionar teclas de acceso rápido nuevo para la terminación repentina de la aplicación de consola de SSMA.  
  
8.  **Proveedor de progreso:** Informa del progreso de cada comando de la consola. Esta opción está deshabilitada de forma predeterminada. Constan de los atributos de informes de progreso:  
  
    -   off  
  
    -   cada 1%  
  
    -   una de las 2%  
  
    -   una de las 5%  
  
    -   una de las 10%  
  
    -   una de las 20%  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
     <progress-reporting enable="<true|false>"           (optional)  
  
                         report-messages="<true|false>"  (optional)  
  
                         report-progress="every-1%|every-2%|every-5%|every-10%|every-20%|off" (optional)/>  
  
    </output-providers>  
    ```  
    *o Administrador de configuración de*  
  
    ```xml  
    <...All commands...>  
  
      <progress-reporting  
  
        enable="<true|false>"              (optional)  
  
        report-messages="<true|false>"     (optional)  
  
        report-progress="every-1%|every-2%|every-5%|every-10%|every-20%|off"     (optional)/>  
  
    </...All commands...>  
    ```  
  
9. **Nivel de detalle del registrador:** Conjuntos de nivel de detalle de registro. Esto se corresponde con la opción de todas las categorías en la interfaz de usuario. De forma predeterminada, el nivel de detalle de registro es "error".  
  
    Las opciones de nivel de registrador incluyen:  
  
    -   fatal-error: Solo los mensajes de error irrecuperable se registran.  
  
    -   error: Solo los mensajes de error y fatal error se registran.  
  
    -   Advertencia: Todos los niveles, salvo que se registran los mensajes de depuración e información.  
  
    -   info: Se registran todos los niveles, excepto los mensajes de depuración.  
  
    -   Depurar: Todos los niveles de los mensajes registrados.  
  
    > [!NOTE]  
    > Se registran mensajes obligatorios en cualquier nivel.  
  
    **Ejemplo:**  
  
    ```xml  
    <output-providers>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </output-providers>  
    ```  
    *o Administrador de configuración de*  
  
    ```xml  
    <...All commands...>  
  
      <log-verbosity level="fatal-error/error/warning/info/debug"/>  
  
    </...All commands...>  
    ```  
  
10. **Reemplace la contraseña cifrada:** Si es 'true', la contraseña de texto no cifrado especificado en la sección de definición de servidor del archivo de conexión del servidor o en el archivo de script, invalidaciones de la contraseña cifrada almacenada en un almacenamiento protegido, si existe. Si se especifica ninguna contraseña en texto no cifrado, se solicita al usuario que escriba la contraseña.  
  
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
  
-   **Máximo de intentos de conexión:** Cuando una conexión establecida se agota el tiempo o se interrumpe debido a un error de red, es necesario para volver a conectar el servidor. Se permiten los intentos de reconexión a un máximo de **5** reintentos después de eso, la consola realiza automáticamente la reconexión. La instalación de la reconexión automática reduce el esfuerzo de volver a ejecutar el script.  
  
## <a name="server-connection-parameters"></a>Parámetros de conexión del servidor  
Parámetros de conexión de servidor pueden definirse en el archivo de script o en el archivo de conexión de servidor. Consulte la [crear los archivos de conexión de servidor &#40;AccessToSQL&#41; ](../../ssma/access/creating-the-server-connection-files-accesstosql.md) sección para obtener más detalles.  
  
## <a name="script-commands"></a>Comandos de script  
El archivo de script contiene una secuencia de comandos de flujo de trabajo de migración en formato XML. La aplicación de consola SSMA procesa la migración en el orden de los comandos que aparecen en el archivo de script.  
  
Por ejemplo, una migración de datos típica de una tabla específica en una base de datos de Access sigue la jerarquía de: Base de datos -&gt; tabla.  
  
Cuando todos los comandos en el archivo de script se ejecuta correctamente, la aplicación de consola SSMA sale y devuelve el control al usuario. El contenido de un archivo de script es más o menos estático con información sobre las variable contenidas en un [archivos de valores de Variable](creating-variable-value-files-accesstosql.md) o, en una sección independiente dentro del archivo de script para los valores de variable.  
  
**Ejemplo:**  
  
```xml  
<!--Sample of script file commands -->  
  
<ssma-script-file>  
  
  <script-commands>  
  
    <create-new-project project-folder="$project_folder$"  
  
                        project-name="$project_name$"  
  
                        overwrite-if-exists="true"/>  
  
    <connect-source-database server="source_2"/>  
  
    <save-project/>  
  
    <close-project/>  
  
  </script-commands>  
  
</ssma-script-file>  
```  
Se proporcionan plantillas que consta de 3 archivos de script (para ejecutar varios escenarios), archivo de valores de variable y un archivo de conexión de servidor en la carpeta de Scripts de la consola de ejemplo del directorio del producto:  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
Puede ejecutar las plantillas (archivos) después de cambiar los parámetros que aparecen en ella por su gran relevancia.  
  
Encontrará una lista completa de comandos de script en [ejecutando la consola de SSMA &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="script-file-validation"></a>Validación del archivo de script  
El usuario puede validar fácilmente su archivo de script en el archivo de definición de esquema **'A2SSConsoleScriptSchema.xsd'** disponible en la carpeta "Esquemas".  
  
## <a name="next-step"></a>Paso siguiente
El siguiente paso en el funcionamiento de la consola es [crear archivos de valor Variable &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md).  
  
## <a name="see-also"></a>Vea también  
[Creación de archivos de valor Variable &#40;AccessToSQL&#41;](../../ssma/access/creating-variable-value-files-accesstosql.md)  
  
