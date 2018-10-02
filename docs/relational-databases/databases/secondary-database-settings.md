---
title: Configuración de base de datos secundaria | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.logshipping.settings.dest.f1
ms.assetid: f992ffc9-ee42-43fe-acec-512032f0ded1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bf02c294bef5d3661fbbbaab258eeef6c7078e9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765263"
---
# <a name="secondary-database-settings"></a>Configuración de base de datos secundaria
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice este cuadro de diálogo para configurar y modificar las propiedades de una base de datos secundaria en la configuración del trasvase de registros.  
  
 Para obtener una explicación de los conceptos relacionados con el trasvase de registros, vea [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>Opciones  
 **Instancia del servidor secundario**  
 Muestra el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada actualmente como servidor secundario en la configuración del trasvase de registros.  
  
 **Base de datos secundaria**  
 Muestra el nombre de la base de datos secundaria de la configuración del trasvase de registros. Cuando agregue una nueva base de datos secundaria a una configuración del trasvase de registros, puede elegir una base de datos de la lista o escribir el nombre de una nueva en el cuadro. Si especifica el nombre de una nueva base de datos, deberá seleccionar una opción en la pestaña **Inicialización** que restaure una copia de seguridad completa de la base de datos principal en la base de datos secundaria. La nueva base de datos se crea como parte de la operación de restauración.  
  
 **Conectar**  
 Se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para utilizarla como servidor secundario en la configuración del trasvase de registros. La cuenta utilizada para la conexión debe ser miembro del rol fijo de servidor sysadmin en la instancia de servidor secundario.  
  
 **Pestaña Inicializar**  
 Las opciones son las siguientes:  
  
 **Sí, generar una copia de seguridad completa de la base de datos principal y restaurarla en la base de datos secundaria (y crear la base de datos secundaria si no existe)**  
 Hace que [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] configure la base de datos secundaria realizando una copia de seguridad de la base de datos principal y restaurándola en el servidor secundario. Si ha especificado un nombre de base de datos nuevo en el cuadro **Base de datos secundaria** , la base de datos se creará como parte de la operación de restauración.  
  
 **Opciones de restauración**  
 Haga clic en esta opción si desea restaurar los datos y los archivos de registro de la base de datos secundaria en ubicaciones que no sean las predeterminadas del servidor secundario.  
  
 Este botón abre el cuadro de diálogo **Opciones de restauración** . En dicho cuadro podrá especificar la ruta de acceso a carpetas no predeterminadas en las que desee que residan la base de datos secundaria y su registro. Si especifica alguna carpeta, deberá especificar ambas cosas.  
  
 Las rutas de acceso deben hacer referencia a las unidades locales en el servidor secundario. Asimismo, las rutas de acceso deben empezar por una letra de unidad local y dos puntos (por ejemplo, `C:`). No puede utilizar rutas de red ni letras de unidades asignadas.  
  
 Si hace clic en el botón **Opciones de restauración** y, a continuación, decide que desea utilizar las carpetas predeterminadas, le recomendamos que cancele el cuadro de diálogo **Opciones de restauración** . Si ya ha especificado ubicaciones no predeterminadas y ahora desea utilizar las ubicaciones predeterminadas en su lugar, haga clic de nuevo en **Opciones de restauración** , desactive los cuadros de texto y haga clic en Aceptar.  
  
 **Sí, restaurar una copia de seguridad existente de la base de datos principal en la base de datos secundaria (y crear la base de datos secundaria si no existe)**  
 Hace que [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] utilice una copia de seguridad existente de la base de datos principal para inicializar la base de datos secundaria. Escriba la ubicación de dicha copia de seguridad en el cuadro **Archivo de copia de seguridad** . Si ha especificado un nombre de base de datos nuevo en el cuadro Base de datos secundaria, la base de datos se creará como parte de la operación de restauración.  
  
 **Archivo de copia de seguridad**  
 Escriba la ruta de acceso y el nombre de archivo de la copia de seguridad completa de la base de datos que quiere usar para inicializar la base de datos secundaria si elige la opción **Sí, restaurar una copia de seguridad existente de la base de datos principal en la base de datos secundaria (y crear la base de datos secundaria si no existe)**.  
  
 **Opciones de restauración**  
 Vea la descripción de este botón realizada anteriormente en este mismo tema.  
  
 **No, la base de datos secundaria está inicializada**  
 Especifique si la base de datos secundaria ya está inicializada y lista para aceptar las copias de seguridad del registro de transacciones de la base de datos principal. Esta opción no se encuentra disponible si ha especificado un nombre de base de datos nuevo en el cuadro **Base de datos secundaria** .  
  
 **Pestaña Copiar archivos**  
 Las opciones son las siguientes:  
  
 **Carpeta de destino de los archivos copiados**  
 Escriba la ruta de acceso en la que deben copiarse las copias de seguridad del registro de transacciones para restaurar la base de datos secundaria. Normalmente se trata de una ruta de acceso local a una carpeta que se encuentra en el servidor secundario. No obstante, si la carpeta se encuentra en otro servidor, deberá especificar una ruta de acceso UNC para esta carpeta. La cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la instancia del servidor secundario deberá tener permisos de lectura en esta carpeta. Además, deberá conceder permisos de lectura y escritura para este recurso compartido de red a las cuentas de proxy con las que los trabajos de copia y restauración se ejecuten en las instancias del servidor secundario. De forma predeterminada, es la cuenta de servicio del Agente SQL Server de la instancia del servidor secundario, aunque un miembro de sysadmin puede elegir otras cuentas de proxy para los trabajos.  
  
 **Eliminar los archivos copiados después de**  
 Elija el período de tiempo que desea que los archivos de copia de seguridad del registro de transacciones copiados permanezcan en la carpeta de destino antes de ser eliminados.  
  
 **Nombre del trabajo**  
 Muestra el nombre del trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizado para copiar los archivos de copia de seguridad del registro de transacciones del servidor principal al servidor secundario. Cuando se crea este trabajo por primera vez, se puede cambiar el nombre escribiéndolo en el cuadro.  
  
 **Programación**  
 Muestra la programación actual del trabajo de copia del Agente SQL Server utilizada para copiar los archivos de copia de seguridad del registro de transacciones del servidor principal en el servidor secundario. Puede modificar esta programación haciendo clic en **Programar...**.  
  
 **Programar...**  
 Modifique los parámetros del trabajo del Agente SQL Server que realiza las copias de seguridad del registro de transacciones del servidor principal en el servidor secundario.  
  
 **Deshabilitar este trabajo**  
 Suspende el trabajo de copia del Agente SQL Server.  
  
 **Pestaña Restaurar registro de transacciones**  
 Las opciones son las siguientes:  
  
 **Desconectar usuarios en la base de datos al restaurar las copias de seguridad**  
 Desconecta automáticamente a los usuarios de la base de datos secundaria mientras se restauran las copias de seguridad del registro de transacciones.  
  
 **Modo sin recuperación**  
 Deje la base de datos secundaria en modo NORECOVERY.  
  
 **Modo de espera**  
 Deje la base de datos secundaria en modo STANDBY. Este modo le permitirá realizar operaciones de solo lectura en la base de datos.  
  
> [!IMPORTANT]  
>  Si cambia el modo de recuperación de una base de datos secundaria existente, por ejemplo de **Modo sin recuperación** a **Modo de espera**, el cambio únicamente surte efecto una vez restaurada la base de datos de copia de seguridad de registros siguiente en la base de datos.  
  
 **Retrasar la restauración de las copias de seguridad al menos**  
 Elija el retraso con el que se restaurarán las copias de seguridad del registro de transacciones (si existen) en la base de datos secundaria.  
  
 **Mostrar una alerta si no se produce una restauración tras**  
 Elija el periodo de tiempo que desea que el trasvase de registros espere antes de generar una alerta que indique que no se ha producido ninguna restauración del registro de transacciones.  
  
 **Nombre del trabajo**  
 Muestra el nombre del trabajo del Agente SQL Server utilizado para restaurar las copias de seguridad del registro de transacciones en la base de datos secundaria. Cuando se crea este trabajo por primera vez, se puede cambiar el nombre escribiéndolo en el cuadro.  
  
 **Programación**  
 Muestra la programación actual del trabajo del Agente SQL Server utilizado para restaurar las copias de seguridad del registro de transacciones en la base de datos secundaria. Puede modificar esta opción haciendo clic en **Programar...**.  
  
 **Programar...**  
 Modifique los parámetros asociados con el trabajo de restauración del Agente SQL Server.  
  
 **Deshabilitar este trabajo**  
 Suspende las operaciones de restauración en la base de datos secundaria.  
  
## <a name="see-also"></a>Ver también  
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  
