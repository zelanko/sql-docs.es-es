---
title: Las claves de cifrado (modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.encryptionkeypanel.F1
ms.assetid: cc7e6f84-80e1-4b5e-9409-d0e074edd147
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 16ac264f89c541f0a864f8b47ed008fa254f181c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095416"
---
# <a name="encryption-keys-ssrs-native-mode"></a>Claves de cifrado (Modo nativo de SSRS)
  Utilice la página Claves de cifrado para administrar la clave simétrica que se usa para cifrar y descifrar datos en un servidor de informes. La administración de las claves de cifrado es una parte importante de la configuración de servidores de informes. La clave simétrica se crea y se aplica automáticamente al crear la base de datos del servidor de informes. Cree una copia de seguridad de la clave simétrica para poder realizar operaciones de mantenimiento rutinarias. Para las siguientes tareas de mantenimiento es necesario tener una copia válida de la clave simétrica:  
  
-   Cambiar la cuenta del servicio Servidor de informes.  
  
-   Migrar una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a un equipo diferente.  
  
-   Configurar una nueva instancia de servidor de informes para compartir o utilizar una base de datos de servidor de informes existente.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Cambiar periódicamente la clave de cifrado de Reporting Services es una práctica recomendada de seguridad. El momento recomendado para cambiar la clave es el inmediatamente posterior a una actualización de versión principal de Reporting Services. Si se cambia la clave después de una actualización se minimiza la interrupción del servicio adicional que ocasiona el cambio de la clave de cifrado de Reporting Services fuera del ciclo de actualización.  
  
 Es necesario restaurar la clave simétrica si se actualizó la cuenta de usuario del servicio Servidor de informes (y se usó una herramienta distinta que el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para cambiar la cuenta) o bien si va a migrar una instalación del servidor de informes a un servidor nuevo.  
  
 Para proteger la clave simétrica contra el acceso no autorizado, se cifra mediante la clave privada del servicio Servidor de informes. Únicamente el servicio Servidor de informes puede desbloquear y usar la clave simétrica para almacenar datos confidenciales en la base de datos del servidor de informes. Si cambia la identidad del servicio Servidor de informes o si se migra el servidor de informes a otro equipo, la clave privada del servicio Servidor de informes ya no podrá desbloquear la clave simétrica. Para restaurar el acceso a la clave simétrica, se debe volver a cifrar con la clave privada de la nueva identidad del servicio Servidor de informes. La restauración de la clave simétrica es el proceso por el que se produce el nuevo cifrado.  
  
 Una clave simétrica solo debe restaurarse si es la misma clave que se usa en ese momento para cifrar y descifrar datos en la base de datos del servidor de informes. Si restaura una clave simétrica que no es válida, ya no puede obtener acceso a los datos confidenciales. En ese caso, elimine y vuelva a crear la clave.  
  
> [!IMPORTANT]  
>  La acción de eliminar y volver a crear la clave simétrica no puede revertirse ni deshacerse. Eliminar o regenerar la clave puede tener consecuencias importantes en la instalación actual. Si elimina la clave, los datos existentes cifrados con la clave simétrica también se eliminan. Entre los datos eliminados se incluyen cadenas de conexión a orígenes de datos de informes externos, cadenas de conexión almacenadas y algunos datos de suscripción.  
  
 Para abrir esta página, inicie el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y seleccione el vínculo en el panel de navegación. Para obtener más información, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opciones  
 **Backup**  
 Copia la clave simétrica al archivo especificado. La clave simétrica nunca se almacena en texto simple. Debe escribir una contraseña para proteger el archivo.  
  
 **Restauración**  
 Aplica una copia guardada anteriormente de la clave simétrica a la base de datos de servidor de informes. Debe proporcionar la contraseña para desbloquear el archivo.  
  
 La copia anterior de la clave simétrica para la instancia de servidor de informes a la que se encuentra conectado actualmente es sobrescrita por la versión restaurada. Después de restaurar la clave simétrica, debe inicializar todos los servidores de informes que utilizan la base de datos del servidor de informes. Para obtener más información acerca de cómo inicializar los servidores de informes, vea [inicializar un servidor de informes &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md).  
  
 **Change**  
 Vuelve a crear la clave simétrica y a cifrar todos los valores cifrados en la base de datos de servidor de informes. Asegúrese de detener el servicio Servidor de informes antes de volver a crear la clave simétrica.  
  
 En una implementación escalada, todas las copias de la clave simétrica son reemplazadas por versiones más recientes. Antes de cambiar la clave simétrica, asegúrese de consultar la lista de servidores combinados con la implementación escalada para comprobar que solo tienen acceso a la nueva clave instancias de servidor de informes válidas. Los servidores que forman parte de una implementación escalada se muestran en la página **Implementación escalada** . Detenga el servicio en cada servidor de informes en la implementación antes de volver a crear la clave.  
  
 Tenga en cuenta que volver a generar la clave simétrica puede ser un proceso de larga duración si tiene muchos orígenes de datos y suscripciones.  
  
 **Eliminar**  
 Elimina la clave simétrica y todo el contenido cifrado, incluidas las cadenas de conexión y credenciales almacenadas. Solo debe eliminar la clave simétrica si no puede restaurarla.  
  
 Una vez que elimine la clave simétrica, debe volver a escribir las cadenas de conexión y credenciales almacenadas que faltan en los informes y orígenes de datos compartidos que no tengan ya estos valores. También debe actualizar todas las suscripciones que utilizan extensiones de entrega que almacenan datos cifrados. Esto incluye la extensión de entrega a recursos compartidos de archivos y las extensiones de entrega a terceros que utilizan valores cifrados.  
  
 No hay ninguna manera automatizada de actualizar esta información. Los informes, suscripciones y orígenes de datos compartidos que utilizan credenciales almacenadas y cadenas de conexión deben actualizarse uno por uno.  
  
## <a name="see-also"></a>Vea también  
 [Temas de Ayuda de F1 de administrador de configuración de Reporting Services &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Eliminar y volver a crear claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Almacenar datos cifrados del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
