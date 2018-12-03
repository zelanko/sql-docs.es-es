---
title: Utilidad rskeymgmt (SSRS) | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], encryption
- joining report server instances [SQL Server]
- report server scale-out deployments [Reporting Services]
- cryptography [Reporting Services]
- multiple report server instances
- command prompt utilities [Reporting Services]
- report servers [Reporting Services], scale-out deployments
- encryption [Reporting Services]
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 53f1318d-bd2d-4c08-b19f-c8b698b5b3d3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8d6d83624fc47a12387e2edf02381faa3cfaedcf
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52545370"
---
# <a name="rskeymgmt-utility-ssrs"></a>rskeymgmt (utilidad) (SSRS)
  Extrae, restaura, crea y elimina la clave simétrica usada para proteger contra el acceso no autorizado los datos importantes del servidor de informes. Esta utilidad también se usa para unir instancias del servidor de informes en una implementación de ampliación horizontal. Una *implementación escalada del servidor de informes* se refiere a varias instancias del servidor de informes que comparten una sola base de datos de servidor de informes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
rskeymgmt {-?}  
{-eextract}  
{-aapply}  
{-ddeleteall}  
{-srecreatekey}  
{-rremoveinstancekey}  
{-jjoinfarm}  
{-iinstance}  
{-ffile}  
{-pencryptionpassword}  
{-mremotecomputer}  
{-ninstancenameofremotecomputer}  
{-uadministratoruseraccount}  
{-vadministratorpassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>Argumentos  
 **-?**  
 Muestra la sintaxis de los argumentos de **rskeymgmt** .  
  
 **-e**  
 Extrae la clave simétrica que se usa para cifrar y descifrar datos para la instancia del servidor de informes con el fin de copiarlos en un archivo.  
  
 Este argumento no toma ningún valor. Sin embargo, para completar la extracción, es necesario incluir argumentos adicionales en la línea de comandos. Los argumentos que debe especificar son **-f** y **-p**.  
  
 **-a**  
 Reemplaza una clave simétrica existente con una copia proporcionada en un archivo de copia de seguridad protegido mediante contraseña. Todas las instancias de la clave simétrica se actualizan.  
  
 Este argumento no toma ningún valor. Sin embargo, es necesario incluir argumentos adicionales en la línea de comandos para seleccionar el archivo que contiene la clave que va a aplicarse. Los argumentos que puede especificar son **-f** y **-p**.  
  
 **-d**  
 Elimina todas las instancias de la clave simétrica y todos los datos cifrados de una base de datos del servidor de informes. Este argumento no toma ningún valor.  
  
 **-s**  
 Genera una nueva clave simétrica y vuelve a cifrar todo el contenido cifrado utilizando la nueva clave. Todas las instancias de la clave simétrica se vuelven a generar.  
  
 **-j**  
 Configura una instancia del servidor de informes remoto para compartir la base de datos del servidor de informes que la instancia del servidor de informes local usa.  
  
 **-r**  *installationID*  
 Quita la información de clave simétrica de una instancia de servidor de informes concreta y, por lo tanto, quita el servidor de informes de una implementación escalada. *installationID* es un valor de GUID que se puede encontrar en el archivo RSReportserver.config.  
  
 **-f**  *file*  
 Especifica una ruta válida al archivo que almacena una copia de seguridad de las claves simétricas.  
  
 Para **rskeymgmt -e**, la clave simétrica se escribe en el archivo especificado.  
  
 Para **rskeymgmt -a**, el valor de la clave simétrica almacenada en el archivo se aplica a la instancia del servidor de informes.  
  
 **-p**  *password*  
 (Se requiere para **-f**). Especifica la contraseña que se usa para realizar una copia de seguridad o para aplicar una clave simétrica. Este valor no puede estar en blanco.  
  
 **-i**  
 Especifica una instancia del servidor de informes local. Este argumento es opcional si ha instalado el servidor de informes en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predeterminada (el valor predeterminado para **-i** es MSSQLSERVER). Si ha instalado el servidor de informes como una instancia con nombre, se requiere **-i** .  
  
 **-m**  
 Especifica el nombre del equipo remoto que hospeda la instancia del servidor de informes que está uniendo a la implementación de ampliación horizontal del servidor de informes. Utilice el nombre del equipo que lo identifica en la red.  
  
 **-n**  
 Especifica el nombre de la instancia del servidor de informes en un equipo remoto. Este argumento es opcional si ha instalado el servidor de informes en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predeterminada (el valor predeterminado para **-n** es MSSQLSERVER). Si ha instalado el servidor de informes como una instancia con nombre, se requiere **-n** .  
  
 **-u**  *useraccount*  
 Especifica la cuenta de administrador del equipo remoto que está combinando con la implementación escalada. Si no se especifica una cuenta, se usan las credenciales del usuario actual.  
  
 **-v**  *password*  
 (Se requiere para **-u**). Especifica la contraseña de una cuenta de administrador del equipo remoto que quiere combinar con la implementación escalada.  
  
 **-t**  *trace*  
 Registra los mensajes de error en el registro de seguimiento. Este argumento no toma ningún valor. Para obtener más información, consulte [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md).  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar esta herramienta, debe ser administrador local y debe hacerlo en el equipo local que hospeda el servidor de informes. La utilidad rskeymgmt funciona con la instancia de Windows Servidor de informes (la utilidad no puede conectar con las instancias remotas del servicio Servidor de informes de Windows y, por lo tanto, no puede usarse para administrar las claves de cifrado de una instancia del servidor de informes remoto).  
  
> [!NOTE]  
>  Si usa los argumentos **-u** y **-v** , asegúrese de especificar una cuenta que tenga permisos de administrador en el equipo remoto.  
  
## <a name="examples"></a>Ejemplos  
 Los siguientes ejemplos muestran algunas formas de usar **rskeymgmt**. Los siguientes ejemplos muestran cómo extraer, restaurar y eliminar claves de cifrado y cómo configurar una implementación escalada del servidor de informes.  
  
#### <a name="extracting-encryption-keys"></a>Extraer claves de cifrado  
 Este ejemplo muestra cómo crear una copia de seguridad de la clave de cifrado y guardarla en un archivo protegido mediante contraseña en un disquete. Si el servidor de informes está instalado como una instancia con nombre, agregue el argumento **-i** .  
  
```  
rskeymgmt -e -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="restoring-encryption-keys"></a>Restaurar claves de cifrado  
 Este ejemplo muestra cómo reemplazar la clave de cifrado. Debe especificar la ubicación de la copia de seguridad de la clave y la contraseña que desbloquea el archivo.  
  
```  
rskeymgmt -a -f a:\backupkey\keys -p <password>  
```  
  
#### <a name="deleting-encryption-keys-and-encrypted-content"></a>Eliminar claves de cifrado y contenido cifrado  
 Este ejemplo muestra cómo eliminar todas las claves de cifrado almacenadas en un servidor de informes. Si la instalación es una implementación de ampliación horizontal del servidor de informes, las claves de cifrado de todas las instancias del servidor de informes que se incluyen en la implementación se eliminarán. Al eliminar una clave de cifrado también se eliminan los valores de cifrado existentes en la base de datos del servidor de informes. Para más información sobre el contenido cifrado, vea [Almacenar datos cifrados del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md).  
  
```  
rskeymgmt -d  
```  
  
#### <a name="joining-a-remote-report-server-named-instance-to-a-scale-out-deployment"></a>Combinar una instancia con nombre del servidor de informes remoto con una implementación de ampliación horizontal  
 Este ejemplo muestra cómo agregar una instancia de servidor de informes que está instalada en un equipo remoto a una implementación de ampliación horizontal del servidor de informes. Debe ejecutar el comando en uno de los equipos que ya está configurado para usar la base de datos compartida. Los argumentos del comando especifican la instancia del servidor de informes remoto que desea combinar con la implementación de ampliación horizontal.  
  
```  
rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
```  
  
> [!NOTE]  
>  Implementación de ampliación horizontal del servidor de informes se refiere a un modelo de implementación en el que varias instancias del servidor de informes comparten la misma base de datos del servidor de informes. Una base de datos del servidor de informes la puede usar cualquier instancia del servidor de informes que almacene sus claves simétricas en la base de datos. Por ejemplo, si una base de datos del servidor de informes contiene información de clave para tres instancias del servidor de informes, las tres instancias se consideran miembros de la misma implementación de ampliación horizontal.  
  
#### <a name="joining-report-server-instances-on-the-same-computer"></a>Combinar instancias del servidor de informes en el mismo equipo  
 Puede crear una implementación escalada a partir de varias instancias del servidor de informes que estén instaladas en el mismo equipo. No establezca los argumentos **-u** y **-v** si va a combinar instancias del servidor de informes que estén instaladas en el equipo local. Los argumentos **-u** y **-v** se usan exclusivamente para combinar instancias desde un equipo remoto. Si especifica los argumentos, recibirá un error que indica que las credenciales de usuario no se pueden utilizar para las conexiones locales.  
  
 El ejemplo siguiente muestra la sintaxis para crear una implementación escalada con varias instancias locales. En este ejemplo, \<**initializedinstance**> es el nombre de una instancia que ya está inicializada para usar la base de datos del servidor de informes y \<**newinstance**> es el nombre de la instancia que quiere agregar a la implementación:  
  
```  
rskeymgmt -j -i <initializedinstance> -m <computer name> -n <newinstance>  
```  
  
#### <a name="removing-encryption-keys-for-a-single-report-server-in-a-scale-out-deployment"></a>Quitar claves de cifrado para un único servidor de informes en una implementación de ampliación horizontal  
 Este ejemplo muestra cómo quitar claves de cifrado de un único servidor de informes en una implementación de ampliación horizontal del servidor de informes. Las claves se quitan de la base de datos del servidor de informes. Cuando se han quitado las claves de la instancia del servidor de informes, esa instancia del servidor de informes ya no puede tener acceso a los datos cifrados de la base de datos, y así se quita de forma efectiva de la implementación de ampliación horizontal.  
  
 Quitar una instancia del servidor de informes de una implementación escalada le exige que especifique un identificador de instalación. El identificador de instalación es un GUID almacenado en el archivo RSReportserver.config de la instancia del servidor de informes para la que desea quitar claves de cifrado. Debe ejecutar el siguiente comando en el equipo que desea quitar de la implementación de ampliación horizontal. Si el servidor de informes está instalado como una instancia con nombre, use el argumento **-i** para especificar la instancia. Para obtener más información, vea [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).  
  
```  
rskeymgmt -r <installationID>  
```  
  
## <a name="file-location"></a>Ubicación del archivo  
 Rskeymgmt.exe se encuentra en **\<*unidad*>:\Archivos de programa\Microsoft SQL Server\110\Tools\Binn** o en **\<*unidad*>:\Archivos de programa (x86)\Microsoft SQL Server\110\Tools\Binn**. Puede ejecutar la utilidad desde cualquier carpeta del sistema de archivos.  
  
## <a name="remarks"></a>Notas  
 El servidor de informes cifra las credenciales almacenadas y la información de la conexión. Para cifrar los datos, se utiliza una clave pública y una clave simétrica. Para que el servidor de informes funcione, la base de datos debe tener claves válidas. Puede usar **rskeymgmt** para realizar una copia de seguridad de las claves, eliminarlas o restaurarlas. Si las claves no se pueden restaurar, esta herramienta proporciona un método para eliminar el contenido cifrado que ya no se pueda usar.  
  
 La utilidad **rskeymgmt** se usa para administrar el conjunto de claves que se define durante la instalación o durante la inicialización. Conecta con el servicio Servidor de informes de Windows local mediante un punto final de llamada a procedimiento remoto (RPC). El servicio Servidor de informes de Windows debe estar en ejecución para que esta utilidad funcione.  
  
 Para más información sobre las claves de cifrado, vea [Configurar y administrar las claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md) e [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md).  
  
## <a name="see-also"></a>Ver también  
 [Configurar una implementación escalada horizontalmente del servidor de informes en modo nativo &#40;Administrador de configuración de SSRS&#41;](https://msdn.microsoft.com/library/4df38294-6f9d-4b40-9f03-1f01c1f0700c)   
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [Utilidades del símbolo del sistema del servidor de informes &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)   
 [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
