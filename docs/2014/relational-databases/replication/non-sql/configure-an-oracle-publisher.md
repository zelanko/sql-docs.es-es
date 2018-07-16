---
title: Configurar un publicador de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], configuring
ms.assetid: 240c8416-c8e5-4346-8433-07e0f779099f
caps.latest.revision: 58
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 66bd7f7e6bc67856a3c5f6e231a2c554a3eb4b29
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37264431"
---
# <a name="configure-an-oracle-publisher"></a>Configurar un publicador de Oracle
  Las publicaciones de publicadores de Oracle se crean de la misma forma que las publicaciones de instantáneas y transaccionales típicas, pero antes de crear una publicación desde un publicador de Oracle, debe completar los siguientes pasos (los pasos uno, tres y cuatro se describen con todo detalle en este tema):  
  
1.  Cree un usuario administrativo de replicación en la base de datos de Oracle con el script que se proporciona.  
  
2.  En las tablas que publique, conceda permiso SELECT directamente en cada una de ellas (no mediante un rol) al usuario administrativo de Oracle que ha creado en el paso uno.  
  
3.  Instale el software de cliente de Oracle y el proveedor OLE DB en el distribuidor de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y, a continuación, reinicie la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Si el distribuidor se ejecuta en una plataforma de 64 bits, debe utilizar la versión de 64 bits del proveedor OLE DB de Oracle.  
  
4.  Configure la base de datos de Oracle como un publicador en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Para obtener una lista de objetos que se pueden replicar desde una base de datos de Oracle, vea [Consideraciones y limitaciones de diseño de los publicadores de Oracle](design-considerations-and-limitations-for-oracle-publishers.md).  
  
> [!NOTE]  
>  Debe ser miembro del rol fijo de servidor **sysadmin** para habilitar un publicador o distribuidor y para crear una publicación de Oracle o una suscripción desde una publicación de Oracle.  
  
## <a name="creating-the-replication-administrative-user-schema-within-the-oracle-database"></a>Crear el esquema de usuario administrativo de replicación dentro de la base de datos de Oracle  
 Los agentes de replicación se conectan a la base de datos de Oracle y realizan operaciones en el contexto del esquema de usuario que debe crear. A este esquema deben concederse diversos permisos, que se enumeran en la sección siguiente. Este esquema es propietario de todos los objetos creados por el proceso de replicación de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el publicador de Oracle, excepto de un sinónimo público, **MSSQLSERVERDISTRIBUTOR**. Para obtener más información sobre los objetos creados en la base de datos de Oracle, vea [Objects Created on the Oracle Publisher](objects-created-on-the-oracle-publisher.md).  
  
> [!NOTE]  
>  Al quitar el sinónimo público **MSSQLSERVERDISTRIBUTOR** y el usuario de replicación de Oracle configurado con la opción **CASCADE** se quitan todos los objetos de replicación del publicador de Oracle.  
  
 Se proporciona un script de ejemplo para ayudar a la configuración del esquema de usuario de replicación de Oracle. El script está disponible en el directorio siguiente después de la instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: *\<unidad>*:\\\Archivos de programa\Microsoft SQL Server\\*\<nombreDeInstancia>* \MSSQL\Install\oracleadmin.sql. También está incluido en el tema [Script to Grant Oracle Permissions](script-to-grant-oracle-permissions.md).  
  
 Conéctese a la base de datos de Oracle utilizando una cuenta con privilegios DBA y ejecute el script. Este script solicita el nombre usuario y la contraseña del esquema de usuario administrativo de replicación y también el espacio de tablas predeterminado donde crear los objetos (el espacio de tablas debe existir en la base de datos de Oracle). Para información sobre cómo especificar otros espacios de tablas para objetos, vea [Administrar espacios de tabla de Oracle](manage-oracle-tablespaces.md). Elija un nombre de usuario y una contraseña segura, pero anótelos porque esta información se le pedirá más tarde al configurar la base de datos de Oracle como un publicador. Se recomienda utilizar el esquema solo para los objetos requeridos por la replicación; no cree tablas para publicarlas en este esquema.  
  
### <a name="creating-the-user-schema-manually"></a>Crear el esquema de usuario manualmente  
 Si crea el esquema de usuario administrativo de replicación manualmente, debe conceder al esquema los siguientes permisos, directamente o mediante un rol de base de datos.  
  
-   CREATE PUBLIC SYNONYM y DROP PUBLIC SYNONYM  
  
-   CREATE PROCEDURE  
  
-   CREATE SEQUENCE  
  
-   CREATE SESSION  
  
 También debe conceder los siguientes permisos al usuario directamente (no mediante un rol):  
  
-   CREATE ANY TRIGGER. Solo es necesario en la replicación de instantáneas y transaccional.  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
## <a name="installing-and-configuring-oracle-client-networking-software-on-the-sql-server-distributor"></a>Instalar y configurar el software de red de cliente de Oracle en el distribuidor de SQL Server  
 Debe instalar y configurar el software de red de cliente de Oracle y el proveedor OLE DB de Oracle en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , para que el distribuidor pueda realizar conexiones al publicador de Oracle. Después de instalar el software, establezca los permisos apropiados en las carpetas donde está instalado el software y, a continuación, detenga y reinicie la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para asegurarse de que todos los valores se actualizan (los permisos se describen más adelante en la sección "Establecer permisos de directorio").  
  
> [!NOTE]  
>  Debe utilizarse la versión más reciente del software de red de cliente de Oracle. Oracle recomienda que los usuarios instalen las versiones más recientes del software de cliente. Por tanto, la versión del software de cliente suele ser más reciente que la del software de base de datos.  
  
 La forma más directa de instalar y configurar el software de red de cliente es utilizar Oracle Universal Installer (Instalador universal de Oracle) y Net Configuration Assistant (Asistente para configuración de redes) del disco del cliente de Oracle.  
  
 En Oracle Universal Installer proporcione la siguiente información:  
  
|Información|Descripción|  
|-----------------|-----------------|  
|Oracle Home (Directorio de inicio de Oracle)|Es la ruta de acceso al directorio de instalación del software de Oracle. Acepte el valor predeterminado (C:\oracle\ora90 o similar) o escriba otra ruta de acceso. Para obtener más información sobre el directorio de inicio de Oracle, vea la sección "Consideraciones sobre el directorio de inicio de Oracle" más adelante en este tema.|  
|Oracle home name (Nombre del directorio de inicio de Oracle)|Un alias para la ruta de acceso del directorio de inicio de Oracle.|  
|Installation type (Tipo de instalación)|En Oracle 10g, seleccione la opción de instalación **Administrator** (Administrador).|  
  
 Una vez finalizada la instalación con Oracle Universal Installer, utilice Net Configuration Assistant para configurar la conectividad de red. Debe proporcionar cuatro grupos de información para configurar la conectividad de red. El administrador de base de datos de Oracle configura la red al instalar la base de datos y la escucha, y debería poder proporcionar esta información si el usuario no la tiene. Debe realizar las siguientes acciones:  
  
|Acción|Descripción|  
|------------|-----------------|  
|Identificar la base de datos|Existen dos métodos para identificar la base de datos. El primer método utiliza el Identificador de sistema (SID) de Oracle y está disponible en cada versión de Oracle. El segundo método utiliza el Nombre de servicio, que está disponible a partir de Oracle versión 8.0. Los dos métodos utilizan un valor que se configura al crear la base de datos y es importante que la configuración de red de cliente use el mismo método de nomenclatura que utilizó el administrador al configurar la escucha para la base de datos.|  
|Identificar un alias de red para la base de datos|Se debe especificar un alias de red, que se utilizará para tener acceso a la base de datos de Oracle. Este alias también se proporciona al identificar la base de datos de Oracle como un publicador en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . El alias de red es básicamente un puntero al SID o al Nombre de servicio remoto que se configuró al crear la base de datos; tiene nombres distintos en las diferentes versiones y productos de Oracle, incluidos Net Service Name y TNS Alias. SQL*Plus solicita este alias como el parámetro "Host String" (Cadena de host) cuando se inicia la sesión.|  
|Seleccionar el protocolo de red|Seleccione los protocolos que desee admitir. La mayoría de aplicaciones utilizan TCP.|  
|Especificar la información de host para identificar las escuchas de base de datos|El host es el nombre o el alias de DNS del equipo donde se está ejecutando la escucha de Oracle, que normalmente es el mismo equipo donde reside la base de datos. En algunos protocolos, se debe proporcionar información adicional. Por ejemplo, si se selecciona TCP, se debe proporcionar el puerto donde se escuchan las solicitudes de conexión a la base de datos de destino. La configuración predeterminada de TCP utiliza el puerto 1521.|  
  
### <a name="setting-directory-permissions"></a>Establecer permisos de directorio  
 A la cuenta con la que se ejecuta el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el distribuidor deben concederse permisos de lectura y ejecución para el directorio (y todos los subdirectorios) en el que esté instalado el software de red de cliente de Oracle.  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>Comprobar la conectividad entre el distribuidor de SQL Server y el publicador de Oracle  
 Casi al final del asistente para configuración de redes puede que aparezca una opción para comprobar la conexión al publicador de Oracle. Antes de comprobar la conexión, asegúrese de que la instancia de la base de datos de Oracle está en línea y que la Escucha de Oracle está ejecutándose. Si la comprobación no es correcta, póngase en contacto con el administrador de bases de datos de Oracle responsable de la base de datos a la intenta conectarse.  
  
 Después de realizar una conexión correcta al publicador de Oracle, intente iniciar la sesión en la base de datos con la cuenta y la contraseña asociados al esquema de usuario administrativo de replicación que ha creado. Debe realizar las siguientes acciones si trabaja con la misma cuenta de Windows que utiliza el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
1.  Haga clic en **Inicio**y, a continuación, haga clic en **Ejecutar**.  
  
2.  Escriba `cmd` y haga clic en **Aceptar**.  
  
3.  En el símbolo del sistema, escriba:  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     Por ejemplo, `sqlplus replication/$tr0ngPasswerd@Oracle90Server`.  
  
4.  Si la configuración de red es correcta, se iniciará la sesión y verá el símbolo de `SQL` .  
  
5.  Si tiene problemas de conexión con la base de datos de Oracle, vea la sección acerca de que el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no se puede conectar a la instancia de base de datos de Oracle en el tema [Troubleshooting Oracle Publishers](troubleshooting-oracle-publishers.md).  
  
### <a name="considerations-for-oracle-home"></a>Consideraciones sobre el directorio de inicio de Oracle  
 Oracle admite la instalación paralela de archivos binarios de aplicaciones, pero la replicación solo puede utilizar un conjunto de archivos binarios a la vez. Cada conjunto de archivos binarios está asociado a un directorio de inicio de Oracle; los archivos binarios se encuentran en el directorio %ORACLE_HOME%\bin. Debe asegurarse de que se utiliza el conjunto de archivos binarios correcto (concretamente, la versión más reciente del software de red de cliente) cuando la replicación realiza las conexiones al publicador de Oracle.  
  
 Inicie la sesión en el distribuidor con las cuentas que utiliza el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el servicio del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , y establezca las variables de entorno apropiadas. Debe establecerse la variable %ORACLE_HOME% para hacer referencia al punto de instalación que ha especificado al instalar el software de red de cliente. La variable %PATH% debe incluir el directorio %ORACLE_HOME% \bin como la primera entrada de Oracle que se encuentre. Para obtener información sobre cómo establecer variables de entorno, vea la documentación de Windows.  
  
## <a name="configuring-the-oracle-database-as-a-publisher-at-the-sql-server-distributor"></a>Configurar la base de datos de Oracle como un publicador en el distribuidor de SQL Server  
 Los publicadores de Oracle siempre utilizan un distribuidor remoto. Se debe configurar una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que actúe como un distribuidor para el publicador de Oracle (un publicador de Oracle solo puede utilizar un distribuidor, pero un solo distribuidor puede dar servicio a más de un publicador de Oracle). Después de configurar un distribuidor, identifique la instancia de la base de datos de Oracle como un publicador en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], Transact-SQL o Replication Management Objects (RMO). Para más información sobre cómo configurar la distribución, vea [Configurar la distribución](../configure-distribution.md).  
  
> [!NOTE]  
>  Un publicador de Oracle no puede tener el mismo nombre que su distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ni el mismo nombre que ninguno de los publicadores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que utilizan el mismo distribuidor.  
  
 Al identificar la base de datos de Oracle como un publicador, se debe elegir una opción de publicación de Oracle: Oracle o Puerta de enlace de Oracle. Después de identificar un publicador, esta opción no se puede cambiar sin quitar y volver a configurar el publicador. La opción Completo está diseñada para proporcionar publicaciones de instantáneas y transaccionales con el conjunto completo de características compatibles para la publicación de Oracle. La opción Puerta de enlace proporciona optimizaciones de diseño específicas para mejorar el rendimiento en casos en los que la replicación sirve como puerta de enlace entre sistemas.  
  
 Después de identificar el publicador de Oracle en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , la replicación crea un servidor vinculado con el mismo nombre que el nombre del servicio TNS en la base de datos de Oracle. Este servidor vinculado solo lo puede utilizar la replicación. Si necesita conectarse al publicador de Oracle a través de una conexión con el servidor vinculado, cree otro nombre de servicio TNS y utilícelo para llamar a [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql).  
  
 Para configurar un publicador de Oracle y crear una publicación, vea [Create a Publication from an Oracle Database](../publish/create-a-publication-from-an-oracle-database.md).  
  
## <a name="see-also"></a>Vea también  
 [Consideraciones administrativas para los publicadores de Oracle](administrative-considerations-for-oracle-publishers.md)   
 [Asignar tipos de datos para publicadores de Oracle](data-type-mapping-for-oracle-publishers.md)   
 [Glosario de términos de publicaciones de Oracle](glossary-of-terms-for-oracle-publishing.md)   
 [Información general de la publicación de Oracle](oracle-publishing-overview.md)  
  
  
