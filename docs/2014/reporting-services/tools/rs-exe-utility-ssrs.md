---
title: Utilidad RS.exe (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- automatic report server tasks
- rs utility
- command prompt utilities [Reporting Services]
- report servers [Reporting Services], automating tasks
- command prompt utilities [SQL Server], rs
- scripts [Reporting Services], command prompt
- deploying reports [Reporting Services]
ms.assetid: bd6f958f-cce6-4e79-8a0f-9475da2919ce
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a6c4bf8f67f787214d38148db40ea8122a064a42
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099826"
---
# <a name="rsexe-utility-ssrs"></a>Utilidad RS.exe (SSRS)
  La utilidad rs.exe procesa el script que proporcione en un archivo de entrada. Use esta utilidad para automatizar las tareas de implementación y administración del servidor de informes.  
  
> [!NOTE]  
>  A partir de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], la utilidad **rs** se admite con los servidores de informes configurados para el modo integrado de SharePoint, así como para los servidores configurados en modo nativo. Las versiones anteriores solo eran compatibles con las configuraciones del modo nativo.  
  
 **En este tema:**  
  
-   [Ubicación del archivo](#bkmk_filelocation)  
  
-   [Argumentos](#bkmk_arguments)  
  
-   [Permisos](#bkmk_permissions)  
  
-   [Ejemplos](#bkmk_examples)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
      rs {-?}  
{-i input_file=}  
{-s serverURL}  
{-u username}  
{-p password}  
{-e endpoint}  
{-l time_out}  
{-b batchmode}  
{-v globalvars=}  
{-t trace}  
```  
  
##  <a name="file-location"></a><a name="bkmk_filelocation"></a> Ubicación del archivo  
 **RS.exe** se encuentra en **\Archivos de programa\Microsoft SQL Server\110\Tools\Binn**. Puede ejecutar la utilidad desde cualquier carpeta del sistema de archivos.  
  
##  <a name="arguments"></a><a name="bkmk_arguments"></a>Argumentos  
 **-?**  
 (Opcional) Muestra la sintaxis de los argumentos de **rs** .  
  
 `-i`*input_file*  
 (Obligatorio) Especifica el archivo .rss que debe ejecutarse. Este valor puede ser una ruta de acceso relativa o una ruta de acceso completa al archivo .rss.  
  
 `-s`*ServerURL*  
 (Obligatorio) Especifica el nombre del servidor web y el nombre del directorio virtual del servidor de informes donde debe ejecutarse el archivo. Un ejemplo de una dirección URL de un servidor de informes es `http://examplewebserver/reportserver`. El prefijo http:// o https:// al principio del nombre del servidor es opcional. Si se omite el prefijo, el host de script del servidor de informes intentará usar primero https y, después, http si https no funciona.  
  
 `-u`[*dominio*\\] *nombre de usuario*  
 (Opcional) Especifica una cuenta de usuario que se utiliza para conectarse al servidor de informes. Si se omiten `-u` y `-p`, se usa la cuenta de usuario actual de Windows.  
  
 `-p`*contraseña* de  
 (Obligatorio si se especifica `-u`) Especifica la contraseña que debe utilizarse con el argumento `-u`. Este valor distingue mayúsculas de minúsculas.  
  
 `-e`  
 (Opcional) Especifica el extremo SOAP en el que debe ejecutarse el script. Los valores válidos son los siguientes:  
  
-   Mgmt2010  
  
-   Mgmt2006  
  
-   Mgmt2005  
  
-   Exec2005  
  
 Si no se especifica ningún valor, se utilizará el extremo Mgmt2005. Para obtener más información acerca de los extremos SOAP, vea [Report Server Web Service Endpoints](../report-server-web-service/methods/report-server-web-service-endpoints.md).  
  
 `-l`*time_out*  
 Opta Especifica el número de segundos que transcurren antes de que se agote el tiempo de espera de la conexión al servidor. El valor predeterminado es 60 segundos. Si no se especifica ningún valor de tiempo de espera, se utiliza el valor predeterminado. El valor `0` indica que nunca se agota el tiempo de espera de la conexión.  
  
 **-b**  
 (Opcional) Especifica que los comandos del archivo de script se ejecutan en un lote. Si se produce un error en alguno de los comandos, se revierte el lote. Algunos comandos no se pueden ejecutar por lotes y se ejecutan de la manera habitual. Solo si se producen excepciones que no se controlan dentro del script tiene lugar una operación de reversión. Si el script controla una excepción y vuelve con normalidad desde `Main`, se confirma el lote. Si omite este parámetro, los comandos se ejecutan sin crear un lote. Para obtener más información, consulte [Batching Methods](../report-server-web-service-net-framework-soap-headers/batching-methods.md).  
  
 `-v` *globalvar*  
 (Opcional) Especifica las variables globales que se usan en el script. Si el script utiliza variables globales, debe especificar este argumento. El valor que especifique debe ser válido para la variable global definida en el archivo .rss. Debe especificar una variable global para cada argumento **-v** .  
  
 El argumento `-v` se especifica en la línea de comandos y se usa para establecer el valor de una variable global que se define en el script en tiempo de ejecución. Por ejemplo, si el script contiene una variable con nombre *parentFolder*, puede especificar un nombre para dicha carpeta en la línea de comandos:  
  
 `rs.exe -i myScriptFile.rss -s http://myServer/reportserver -v parentFolder="Financial Reports"`  
  
 Se crean variables globales con los nombres indicados y se establecen en los valores proporcionados. Por ejemplo, **-v a =**"`1`" **-v b =**"`2`" da como resultado una variable `a` denominada con un valor de`1`"" y una variable **b** con un valor de`2`"".  
  
 Las variables globales están disponibles para todas las funciones del script. Una barra diagonal inversa y Comillas (**\\"**) se interpretan como comillas dobles. Las comillas solo son necesarias si la cadena contiene un espacio. Los nombres de variable deben ser [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]válidos para; deben empezar por un carácter alfabético o un carácter de subrayado y contener caracteres alfabéticos, dígitos o caracteres de subrayado. No se pueden utilizar palabras reservadas como nombres de variables. Para más información sobre las variables globales, vea [Colecciones integradas en expresiones &#40;Generador de informes y SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
 **-t**  
 (Opcional) Muestra mensajes de error en el registro de seguimiento. Este argumento no toma ningún valor. Para obtener más información, consulte [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md).  
  
##  <a name="permissions"></a><a name="bkmk_permissions"></a> Permisos  
 Para ejecutar la herramienta, debe tener permiso para conectarse a la instancia del servidor de informes en la que se está ejecutando el script. Puede ejecutar scripts para realizar cambios en el equipo local o en un equipo remoto. Para realizar cambios en un servidor de informes instalado en un equipo remoto, especifique el equipo remoto en el argumento `-s`.  
  
##  <a name="examples"></a><a name="bkmk_examples"></a> Ejemplos  
 En el ejemplo siguiente se muestra cómo especificar el archivo de script que contiene el script de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET y los métodos del servicio Web que se desea ejecutar.  
  
```  
rs -i c:\scriptfiles\script_copycontent.rss -s http://localhost/reportserver  
```  
  
 Para obtener un ejemplo detallado, vea [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
 Para ver otros ejemplos, vea [Ejecutar un archivo de script de Reporting Services](run-a-reporting-services-script-file.md).  
  
## <a name="remarks"></a>Observaciones  
 Puede definir scripts para establecer propiedades del sistema, publicar informes, etc. Los scripts que crea pueden incluir cualquier método de la API [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información sobre los métodos y las propiedades disponibles, vea [Report Server Web Service](../report-server-web-service/report-server-web-service.md).  
  
 Es necesario escribir el script en código de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .NET y guardarlo en un archivo de texto Unicode o UTF-8 con la extensión de nombre de archivo .rss. No se pueden depurar scripts mediante la utilidad **rs** . Para depurar un script, ejecute el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]código dentro de.  
  
> [!TIP]  
>  Para obtener un ejemplo detallado, vea [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar un archivo de script de Reporting Services](run-a-reporting-services-script-file.md)   
 [Crear script de tareas administrativas y de implementación](script-deployment-and-administrative-tasks.md)   
 [Script con la utilidad RS. exe y el servicio Web](script-with-the-rs-exe-utility-and-the-web-service.md)   
 [Utilidades del símbolo del sistema del servidor de informes &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)  
  
  
