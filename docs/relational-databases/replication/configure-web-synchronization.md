---
title: "Configuración de sincronización web | Microsoft Docs"
ms.custom: 
ms.date: 01/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL10.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL10.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1
- SQL13.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1
helpviewer_keywords:
- Web synchronization, security best practices
- Web synchronization, configuring
ms.assetid: 21f8e4d4-cd07-4856-98f0-9c9890ebbc82
caps.latest.revision: 74
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bc4b16adf509a811980323e2bc41e3f44c9906d9
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
<a id="configure-web-synchronization" class="xliff"></a>

# Configurar la sincronización web
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La opción de sincronización web para la replicación de mezcla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] habilita la replicación de datos con el protocolo HTTPS a través de Internet. Para utilizar la sincronización web, primero debe realizar las siguientes acciones de configuración:  
  
1.  Cree nuevas cuentas de dominio y asignar inicios de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Configure el equipo en el que se están ejecutando [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) para sincronizar suscripciones.  
  
3.  Configure una publicación de combinación para que permita la sincronización web.  
  
4.  Configure una o más suscripciones para utilizar la sincronización web.  
  
> [!NOTE]  
>  Si piensa replicar grandes volúmenes de datos o utilizar tipos de datos de gran tamaño como **varchar(max)**, lea la sección "Replicar grandes volúmenes de datos" de este tema.  
  
 Para preparar la sincronización web correctamente, debe decidir cómo configurará la seguridad para cumplir sus requisitos y directivas especiales. Es aconsejable tomar estas decisiones y crear las cuentas necesarias antes de intentar configurar IIS, la publicación y las suscripciones.  
  
 En los procedimientos que siguen, se describe una configuración de seguridad simplificada utilizando cuentas locales por motivos de brevedad. Esta configuración simplificada es adecuada para instalaciones donde IIS y el publicador y distribuidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecutan en el mismo equipo, aunque es mucho más probablemente (y recomendado) que utilice una topología de varios servidores en una instalación de producción. Puede sustituir las cuentas de dominio por cuentas locales en los procedimientos.  
  
<a id="creating-new-accounts-and-mapping-sql-server-logins" class="xliff"></a>

## Crear cuentas nuevas y asignar inicios de sesión de SQL Server  
 La Escucha de replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (replisapi.dll) se conecta al publicador suplantando la cuenta especificada para el grupo de aplicaciones asociado al sitio web de replicación.  
  
 La cuenta utilizada para la Escucha de replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener los permisos descritos en [Merge Agent Security](../../relational-databases/replication/merge-agent-security.md), en la sección sobre conexión al publicador o distribuidor. En resumen, la cuenta debe:  
  
-   Ser miembro de la lista de acceso a la publicación (PAL).  
  
-   Estar asignada un inicio de sesión asociado a un usuario en la base de datos de publicaciones.  
  
-   Estar asignada un inicio de sesión asociado a un usuario en la base de datos de distribución.  
  
-   Tener permisos de lectura en el recurso compartido de instantáneas.  
  
 Si es la primera vez que utiliza la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , también tendrá que crear cuentas e inicios de sesión para los agentes de réplica. Para obtener más información, vea las secciones sobre configuración de la publicación y la suscripción de este tema.  
  
 Antes de configurar la sincronización web, se recomienda leer la sección "Prácticas recomendadas de seguridad para la sincronización web", de este tema. Para obtener más información acerca de la seguridad en la sincronización web, vea [Security Architecture for Web Synchronization](../../relational-databases/replication/security/security-architecture-for-web-synchronization.md).  
  
<a id="configuring-the-computer-that-is-running-iis" class="xliff"></a>

## Configurar el equipo en el que se ejecuta IIS  
 La sincronización web requiere que instale y configure IIS. Necesitará la dirección URL del sitio web de replicación para poder configurar una publicación para utilizar la sincronización web.  
  
 La sincronización web es compatible con IIS, a partir de la versión 5.0. El Asistente para configurar la sincronización web no se admite en la versión 7.0 de IIS. A partir de SQL Server 2012, para usar el componente de sincronización web en el servidor IIS, recomendamos instalar SQL Server con replicación. Puede ser la edición gratuita de SQL Server Express.  
  
 SSL es necesario para la sincronización web. Necesitará un certificado de seguridad emitido por una entidad de certificación. Únicamente en los casos en que se estén realizando pruebas se puede utilizar un certificado de seguridad autofirmado.  
   
  
 **Para configurar IIS para la sincronización web**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Configurar IIS para la sincronización web](../../relational-databases/replication/configure-iis-for-web-synchronization.md)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Configurar IIS 7 para la sincronización web](../../relational-databases/replication/configure-iis-7-for-web-synchronization.md)  
  
<a id="creating-a-web-garden" class="xliff"></a>

## Crear hospedaje multiproceso en una única máquina  
 La Escucha de replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite dos operaciones de sincronización simultáneas por subproceso. Si se supera este límite la Escucha de replicación podría dejar de responder. La propiedad de máximo de subprocesos de trabajo del grupo de aplicaciones determina el número de subprocesos asignado a replisapi.dll. De forma predeterminada, esta propiedad está establecida en 1.  
  
 Puede admitir un número mayor de operaciones de sincronización simultáneas por CPU aumentando el valor de la propiedad de máximo de procesos de trabajo. La ampliación horizontal mediante el aumento del número de procesos de trabajo por CPU se denomina crear "hospedaje multiproceso en una única máquina".  
  
 El hospedaje multiproceso en una única máquina permitirá que más de dos suscriptores se sincronicen a la vez. También aumentará la utilización de la CPU por parte de replisapi.dll, lo que puede afectar al rendimiento del servidor negativamente. Es importante tener en cuenta estos aspectos al elegir un valor para el máximo de procesos de trabajo.  
  
<a id="to-increase-maximum-worker-processes-in-iis-7" class="xliff"></a>

#### Para aumentar el máximo de procesos de trabajo en IIS 7  
  
1.  En **Administrador de Internet Information Services (IIS)**, expanda el nodo del servidor y, después, haga clic en el nodo **Grupos de aplicaciones** .  
  
2.  Seleccione el grupo de aplicaciones asociado al sitio de sincronización web y, a continuación, haga clic en **Configuración avanzada** en el panel **Acciones** .  
  
3.  En el cuadro de diálogo Configuración avanzada, bajo en el encabezado **Procesar modelo** , haga clic la fila etiquetada **Máximo de procesos de trabajo**. Cambie el valor de la propiedad y haga clic en **Aceptar**.  
  
<a id="configuring-the-publication" class="xliff"></a>

## Configurar la publicación  
 Para utilizar la sincronización web, cree una publicación igual que lo haría para una topología de mezcla estándar. Para obtener más información sobre la creación de publicaciones, vea [Publicar datos y objetos de base de datos](../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
 Una vez creada la publicación, habilite la opción para permitir la sincronización web mediante de estos métodos: [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]o Replication Management Objects (RMO). Para habilitar la sincronización web, tendrá que proporcionar la dirección del servidor web para las conexiones del suscriptor.  
  
 Si utiliza un publicador por primera vez, también debe configurar un distribuidor y un recurso compartido de instantáneas. El Agente de mezcla de cada suscriptor debe tener permisos de lectura en el recurso compartido de instantáneas. Para obtener más información sobre cómo configurar la distribución, vea [Configure Distribution (Configurar la distribución)](../../relational-databases/replication/configure-distribution.md) y [Proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
 **gen** es una palabra reservada en los archivos XML de websync. No intente publicar tablas que contengan columnas denominadas **gen**.  
  
<a id="configuring-the-subscription" class="xliff"></a>

## Configurar la suscripción  
 Después de habilitar una publicación y configurar IIS, cree una suscripción de extracción y especifique que dicha suscripción debe sincronizarse mediante IIS. La sincronización web solo puede usarse para las suscripciones de extracción.  
  
<a id="upgrading-from-an-earlier-version-of-sql-server" class="xliff"></a>

## Actualizar de una versión anterior de SQL Server  
 Si tiene una topología de sincronización web existente configurada y actualiza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe asegurarse de que la última versión de Replisapi.dll se copia en el directorio virtual utilizado por la sincronización web. De forma predeterminada, la última versión de Replisapi.dll se encuentra en C:\Archivos de programa\Microsoft SQL Server\\<nnn\>\COM.  
  
<a id="replicating-large-volumes-of-data" class="xliff"></a>

## Replicar grandes volúmenes de datos.  
 Para evitar que se produzcan posibles problemas de memoria en los equipos suscriptores, la sincronización web usa un tamaño máximo predeterminado de 100 MB para el archivo XML que se utiliza para transferir los cambios. Es posible aumentar este límite estableciendo la siguiente clave del Registro:  
  
 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\Replication**  
  
 **WebSyncMaxXmlSize DWORD 2000000**  
  
 El intervalo de valores aceptables para esta clave está comprendido entre 100 MB y 4GB. El valor se especifica en KB. Establecer este parámetro en un valor alto no garantiza que sea posible sincronizar esa cantidad de datos. El límite real queda restringido por la cantidad de memoria contigua disponible en el equipo suscriptor. Si el valor ha de ser mayor de 100 MB, es recomendable que aumente el valor de forma incremental y que pruebe el consumo de memoria en el suscriptor con una carga de trabajo típica.  
  
 El tamaño máximo para el archivo XML es 4 GB, pero la replicación sincroniza los cambios de ese archivo en lotes. El tamaño máximo del lote de datos y metadatos es de 25 MB. Debe asegurarse de que los datos de cada lote no superan aproximadamente los 20 MB, lo que concede un margen suficiente para los metadatos y cualquier otra sobrecarga. Este límite tiene las implicaciones siguientes:  
  
-   No se puede replicar ninguna columna que haga que los datos y los metadatos superen los 25 MB. Este podría constituir un problema si se replican filas que contienen tipos de datos de gran tamaño, como **varchar(max)**.  
  
-   Si se replican grandes volúmenes de datos, podría ser necesario ajustar el tamaño del lote del Agente de mezcla.  
  
 El tamaño del lote para la replicación de mezcla se mide en *generaciones*, que son conjuntos de cambios por artículo. El número de generaciones de un lote se especifica utilizando los parámetros **DownloadGenerationsPerBatch** y–**UploadGenerationsPerBatch** del Agente de mezcla. Para más información, consulte [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md).  
  
 Para grandes volúmenes de datos, especifique un número pequeño para cada uno de los parámetros de procesamiento por lotes. Se recomienda comenzar con un valor de 10 y optimizarlo después de acuerdo con las necesidades y el rendimiento de la aplicación. Normalmente, estos parámetros se especifican en un perfil de agente. Para obtener más información acerca de los perfiles, vea [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
<a id="security-best-practices-for-web-synchronization" class="xliff"></a>

## Prácticas recomendadas de seguridad para la sincronización web  
 Existen muchas opciones de configuración relacionadas con la seguridad en la sincronización web. Se recomienda el siguiente enfoque:  
  
-   El distribuidor y el publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden estar en el mismo equipo, configuración típica para la replicación de mezcla. Sin embargo, IIS debe estar en otro equipo.  
  
-   Utilice SSL (Capa de sockets seguros) para cifrar la conexión entre el suscriptor y el equipo en el que se ejecuta IIS. Esto es necesario para la sincronización web.  
  
-   Use la autenticación básica para las conexiones del suscriptor a IIS. Con la autenticación básica, IIS puede realizar conexiones al publicador o distribuidor en nombre del suscriptor sin que sea necesaria la delegación. La delegación es necesaria si se usa la autenticación integrada.  
  
    > [!NOTE]  
    >  La autenticación básica es el método que se utiliza para enviar credenciales a IIS. El uso de la autenticación básica no impide que se puedan especificar cuentas de dominio de Windows para las conexiones a IIS.  
  
-   Especifique que el Agente de instantáneas se ejecute con una cuenta de dominio de Windows y que el agente realice las conexiones con esta cuenta. Es la configuración predeterminada. Especifique que cada Agente de mezcla se ejecute con la cuenta de dominio del usuario que utiliza el equipo del suscriptor y que el agente realice las conexiones con esta cuenta.  
  
     Para obtener más información acerca de los permisos que necesitan los agentes, vea [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
-   Especifique la misma cuenta de dominio que utiliza el Agente de mezcla cuando especifique una cuenta y una contraseña en la página **Información del servidor web** del Asistente para nueva suscripción o cuando especifique valores para los parámetros **@internet_url** y **@internet_login** de [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md). Esta cuenta debe tener permisos de lectura en el recurso compartido de la instantánea.  
  
-   Cada publicación debe utilizar un directorio virtual independiente para IIS.  
  
-   La cuenta bajo la que se ejecuta la Escucha de replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Replisapi.dll) es también la cuenta que se conectará al publicador y al distribuidor durante la sincronización. Esta cuenta debe estar asignada a una cuenta de inicio de sesión de SQL en el publicador y el distribuidor. Para obtener más información, vea la sección "Establecer los permisos para la Escucha de replicación de SQL Server" en [Configurar IIS para la sincronización web](../../relational-databases/replication/configure-iis-for-web-synchronization.md).  
  
-   Puede usar FTP para entregar la instantánea desde el publicador al equipo en el que se ejecuta IIS. La instantánea se entrega siempre desde el equipo en el que se ejecuta IIS al suscriptor mediante HTTPS. Para obtener más información, vea [Transferir instantáneas mediante FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
-   Si los servidores de la topología de replicación están situados detrás de un firewall, quizá sea necesario abrir puertos del firewall para habilitar la sincronización web.  
  
    -   El equipo suscriptor se conecta al equipo que está ejecutando IIS sobre HTTPS usando SSL, que se configura normalmente para usar el puerto 443. [!INCLUDE[ssEW](../../includes/ssew-md.md)] Los suscriptores también pueden conectarse a través de HTTP, que se configura normalmente para usar el puerto 80.  
  
    -   El equipo en el que se ejecuta IIS suele conectarse con el publicador o con el distribuidor usando el puerto 1433 (instancia predeterminada). Cuando el publicador o el distribuidor es una instancia con nombre en un servidor con otra instancia predeterminada, suele usarse el puerto 1500 para la conexión con la instancia con nombre.  
  
    -   Si el equipo en el que se ejecuta IIS se encuentra separado del distribuidor mediante un firewall y se usa un recurso compartido de FTP para la entrega de instantáneas, deben abrirse los puertos que se usan para FTP. Para obtener más información, vea [Transferir instantáneas mediante FTP](../../relational-databases/replication/transfer-snapshots-through-ftp.md).  
  
> [!IMPORTANT]  
>  El hecho de abrir puertos en el firewall puede dejar el servidor expuesto a ataques malintencionados. Asegúrese de que conoce los sistemas de firewall antes de abrir puertos. Para obtener más información, vea [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
<a id="see-also" class="xliff"></a>

## Vea también  
 [Sincronización web para la replicación de mezcla](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  

