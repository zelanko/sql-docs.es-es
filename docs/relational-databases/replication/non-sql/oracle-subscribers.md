---
title: Suscriptores de Oracle | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [SQL Server replication], non-SQL Server Subscribers
- Oracle Subscribers [SQL Server replication]
- non-SQL Server Subscribers, Oracle
- heterogeneous Subscribers, Oracle
- mapping data types [SQL Server replication]
ms.assetid: 591c0313-82ce-4689-9fc1-73752ff122cf
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 35360f2cfd76745e0222845f3bac0dd868283657
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="oracle-subscribers"></a>Suscriptores de Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A partir de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] admite las suscripciones de inserción a Oracle a través del proveedor Oracle OLE DB suministrado por Oracle.  
  
## <a name="configuring-an-oracle-subscriber"></a>Configurar un suscriptor de Oracle  
 Para configurar un suscriptor de Oracle, siga estos pasos:  
  
1.  Instale y configure el software de red de cliente de Oracle y el proveedor OLE DB de Oracle en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , a fin de que el distribuidor pueda realizar conexiones al suscriptor de Oracle. Debe utilizarse la versión más reciente del software de red de cliente de Oracle. Oracle recomienda que los usuarios instalen las versiones más recientes del software de cliente. Por tanto, la versión del software de cliente suele ser más reciente que la del software de base de datos. La manera más sencilla de instalar el software es utilizar Oracle Universal Installer, que se encuentra en el disco de cliente de Oracle. En Oracle Universal Installer proporcione la siguiente información:  
  
    |Información|Description|  
    |-----------------|-----------------|  
    |Oracle Home (Directorio de inicio de Oracle)|Es la ruta de acceso al directorio de instalación del software de Oracle. Acepte el valor predeterminado (C:\oracle\ora90 o similar) o escriba otra ruta de acceso. Para obtener más información sobre el directorio de inicio de Oracle, vea la sección "Consideraciones sobre el directorio de inicio de Oracle" más adelante en este tema.|  
    |Oracle home name (Nombre del directorio de inicio de Oracle)|Un alias para la ruta de acceso del directorio de inicio de Oracle.|  
    |Installation type (Tipo de instalación)|En Oracle 10g, seleccione la opción de instalación **Runtime** (Biblioteca de tiempo de ejecución) o **Administrator** (Administrador).|  
  
2.  Muestra un nombre TNS para el suscriptor. TNS (Transparent Network Substrate, Sustrato de red transparente) es una capa de comunicación que utilizan las bases de datos Oracle. TNS Service Name es el nombre por el que se conocen las instancias de una base de datos Oracle en una red. Se asigna un nombre a este servicio cuando se configura la conectividad de la base de datos Oracle. La replicación utiliza el nombre de servicio TNS para identificar al suscriptor y establecer las conexiones.  
  
     Una vez finalizada la instalación con Oracle Universal Installer, utilice Net Configuration Assistant para configurar la conectividad de red. Debe proporcionar cuatro grupos de información para configurar la conectividad de red. El administrador de base de datos de Oracle configura la red al instalar la base de datos y la escucha, y debería poder proporcionar esta información si el usuario no la tiene. Debe realizar las siguientes acciones:  
  
    |Acción|Description|  
    |------------|-----------------|  
    |Identificar la base de datos|Existen dos métodos para identificar la base de datos. El primer método utiliza el Identificador de sistema (SID) de Oracle y está disponible en cada versión de Oracle. El segundo método utiliza el Nombre de servicio, que está disponible a partir de Oracle versión 8.0. Los dos métodos utilizan un valor que se configura al crear la base de datos y es importante que la configuración de red de cliente use el mismo método de nomenclatura que utilizó el administrador al configurar la escucha para la base de datos.|  
    |Identificar un alias de red para la base de datos|Se debe especificar un alias de red, que se utilizará para tener acceso a la base de datos de Oracle. El alias de red es básicamente un puntero al SID o al Nombre de servicio remoto que se configuró al crear la base de datos; tiene nombres distintos en las diferentes versiones y productos de Oracle, incluidos Net Service Name y TNS Alias. SQL*Plus solicita este alias como el parámetro "Host String" (Cadena de host) cuando se inicia la sesión.|  
    |Seleccionar el protocolo de red|Seleccione los protocolos que desee admitir. La mayoría de aplicaciones utilizan TCP.|  
    |Especificar la información de host para identificar las escuchas de base de datos|El host es el nombre o el alias de DNS del equipo donde se está ejecutando la escucha de Oracle, que normalmente es el mismo equipo donde reside la base de datos. En algunos protocolos, se debe proporcionar información adicional. Por ejemplo, si se selecciona TCP, se debe proporcionar el puerto donde se escuchan las solicitudes de conexión a la base de datos de destino. La configuración predeterminada de TCP utiliza el puerto 1521.|  
  
3.  Cree una instantánea o una publicación transaccional, habilítela para suscriptores que no sean[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y, después, cree una suscripción de inserción para el suscriptor. Para más información, consulte [Crear una suscripción para un suscriptor que no sea de SQL Server](../../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
### <a name="setting-directory-permissions"></a>Configurar permisos de directorio  
 A la cuenta con la que se ejecuta el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en el distribuidor deben concederse permisos de lectura y ejecución para el directorio (y todos los subdirectorios) en el que esté instalado el software de red de cliente de Oracle.  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>Comprobar la conectividad entre el distribuidor de SQL Server y el publicador de Oracle  
 Casi al final del asistente para configuración de redes puede que aparezca una opción para comprobar la conexión al publicador de Oracle. Antes de comprobar la conexión, asegúrese de que la instancia de la base de datos de Oracle está en línea y que la Escucha de Oracle está ejecutándose. Si la comprobación no es correcta, póngase en contacto con el administrador de bases de datos de Oracle responsable de la base de datos a la intenta conectarse.  
  
 Después de realizar una conexión correcta al publicador de Oracle, intente iniciar la sesión en la base de datos con la cuenta y la contraseña configurados para el Agente de distribución de la suscripción.  
  
1.  Haga clic en **Inicio**y, a continuación, haga clic en **Ejecutar**.  
  
2.  Escriba `cmd` y haga clic en **Aceptar**.  
  
3.  En el símbolo del sistema, escriba:  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     Por ejemplo, `sqlplus replication/$tr0ngPasswerd@Oracle90Server`.  
  
4.  Si la configuración de red es correcta, se iniciará la sesión y verá el símbolo de `SQL` .  
  
### <a name="considerations-for-oracle-home"></a>Consideraciones sobre el directorio de inicio de Oracle  
 Oracle admite la instalación paralela de archivos binarios de aplicaciones, pero la replicación solo puede utilizar un conjunto de archivos binarios a la vez. Cada conjunto de archivos binarios está asociado a un directorio de inicio de Oracle; los archivos binarios se encuentran en el directorio %ORACLE_HOME%\bin. Debe asegurarse de que se utiliza el conjunto de archivos binarios correcto (concretamente, la versión más reciente del software de red de cliente) cuando la replicación realiza las conexiones al publicador de Oracle.  
  
 Inicie la sesión en el distribuidor con las cuentas que utiliza el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y el servicio del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , y establezca las variables de entorno apropiadas. Debe establecerse la variable %ORACLE_HOME% para hacer referencia al punto de instalación que ha especificado al instalar el software de red de cliente. La variable %PATH% debe incluir el directorio %ORACLE_HOME% \bin como la primera entrada de Oracle que se encuentre. Para obtener información sobre cómo establecer variables de entorno, vea la documentación de Windows.  
  
> [!NOTE]  
>  Si tiene más de un directorio de inicio de Oracle en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , asegúrese de que el Agente de distribución está utilizando el proveedor Oracle OLE DB más reciente. En algunos casos, Oracle no actualiza el proveedor OLE DB de manera predeterminada cuando se actualizan los componentes de cliente en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Desinstale el proveedor OLE DB antiguo e instale la versión más reciente. Para obtener más información acerca de cómo instalar y desinstalar el proveedor, vea la documentación de Oracle.  
  
## <a name="considerations-for-oracle-subscribers"></a>Consideraciones sobre los suscriptores de Oracle  
 Además de las consideraciones incluidas en el tema [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md), tenga en cuenta los siguientes aspectos al replicar en suscriptores de Oracle:  
  
-   Oracle trata tanto las cadenas vacías como los valores NULL como NULL. Esto es importante si se define una columna de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como NOT NULL, y se replica la columna en un suscriptor de Oracle. Para evitar errores al aplicar cambios en el suscriptor de Oracle, debe realizar una de las siguientes acciones:  
  
    -   Asegúrese de que las cadenas vacías no se insertan como valores de columna en la tabla publicada.  
  
    -   Utilice el parámetro **–SkipErrors** para el Agente de distribución si es aceptable recibir una notificación de errores en el registro de historial del Agente de distribución y continuar el procesamiento. Especifique el código de error 1400 de Oracle (**-SkipErrors1400**).  
  
    -   Modifique el script de la tabla generada, quitando el atributo NOT NULL de cualquier columna de caracteres a la que puedan haberse asociado cadenas vacías y suministre el script modificado como script personalizado para el artículo mediante el parámetro @creation_script de [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
-   Los suscriptores de Oracle admiten la opción de esquema 0x4071. Para obtener más información sobre las opciones de esquema, vea [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
## <a name="mapping-data-types-from-sql-server-to-oracle"></a>Asignar tipos de datos desde SQL Server a Oracle  
 En la tabla siguiente se muestran las asignaciones de tipos de datos que se utilizan cuando se replican datos en un suscriptor que está ejecutando Oracle.  
  
|Tipo de datos de SQL Server|Tipo de datos de Oracle|  
|--------------------------|----------------------|  
|**bigint**|NUMBER(19,0)|  
|**binary(1-2000)**|RAW(1-2000)|  
|**binary(2001-8000)**|BLOB|  
|**bit**|NUMBER(1)|  
|**char(1-2000)**|CHAR(1-2000)|  
|**char(2001-4000)**|VARCHAR2(2001-4000)|  
|**char(4001-8000)**|CLOB|  
|**date**|DATE|  
|**datetime**|DATE|  
|**datetime2(0-7)**|TIMESTAMP(7) para Oracle 9 y Oracle 10; VARCHAR(27) para Oracle 8|  
|**datetimeoffset(0-7)**|TIMESTAMP(7) WITH TIME ZONE para Oracle 9 y Oracle 10; VARCHAR(34) para Oracle 8|  
|**decimal(1-38, 0-38)**|NUMBER(1-38, 0-38)|  
|**float(53)**|FLOAT|  
|**float**|FLOAT|  
|**geography**|BLOB|  
|**geometry**|BLOB|  
|**hierarchyid**|BLOB|  
|**imagen**|BLOB|  
|**int**|NUMBER(10,0)|  
|**money**|NUMBER(19,4)|  
|**nchar(1-1000)**|CHAR(1-1000)|  
|**nchar(1001-4000)**|NCLOB|  
|**ntext**|NCLOB|  
|**numeric(1-38, 0-38)**|NUMBER(1-38, 0-38)|  
|**nvarchar(1-1000)**|VARCHAR2(1-2000)|  
|**nvarchar(1001-4000)**|NCLOB|  
|**nvarchar(max)**|NCLOB|  
|**real**|real|  
|**smalldatetime**|DATE|  
|**smallint**|NUMBER(5,0)|  
|**smallmoney**|NUMBER(10,4)|  
|**sql_variant**|N/D|  
|**sysname**|VARCHAR2(128)|  
|**varchar(max)**|CLOB|  
|**time(0-7)**|VARCHAR(16)|  
|**timestamp**|RAW (8)|  
|**tinyint**|NUMBER(3,0)|  
|**uniqueidentifier**|CHAR(38)|  
|**varbinary(1-2000)**|RAW(1-2000)|  
|**varbinary(2001-8000)**|BLOB|  
|**varchar(1-4000)**|VARCHAR2(1-4000)|  
|**varchar(4001-8000)**|CLOB|  
|**varbinary(max)**|BLOB|  
|**ntext**|CLOB|  
|**xml**|NCLOB|  
  
## <a name="see-also"></a>Ver también  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)   
 [Suscribirse a publicaciones](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
