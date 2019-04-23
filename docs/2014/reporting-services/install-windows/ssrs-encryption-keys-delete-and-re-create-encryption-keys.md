---
title: Eliminar y volver a crear claves de cifrado (Administrador de configuración de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- re-creating encryption keys
- encryption keys [Reporting Services]
- deleting encryption keys
- symmetric keys [Reporting Services]
- removing encryption keys
- resetting encryption keys
ms.assetid: 201afe5f-acc9-4a37-b5ec-121dc7df2a61
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 38547a2d48ecbe1887702d7be9b45b3166d75243
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59952441"
---
# <a name="delete-and-re-create-encryption-keys--ssrs-configuration-manager"></a>Eliminar y volver a crear claves de cifrado (Administrador de configuración de SSRS)
  Las actividades de eliminación y nueva creación de claves de cifrado quedan fuera del mantenimiento rutinario de las claves de cifrado. Estas tareas se realizan en respuesta a una amenaza específica al servidor de informes o como último recurso cuando ya no se tiene acceso a una base de datos del servidor de informes.  
  
-   Vuelva a crear la clave simétrica cuando crea que la existente está en riesgo. También puede volver a crearla con una frecuencia determinada, como práctica recomendada de seguridad.  
  
-   Elimine claves de cifrado existentes y el contenido cifrado no utilizable cuando no pueda restaurar la clave simétrica.  
  
## <a name="re-creating-encryption-keys"></a>volver a crear claves de cifrado  
 Si tiene pruebas de que hay usuarios no autorizados que conocen la clave simétrica, o si el servidor de informes ha sufrido algún ataque y desea restablecer la clave simétrica como medida de precaución, puede volver a crearla. Cuando se vuelve a crear la clave simétrica, todos los valores cifrados se cifran de nuevo con este valor. Si se ejecutan varios servidores de informes en una implementación escalada, todas las copias de la clave simétrica se actualizan con el nuevo valor. El servidor de informes utiliza las claves públicas disponibles para actualizar la clave simétrica en cada servidor de la implementación.  
  
 Solo se puede volver a crear la clave simétrica cuando el servidor de informes se encuentre en un estado de funcionamiento. La creación de claves de cifrado y el cifrado de contenido interrumpen las operaciones del servidor. Debe poner el servidor en modo sin conexión durante el proceso de nuevo cifrado. No se deben realizar solicitudes al servidor de informes durante este proceso.  
  
 Para restablecer la clave simétrica y los datos cifrados, se puede usar la herramienta de configuración de Reporting Services o la utilidad **rskeymgmt** . Para obtener más información sobre cómo se crea la clave simétrica, vea [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](ssrs-encryption-keys-initialize-a-report-server.md).  
  
#### <a name="how-to-re-create-encryption-keys-reporting-services-configuration-tool"></a>Cómo volver a crear claves de cifrado (herramienta de configuración de Reporting Services)  
  
1.  Deshabilite el acceso HTTP y el servicio web del servidor de informes modificando la propiedad `IsWebServiceEnabled` en el archivo rsreportserver.config. Este paso evita temporalmente que las solicitudes de autenticación se envíen al servidor de informes sin cerrar el servidor completamente. Debe tener el servicio mínimo para poder volver a crear las claves.  
  
     Si vuelve a crear claves de cifrado para una implementación escalada del servidor de informes, deshabilite esta propiedad en todas las instancias de la implementación.  
  
    1.  Abra el Explorador de Windows y navegue a *unidad*:\Archivos de programa\Microsoft SQL Server\\*instancia_servidor_informes*\Reporting Services. Reemplace *unidad* por su letra de unidad e *instancia_servidor_informes* por el nombre de carpeta que corresponde a la instancia del servidor de informes para la que quiere deshabilitar el acceso HTTP y el servicio web. Por ejemplo, C:\Archivos de programa\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services.  
  
    2.  Abra el archivo rsreportserver.config.  
  
    3.  Para la propiedad `IsWebServiceEnabled`, especifique `False` y, a continuación, guarde los cambios.  
  
2.  Inicie la herramienta de configuración de Reporting Services y, a continuación, conéctese a la instancia del servidor de informes que desea configurar.  
  
3.  En la página Claves de cifrado, haga clic en **Cambiar**. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Reinicie el servicio Servidor de informes de Windows. Si vuelve a crear claves de cifrado para una implementación escalada, reinicie el servicio en todas las instancias.  
  
5.  Vuelva a habilitar el acceso HTTP y el servicio web modificando la propiedad `IsWebServiceEnabled` en el archivo rsreportserver.config. Hágalo para todas las instancias si está trabajando con una implementación escalada.  
  
#### <a name="how-to-re-create-encryption-keys-rskeymgmt"></a>Cómo volver a crear claves de cifrado (rskeymgmt)  
  
1.  Deshabilite el acceso HTTP y el servicio web del servidor de informes. Siga las instrucciones del procedimiento anterior para detener las operaciones de los servicios web.  
  
2.  Ejecute **rskeymgmt.exe** localmente en el equipo que hospeda el servidor de informes. Utilice el argumento `-s` para restablecer la clave simétrica. No se requieren más argumentos:  
  
    ```  
    rskeymgmt -s  
    ```  
  
3.  Reinicie el servicio Windows y habilite las operaciones de los servicios web.  
  
## <a name="deleting-unusable-encrypted-content"></a>Eliminar contenido cifrado que no pueda utilizarse  
 Si, por algún motivo, no puede restaurar la clave de cifrado, el servidor de informes nunca podrá descifrar ni utilizar los datos que se hayan cifrado con esa clave. Para devolver al servidor de informes a un estado de funcionamiento, se deben eliminar los valores cifrados almacenados actualmente en la base de datos del servidor de informes y después, volver a especificar manualmente los valores que se necesiten.  
  
 La eliminación de las claves de cifrado provoca la supresión de toda información de clave simétrica de la base de datos del servidor de informes y elimina todo el contenido cifrado. Los datos no cifrados permanecen intactos; solo se suprime el contenido cifrado. Cuando se eliminan las claves de cifrado, el servidor de informes se reinicializa automáticamente agregando una nueva clave simétrica. Cuando se elimina el contenido cifrado, ocurre lo siguiente:  
  
-   Se eliminan las cadenas de conexión en orígenes de datos compartidos. Los usuarios que ejecutan informes obtienen el error "No se inicializó la propiedad ConnectionString".  
  
-   Se eliminan las credenciales almacenadas. Los informes y los orígenes de datos compartidos se reconfiguran para que utilicen credenciales solicitadas.  
  
-   No se pueden ejecutar los informes que se basan en modelos (y que requieren orígenes de datos compartidos configurados con credenciales almacenadas o sin ninguna credencial).  
  
-   Las suscripciones se desactivan.  
  
 Una vez eliminado el contenido cifrado, ya no es posible recuperarlo. Se deben volver a especificar cadenas de conexión y credenciales almacenadas, y es necesario activar las suscripciones.  
  
 Para quitar los valores, se puede usar la herramienta de configuración de Reporting Services o la utilidad **rskeymgmt** .  
  
#### <a name="how-to-delete-encryption-keys-reporting-services-configuration-tool"></a>Cómo eliminar claves de cifrado (herramienta de configuración de Reporting Services)  
  
1.  Inicie la herramienta de configuración de Reporting Services y, a continuación, conéctese a la instancia del servidor de informes que desea configurar.  
  
2.  Haga clic en **Claves de cifrado**y, a continuación, en **Eliminar**. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Reinicie el servicio Servidor de informes de Windows. En una implementación escalada, repita el procedimiento con todas las instancias del servidor de informes.  
  
#### <a name="how-to-delete-encryption-keys-rskeymmgt"></a>Cómo eliminar claves de cifrado (rskeymmgt)  
  
1.  Ejecute **rskeymgmt.exe** localmente en el equipo que hospeda el servidor de informes. Debe usar el argumento de aplicación **-d** . El siguiente ejemplo ilustra el argumento que debe especificar:  
  
    ```  
    rskeymgmt -d  
    ```  
  
2.  Reinicie el servicio Servidor de informes de Windows. En una implementación escalada, repita el procedimiento con todas las instancias del servidor de informes.  
  
#### <a name="how-to-re-specify-encrypted-values"></a>Cómo volver a especificar valores cifrados  
  
1.  En cada origen de datos compartido se debe volver a escribir la cadena de conexión.  
  
2.  Para cada informe y origen de datos compartido que utilice credenciales almacenadas, debe volver a escribir el nombre de usuario y la contraseña y luego guardarlos. Para obtener más información, vea [Especificar información de credenciales y conexión para los orígenes de datos de informes](../../integration-services/connection-manager/data-sources.md) en Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3.  Para cada suscripción controlada por datos, ábrala y vuelva a escribir las credenciales de la base de datos de suscripciones.  
  
4.  Para suscripciones que utilizan datos cifrados (como la extensión de entrega de recurso compartido de archivos y todas las extensiones de entrega de terceros que utilicen cifrado), abra cada suscripción y vuelva a escribir las credenciales. Las suscripciones que usan entrega por correo electrónico del Servidor de informes no emplean datos cifrados y, por tanto, no les afecta el cambio de clave.  
  
## <a name="see-also"></a>Vea también  
 [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](ssrs-encryption-keys-manage-encryption-keys.md)   
 [Almacenar datos cifrados del servidor de informes &#40;Administrador de configuración de SSRS&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
