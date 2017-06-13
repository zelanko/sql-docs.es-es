---
title: "Ayuda del Asistente para la instalación | Documentos de Microsoft"
ms.custom: 
ms.date: 2017-04-21
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
caps.latest.revision: 62
ms.author: mikeray
manager: jhubbard
robots: noindex,nofollow
ms.translationtype: Human Translation
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 4b16feb70ed6de54240e3335a42ce6df8fa57b81
ms.contentlocale: es-es
ms.lasthandoff: 04/25/2017

---
# <a name="installation-wizard-help"></a>Ayuda del Asistente para la instalación

En este tema se describe algunas de las páginas de configuración de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Asistente para la instalación. 

## <a name="instance-configuration"></a>Configuración de instancia
Use la **configuración de instancia** página de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Asistente para la instalación para especificar si desea crear una instancia predeterminada o una instancia con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es aún no está instalado, una instancia predeterminada se creará a menos que especifique una instancia con nombre.  
  
Cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consta de un conjunto de servicios distinto con una configuración específica para intercalaciones y otras opciones. La estructura de directorios, la estructura del Registro y los nombres de los servicios reflejan todos el nombre de instancia y un identificador de instancia específico que se crearon durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 La instancia puede ser una instancia predeterminada o una instancia con nombre. El nombre de instancia predeterminado es MSSQLSERVER. Para realizar una conexión, no es necesario que un cliente especifique el nombre de la instancia. La instancia con nombre queda determinada por el usuario durante la instalación. Puede instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como una instancia con nombre sin instalar primero la instancia predeterminada. Al mismo tiempo, solo una instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independientemente de la versión, puede ser la instancia predeterminada.  
  
> [!NOTE]  
> Con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep, puede especificar el nombre de instancia cuando complete una instancia preparada en el **configuración de instancia** página. Puede optar por configurar la instancia preparada que está completando como una instancia predeterminada si no existe una instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo.  
  
### <a name="multiple-instances"></a>Instancias múltiples  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un solo servidor o procesador, pero solo una puede ser la predeterminada. Todas las demás deben ser instancias con nombre. Un equipo puede ejecutar varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] simultáneamente y cada instancia se ejecuta independientemente de las otras instancias.  
  
 Para obtener más información, consulte [especificaciones de capacidad máxima para SQL Server](../maximum-capacity-specifications-for-sql-server.md).  
  
### <a name="options"></a>Opciones  
 Solo instancias de clústeres de conmutación por error: especifique el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombre de red del clúster de conmutación por error. Este nombre identifica la instancia en clúster de conmutación por error en la red.  
  
 Instancia predeterminada o con nombre: tenga presente la información siguiente a la hora de decidir entre instalar una instancia predeterminada o una instancia con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Si piensa instalar una única instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un servidor de base de datos, debe ser una instancia predeterminada.  
  
-   Use una instancia con nombre para aquellas situaciones en las que piensa tener varias instancias en el mismo equipo. Un servidor solo puede alojar una instancia predeterminada.  
  
-   Cualquier aplicación que instale [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] debe instalarla como instancia con nombre. Con ello se reducen los conflictos en situaciones en las que se instalan varias aplicaciones en el mismo equipo.  
  
 **Instancia predeterminada**  
 Seleccione esta opción para instalar una instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un equipo solo puede hospedar una instancia predeterminada; todas las demás instancias deben ser instancias con nombre. No obstante, si tiene instalada una instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], podrá agregar una instancia predeterminada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] al mismo equipo.  
  
 **Instancia con nombre**  
 Seleccione esta opción para crear una instancia con nombre nueva. Cuando asigne un nombre a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tenga en cuenta lo siguiente:  
  
-   En los nombres de instancia no se distinguen mayúsculas y minúsculas.  
  
-   Los nombres no pueden comenzar ni terminar por un guión bajo (_).  
  
-   Los nombres de instancia no pueden contener el término "Default" ni otras palabras clave reservadas. Si se utiliza una palabra clave reservada en un nombre de instancia, se producirá un error en el programa de instalación. Para obtener más información, vea [palabras clave reservadas &#40; Transact-SQL &#41; ](../../t-sql/language-elements/reserved-keywords-transact-sql.md).  
  
-   Si especifica MSSQLServer como nombre de instancia, se creará una instancia predeterminada.  
  
-   Una instalación de [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] siempre se instala como una instancia con nombre de '[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]'. No puede especificar un nombre de instancia diferente para este rol de característica.  
  
-   Los nombres de instancias están limitados a 16 caracteres.  
  
-   El primer carácter del nombre de la instancia debe ser una letra. Las letras aceptables son las que define el estándar Unicode 2.0. Se incluyen los caracteres latinos, a-z, A-Z y los caracteres alfabéticos de otros idiomas.  
  
-   Los siguientes caracteres pueden ser letras definidas por el estándar Unicode 2.0, números decimales del alfabeto Latín básico y de otros alfabetos nacionales, el signo de dólar ($) o un carácter de subrayado (_).  
  
-   En los nombres de instancia no se permiten espacios insertados ni otros caracteres especiales. Tampoco se permiten la barra diagonal inversa (\\), la coma (,), los dos puntos (:), el punto y coma (;), la comilla simple ('), el símbolo Y comercial (&), el guion (-) ni la arroba (@).  
  
     Solo los caracteres que son válidos en la página de códigos actual de Windows pueden utilizarse en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombres de instancia. Si se utiliza un carácter Unicode no admitido, se producirá un error en el programa de instalación.  
  
 **Instancias y características detectadas**  
 Vea una lista de las instancias y los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados en el equipo en el que se ejecuta el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Id. de instancia** : de manera predeterminada, el nombre de instancia se usa como identificador de la instancia. Se usa para identificar los directorios de instalación y las claves del Registro para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Es así en las instancias predeterminadas y en las instancias con nombre. Con una instancia predeterminada, el nombre y el identificador serían MSSQLSERVER. Para usar un identificador de instancia no predeterminado, especifíquelo en el campo **Id. de instancia** .  
  
> [!IMPORTANT]  
>  Con SysPrep de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el identificador de instancia que se muestra en esta página es el identificador de instancia especificado durante el paso de preparación de la imagen en el proceso SysPrep de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No podrá especificar un identificador de instancia diferente durante el paso para completar la imagen.  
  
> [!NOTE]  
>  No se admiten identificadores de instancia que comiencen por un guión bajo (_) o que contengan el signo de almohadilla (#) o el signo de dólar ($).  
  
 Para obtener más información acerca de los directorios, las ubicaciones de archivo y nombres de identificador de instancia, consulte [ubicaciones de archivos para las predeterminadas y con nombre de instancias de SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  
 Todos los componentes de una instancia determinada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se administran como una unidad. Todos los Service Pack y actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se aplicarán a cada componente de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Todos los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que comparten el mismo nombre de instancia deben cumplir los siguientes criterios:  
  
-   **Misma versión**  
  
-   **Misma edición**  
  
-   **Misma configuración de idioma**  
  
-   **Mismo estado de clúster**  
  
    > [!NOTE]  
    >  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no detecta los clústeres.  
  
-   **El mismo sistema operativo**  
  
## <a name="analysis-services-configuration---account-provisioning"></a>Configuración de Analysis Services - Aprovisionamiento de cuentas
  Use esta página para establecer el modo de servidor y para conceder permisos administrativos a los usuarios o servicios que requieran acceso sin restricciones a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. La instalación no agrega automáticamente el grupo Windows local BUILTIN\Administrators al rol de administrador del servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de la instancia que está instalando. Si desea agregar el grupo local de administradores al rol de administrador del servidor, debe especificar ese grupo explícitamente.  
  
 Si está instalando [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], asegúrese de conceder permisos administrativos a los administradores de la granja de SharePoint o a los administradores de servicios que sean responsables de una implementación del servidor de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en una granja de [!INCLUDE[SPS2010](../../includes/sps2010-md.md)].  
  
### <a name="options"></a>Opciones  
 **Modo de servidor** : permite especificar el tipo de bases de datos de Analysis Services que se pueden implementar en el servidor. Los modos de servidor se determinan durante la instalación y no se pueden modificar posteriormente. Cada modo es mutuamente exclusivo, lo que significa que se necesitarán dos instancias de Analysis Services, cada una configurada para un modo diferente, para admitir soluciones de modelo OLAP clásicas y tabulares.  
  
 **Especificar administradores** Debe especificar al menos un administrador de servidor para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los usuarios o grupos que especifique serán miembros del rol de administrador del servidor de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que está instalando. Debe haber cuentas de usuario de dominio de Windows en el mismo dominio que el del equipo en el que se instala el software.  
  
> [!NOTE]  
>  Control de cuentas de usuario (UAC) es una característica de seguridad de Windows que requiere que un administrador apruebe específicamente acciones administrativas o aplicaciones antes de que se puedan ejecutar. Dado que UAC está activado de forma predeterminada, se le solicitará que permita las operaciones concretas que requieren privilegios elevados. Puede configurar UAC para cambiar el comportamiento predeterminado o personalizar UAC para programas concretos. Para más información sobre UAC y la configuración de UAC, consulte [Guía paso a paso de Control de cuentas de usuario](http://go.microsoft.com/fwlink/?linkid=196350) y el tema sobre [control de cuentas de usuario (Wikipedia)](http://go.microsoft.com/fwlink/?linkid=196351).  
  
### <a name="see-also"></a>Vea también  
 [Configurar cuentas de servicio &#40; Analysis Services &#41; ](../../analysis-services/instances/configure-service-accounts-analysis-services.md) 
  [Configurar los permisos y cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  

 ## <a name="analysis-services-configuration---data-directories"></a>Configuración de Analysis Services - Directorios de datos
  Los directorios predeterminados de la tabla siguiente los puede configurar el usuario durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se concede permiso para acceder a estos archivos a los administradores locales y a los miembros de SQLServerMSASUser$\<instancia > grupo de seguridad que se crea y suministra durante la instalación.  
  
### <a name="uielement-list"></a>Lista de UIElement  
  
|Descripción|Directorio predeterminado|Recomendaciones|  
|-----------------|-----------------------|---------------------|  
|Directorio raíz de datos|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\< InstanceID > \OLAP\Data\ |Asegúrese de que la carpeta \Archivos de programa\Microsoft SQL Server\ está protegida con permisos limitados. El rendimiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] depende, en muchas configuraciones, del rendimiento del espacio de almacenamiento en el que se ubica el directorio de datos. Coloque este directorio en el almacenamiento asociado al sistema cuyo rendimiento sea máximo. En las instalaciones del clúster de conmutación por error, asegúrese de que los directorios de datos están ubicados en el disco compartido.|  
|Directorio de archivos de registro|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\< InstanceID > \OLAP\Log\ |Este es el directorio para los archivos de registro de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e incluye el registro FlightRecorder. Si incrementa la duración de la Caja negra SQL, asegúrese de que el directorio del registro tenga espacio suficiente.|  
|Directorio temporal|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\< InstanceID > \OLAP\Temp\ |Coloque el directorio Temp en el subsistema de almacenamiento de alto rendimiento.|  
|Directorio de copia de seguridad|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\< InstanceID > \OLAP\Backup\ |Este es el directorio para los archivos de copia de seguridad predeterminados de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. En las instalaciones de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, es también donde los Servicios del sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] almacenan en caché los archivos de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Asegúrese de que se han establecido los permisos adecuados para evitar la pérdida de datos y de que el grupo de usuarios del servicio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tiene los permisos apropiados para escribir en el directorio de copia de seguridad. No se permite usar una unidad asignada para los directorios de copia de seguridad.|  
  
### <a name="notes"></a>Notas  
  
-   Las instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se implementan en una granja de SharePoint almacenan archivos de aplicación, archivos de datos y propiedades de bases de datos de contenido y de aplicación de servicio.  
  
-   Cuando agregue características a una instalación existente, no podrá cambiar la ubicación de una característica instalada anteriormente, ni especificar dicha ubicación para una característica nueva.  

-   Es posible que necesite configurar el software de detección, como aplicaciones antivirus y antispyware, para excluir las carpetas y los tipos de archivo de SQL Server. Revise este artículo de ayuda para obtener más información: [Cómo elegir software antivirus para ejecutar en equipos que ejecutan SQL Server](https://support.microsoft.com/kb/309422).
  
-   Si especifica los directorios de instalación no predeterminados, asegúrese de que las carpetas de instalación sean únicas para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ninguno de los directorios de este cuadro de diálogo se debe compartir con los de otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los componentes de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también deben instalarse en directorios independientes.  
  
-   Los archivos de programa y los archivos de datos no se pueden instalar en las situaciones siguientes:  
  
    -   En una unidad de disco extraíble  
  
    -   En un sistema de archivos que usa compresión  
  
    -   En un directorio que contiene archivos del sistema  
  
### <a name="see-also"></a>Vea también  
 Para obtener más información acerca de los directorios, las ubicaciones de archivo y nombres de identificador de instancia, consulte [ubicaciones de archivos para las predeterminadas y con nombre de instancias de SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  
## <a name="database-engine-configuration---data-directories"></a>Configuración del motor de base de datos - Directorios de datos
  Utilice esta página para especificar la ubicación de instalación para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] archivos de programa y datos. Según el tipo de instalación, es posible que el almacenamiento compatible incluya un disco local, almacenamiento compartido o un servidor de archivos SMB.  
  
 Para especificar un recurso compartido de archivos SMB como directorio, deberá escribir manualmente la ruta UNC admitida. No se admite el desplazamiento a un recurso compartido de archivos SMB. Este es un formato de ruta de acceso UNC admitida para un recurso compartido de archivos SMB: \\\NombreServidor\NombreRecursoCompartido\\...  
  
### <a name="stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Instancia independiente de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 En la tabla siguiente se indican los tipos de almacenamiento admitidos y los directorios predeterminados para una instancia independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que el usuario puede configurar durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="uielement-list"></a>Lista de UIElement  
  
|Descripción|Tipo de almacenamiento compatible|Directorio predeterminado|Recomendaciones|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Directorio raíz de datos|Disco local, servidor de archivos SMB, almacenamiento compartido* |C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]El programa de instalación configurará las ACL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directorios y anulará la herencia como parte de la configuración.|  
|Directorio de base de datos de usuario|Disco local, servidor de archivos SMB, almacenamiento compartido*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\< InstanceID > \MSSQL\Data |Las prácticas recomendadas para los directorios de datos del usuario dependen de los requisitos de carga de trabajo y rendimiento.|  
|Directorio de registro de base de datos de usuario|Disco local, servidor de archivos SMB, almacenamiento compartido*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\< InstanceID > \MSSQL\Data|Asegúrese de que el directorio de registro tenga espacio suficiente.|  
|Directorio de copia de seguridad|Disco local, servidor de archivos SMB, almacenamiento compartido*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\< InstanceID > \MSSQL\Backup|Establezca los permisos apropiados para evitar la pérdida de datos y asegúrese de que la cuenta de usuario para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servicio tiene los permisos adecuados para escribir en el directorio de copia de seguridad. No se permite usar una unidad asignada para los directorios de copia de seguridad.|  
  
 * Aunque se admiten discos compartidos, no es una práctica recomendada para una instancia independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 En la tabla siguiente se enumera los tipos de almacenamiento admitidos y los directorios predeterminados para una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que son el usuario puede configurar durante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación.  
  
|Descripción|Tipo de almacenamiento compatible|Directorio predeterminado|Recomendaciones|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Directorio raíz de datos|Almacenamiento compartido, servidor de archivos SMB|\<Unidad: > \Program archivos\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> Sugerencia: Si se seleccionó un disco compartido en la página **Selección de disco de clúster** , el valor predeterminado es el primer disco compartido. El valor predeterminado de este campo será en blanco si no se realizó ninguna selección en la página **Selección de disco de clúster** .|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]El programa de instalación configurará las ACL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directorios y anulará la herencia como parte de la configuración.|  
|Directorio de base de datos de usuario|Almacenamiento compartido, servidor de archivos SMB|\<Unidad: > archivos de programa\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\< InstanceID > \MSSQL\Data<br /><br /> Sugerencia: Si se seleccionó un disco compartido en la página **Selección de disco de clúster** , el valor predeterminado es el primer disco compartido. El valor predeterminado de este campo será en blanco si no se realizó ninguna selección en la página **Selección de disco de clúster** .|Las prácticas recomendadas para los directorios de datos del usuario dependen de los requisitos de carga de trabajo y rendimiento.|  
|Directorio de registro de base de datos de usuario|Almacenamiento compartido, servidor de archivos SMB|\<Unidad: > \Program archivos\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\< InstanceID > \MSSQL\Data<br /><br /> Sugerencia: Si se seleccionó un disco compartido en la página **Selección de disco de clúster** , el valor predeterminado es el primer disco compartido. El valor predeterminado de este campo será en blanco si no se realizó ninguna selección en la página **Selección de disco de clúster** .|Asegúrese de que el directorio de registro tenga espacio suficiente.|  
|Directorio de copia de seguridad|Disco local, almacenamiento compartido, servidor de archivos SMB|\<Unidad: > \Program archivos\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\< InstanceID > \MSSQL\Backup<br /><br /> Sugerencia: Si se seleccionó un disco compartido en la página **Selección de disco de clúster** , el valor predeterminado es el primer disco compartido. El valor predeterminado de este campo será en blanco si no se realizó ninguna selección en la página **Selección de disco de clúster** .|Establezca los permisos apropiados para evitar la pérdida de datos y asegúrese de que la cuenta de usuario para el servicio de SQL Server tenga los permisos adecuados para escribir en el directorio de copia de seguridad. No se permite usar una unidad asignada para los directorios de copia de seguridad.|  
  
### <a name="security-considerations"></a>Consideraciones de seguridad  
 El programa de instalación configurará las ACL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directorios y anulará la herencia como parte de la configuración.  
  
 Al servidor de archivos SMB se aplican las recomendaciones siguientes:  
  
-   Si se usa un servidor de archivos SMB, la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una cuenta de dominio.  
  
-   La cuenta que se usa para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe los tener permisos NTFS de CONTROL TOTAL en las carpetas de recurso compartido de archivos SMB que se usan como directorio de datos.  
  
-   Al a cuenta que se usa para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se le debe conceder los privilegios SeSecurityPrivilege en el servidor de archivos SMB. Para ello, utilice la consola de directiva de seguridad Local en el servidor de archivos para agregar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta para la instalación del **Administrar registro de auditoría y seguridad** directiva. Esta opción está disponible en la sección **Asignaciones de derechos de usuario** bajo **Directivas locales** de la consola **Directiva de seguridad local** .  
  
### <a name="notes"></a>Notas  
  
-   Cuando agregue características a una instalación existente, no podrá cambiar la ubicación de una característica instalada anteriormente ni especificar dicha ubicación para una característica nueva.  
  
-   Si especifica los directorios de instalación no predeterminados, asegúrese de que las carpetas de instalación sean únicas para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ninguno de los directorios de este cuadro de diálogo se debe compartir con los de otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los componentes de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también deben instalarse en directorios independientes.  
  
-   Los archivos de programa y los archivos de datos no se pueden instalar en las situaciones siguientes:  
  
    -   En una unidad de disco extraíble  
  
    -   En un sistema de archivos que usa compresión  
  
    -   En un directorio que contiene archivos del sistema  
  
    -   En una unidad de red asignada en una instancia de clúster de conmutación por error  
  
### <a name="see-also"></a>Vea también  
### <a name="analysis-services-configuration---data-directories"></a>Configuración de Analysis Services - Directorios de datos
  Los directorios predeterminados de la tabla siguiente los puede configurar el usuario durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se concede permiso para acceder a estos archivos a los administradores locales y a los miembros de SQLServerMSASUser$\<instancia > grupo de seguridad que se crea y suministra durante la instalación.  
  
#### <a name="uielement-list"></a>Lista de UIElement  
  
|Descripción|Directorio predeterminado|Recomendaciones|  
|-----------------|-----------------------|---------------------|  
|Directorio raíz de datos |C:\Program Files\Microsoft SQL Server\MSAS*nn*.\< InstanceID > \OLAP\Data |Asegúrese de que la carpeta \Archivos de programa\Microsoft SQL Server\ está protegida con permisos limitados. El rendimiento de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] depende, en muchas configuraciones, del rendimiento del espacio de almacenamiento en el que se ubica el directorio de datos. Coloque este directorio en el almacenamiento asociado al sistema cuyo rendimiento sea máximo. En las instalaciones del clúster de conmutación por error, asegúrese de que los directorios de datos están ubicados en el disco compartido.|  
|Directorio de archivos de registro|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\< InstanceID > \OLAP\Log |Este es el directorio para los archivos de registro de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e incluye el registro FlightRecorder. Si incrementa la duración de la Caja negra SQL, asegúrese de que el directorio del registro tenga espacio suficiente.|  
|Directorio temporal|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\< InstanceID > \OLAP\Temp |Coloque el directorio Temp en el subsistema de almacenamiento de alto rendimiento.|  
|Directorio de copia de seguridad|C:\Program Files\Microsoft SQL Server\MSAS*nn*.\< InstanceID > \OLAP\Backup |Este es el directorio para los archivos de copia de seguridad predeterminados de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. En las instalaciones de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, es también donde los Servicios del sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] almacenan en caché los archivos de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .<br /><br /> Asegúrese de que se han establecido los permisos adecuados para evitar la pérdida de datos y de que el grupo de usuarios del servicio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tiene los permisos apropiados para escribir en el directorio de copia de seguridad. No se permite usar una unidad asignada para los directorios de copia de seguridad.|  
  
#### <a name="notes"></a>Notas  
  
-   Las instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se implementan en una granja de SharePoint almacenan archivos de aplicación, archivos de datos y propiedades de bases de datos de contenido y de aplicación de servicio.  
  
-   Cuando agregue características a una instalación existente, no podrá cambiar la ubicación de una característica instalada anteriormente, ni especificar dicha ubicación para una característica nueva.  

-   Es posible que necesite configurar el software de detección, como aplicaciones antivirus y antispyware, para excluir las carpetas y los tipos de archivo de SQL Server. Revise este artículo de ayuda para obtener más información: [Cómo elegir software antivirus para ejecutar en equipos que ejecutan SQL Server](https://support.microsoft.com/kb/309422).
  
-   Si especifica los directorios de instalación no predeterminados, asegúrese de que las carpetas de instalación sean únicas para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ninguno de los directorios de este cuadro de diálogo se debe compartir con los de otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los componentes de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también deben instalarse en directorios independientes.  
  
-   Los archivos de programa y los archivos de datos no se pueden instalar en las situaciones siguientes:  
  
    -   En una unidad de disco extraíble  
  
    -   En un sistema de archivos que usa compresión  
  
    -   En un directorio que contiene archivos del sistema  
  
#### <a name="see-also"></a>Vea también  
 Para obtener más información acerca de los directorios, las ubicaciones de archivo y nombres de identificador de instancia, consulte [ubicaciones de archivos para las predeterminadas y con nombre de instancias de SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  
    
 [Los permisos NTFS en un servidor de archivos y recursos compartidos](http://go.microsoft.com/fwlink/?LinkID=206571) 

## <a name="database-engine-configuration---filestream"></a>Configuración del motor de base de datos - Secuencia de archivo
  Utilice esta página para habilitar FILESTREAM para esta instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. FILESTREAM integra [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] con un sistema de archivos NTFS almacenando datos de objetos binarios grandes (BLOB) **varbinary(max)** como archivos en el sistema de archivos. [!INCLUDE[tsql](../../includes/tsql-md.md)] pueden insertar, actualizar, consultar, buscar y realizar copias de seguridad de los datos FILESTREAM. Las interfaces del sistema de archivos de Win32 proporcionan el acceso de la transmisión por secuencias a los datos.  
  
### <a name="uielement-list"></a>Lista de UIElement  
 **Habilitar FILESTREAM para acceso Transact-SQL**  
 Seleccione esta opción para habilitar FILESTREAM para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] . Este control debe comprobarse para que las otras opciones de control estén disponibles.  
  
 **Habilitar FILESTREAM para el acceso de transmisión por secuencias de E/S de archivos**  
 Seleccione esta opción para habilitar el acceso de transmisión por secuencias de Win32 para FILESTREAM.  
  
 **Nombre de recurso compartido de Windows**  
 Utilice este control para escribir el nombre del recurso compartido de Windows en el que los datos de FILESTREAM se almacenarán.  
  
 **Permitir que los clientes remotos tengan acceso de transmisión por secuencias a los datos de FILESTREAM**  
 Seleccione este control para permitir que los clientes remotos tengan acceso a estos datos de FILESTREAM en este servidor.  
  
### <a name="see-also"></a>Vea también  
 [Habilitar y configurar FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  

  
## <a name="database-engine-configuration---server-configuration"></a>Configuración del motor de base de datos: configuración del servidor
  Use esta página para establecer el modo de seguridad en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , así como para agregar grupos o usuarios de Windows como administradores de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
### <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>Consideraciones para ejecutar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se aprovisionaba el grupo **BUILTIN\Administrators** como posibilidad en el inicio de sesión de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y los miembros del grupo local Administradores podían iniciar sesión con sus credenciales de administrador. El uso de permisos elevados no es una práctica recomendada. En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , el grupo **BUILTIN\Administrators** no se aprovisiona como inicio de sesión. En consecuencia, debería crear un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada usuario administrativo y agregarlo al rol fijo de servidor sysadmin durante la instalación de una nueva instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. También debe hacer esto para las cuentas de Windows que se utilizan para ejecutar trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . También se incluyen las cuentas utilizadas para ejecutar trabajos del Agente de replicación.  
  
### <a name="options"></a>Opciones  
 **Modo de seguridad** : seleccione la autenticación de Windows o la autenticación de modo mixto para la instalación.  
  
 **Aprovisionamiento de entidad de seguridad de Windows** : en las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el grupo local Windows Builtin\Administrator estaba ubicado en el rol de servidor sysadmin de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , con lo que se concedía a los administradores de Windows acceso a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], el grupo Builtin\Administrator no se proporciona en el rol de servidor sysadmin. En su lugar, debería aprovisionar explícitamente administradores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para las nuevas instalaciones durante la instalación.  
  
> [!IMPORTANT]  
>  Debe aprovisionar explícitamente administradores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para las nuevas instalaciones durante la instalación. El programa de instalación no le permitirá continuar hasta que complete este paso.  
  
 **Especificar administradores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**: debe especificar por lo menos una entidad de seguridad de Windows para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para agregar la cuenta en la que se ejecuta el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en el botón **Usuario actual** . Para agregar o quitar cuentas de la lista de administradores del sistema, haga clic en **Agregar** o en **Quitar**y, a continuación, edite la lista de usuarios, grupos o equipos que tendrán privilegios de administrador para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Cuando termine de modificar la lista, haga clic en **Aceptar**y, a continuación, compruebe la lista de administradores en el cuadro de diálogo de configuración. Cuando la lista esté completa, haga clic en **Siguiente**.  
  
 Si selecciona la autenticación de modo mixto, debe proporcionar las credenciales de inicio de sesión para la cuenta de administrador de sistema (SA) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] builtin.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Modo de autenticación de Windows**  
 Cuando un usuario se conecta a través de una cuenta de usuario de Microsoft Windows, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valida el nombre de cuenta y la contraseña con el token de la entidad de seguridad de Windows del sistema operativo. Éste es el modo de autenticación predeterminado, y es mucho más seguro que el modo mixto. La autenticación de Windows utiliza el protocolo de seguridad Kerberos, cumple la directiva de contraseñas en lo que respecta a la validación de la complejidad de las contraseñas seguras, y permite el bloqueo de las cuentas y la expiración de las contraseñas.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] No establezca nunca una contraseña en blanco o no segura.  
  
 **Modo mixto (autenticación de Windows o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación)**  
 Permite a los usuarios conectarse con la autenticación de Windows o la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los usuarios que se conectan mediante una cuenta de usuario de Windows pueden usar conexiones de confianza validadas por Windows.  
  
 Si tiene que elegir el modo de autenticación mixto y necesita utilizar inicios de sesión de SQL para incluir aplicaciones heredadas, debe establecer contraseñas seguras para todas las cuentas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
> La autenticación de  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se proporciona únicamente por motivos de compatibilidad con versiones anteriores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **Escribir contraseña**  
 Escriba y confirme el inicio de sesión del administrador del sistema (sa). Las contraseñas son la primera línea de defensa contra los intrusos, por lo que establecer contraseñas seguras es esencial para la seguridad del sistema. No establezca nunca una contraseña en blanco o no segura.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]las contraseñas pueden contener de 1 a 128 caracteres, incluida cualquier combinación de letras, símbolos y números. Si elige la autenticación de modo mixto, debe escribir una contraseña de sa segura antes de continuar con la siguiente página del Asistente para la instalación.  
  
 **Directrices para contraseñas seguras**  
 Las contraseñas seguras no pueden ser adivinadas con facilidad y tampoco son fácilmente vulnerables en caso de utilizar un programa informático. Las contraseñas seguras no pueden utilizar los siguientes términos o condiciones prohibidos:  
  
-   Una condición en blanco o NULL  
  
-   "Password"  
  
-   "Admin"  
  
-   "Administrator"  
  
-   "sa"  
  
-   "sysadmin"  
  
 Una contraseña segura no puede ser ninguno de los siguientes términos asociados al equipo de instalación:  
  
-   El nombre del usuario que haya iniciado actualmente la sesión en el equipo.  
  
-   El nombre del equipo.  
  
 Una contraseña segura debe tener más de 8 caracteres de longitud y satisfacer al menos tres de los siguientes criterios:  
  
-   Debe contener letras mayúsculas.  
  
-   Debe contener letras minúsculas.  
  
-   Debe contener números.  
  
-   Debe contener caracteres no alfanuméricos; por ejemplo, #, %, o ^.  
  
 Las contraseñas que se escriben en esta página deben cumplir los requisitos de las directivas de contraseñas seguras. Si tiene alguna automatización que use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , asegúrese de que la contraseña cumple los requisitos de las directivas de contraseñas seguras.  
  
### <a name="related-content"></a>Contenido relacionado  
 Para más información sobre elegir la autenticación de Windows en lugar de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]La autenticación, vea [elegir un modo de autenticación](../../relational-databases/security/choose-an-authentication-mode.md).  
  
 Para obtener más información acerca de cómo elegir una cuenta para ejecutar el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], consulte [configurar cuentas de servicio de Windows y permisos](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).
  
## <a name="database-engine-configuration---tempdb"></a>Configuración del motor de base de datos: TempDB
  Utilice esta página para especificar **tempdb** archivo de registro y datos de ubicación, tamaño, su configuración de crecimiento y número de archivos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Según el tipo de instalación, es posible que el almacenamiento compatible incluya un disco local, almacenamiento compartido o un servidor de archivos SMB.  
  
 Para especificar un recurso compartido de archivos SMB como directorio, deberá escribir manualmente la ruta UNC admitida. No se admite el desplazamiento a un recurso compartido de archivos SMB. Este es un formato de ruta de acceso UNC admitida para un recurso compartido de archivos SMB: \\\NombreServidor\NombreRecursoCompartido\\...  
  
### <a name="data-and-log-directories-for--a-stand-alone-instance-of--includessnoversionincludesssnoversion-mdmd"></a>Directorios de datos y de registro para una instancia independiente de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 En la tabla siguiente se enumera los tipos de almacenamiento admitidos y los directorios predeterminados para instancias independientes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se pueden configurar durante la instalación.  
  
|Descripción|Tipo de almacenamiento compatible|Directorio predeterminado|Recomendaciones|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**Directorios de datos**|Disco local, servidor de archivos SMB y almacenamiento compartido* |C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\< InstanceID > \MSSQL\Data|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]El programa de instalación configurará las ACL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directorios y anulará la herencia como parte de la configuración.<br /><br /> Las prácticas recomendadas para los directorios **tempdb** dependen de los requisitos de carga de trabajo y rendimiento. Especifique varias carpetas y unidades para distribuir los archivos de datos entre diversos volúmenes.|  
|**Directorio de registro**|Disco local, servidor de archivos SMB y almacenamiento compartido*|C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\< InstanceID > \MSSQL\Data|Asegúrese de que el directorio de registro tenga espacio suficiente.|  
  
 * Aunque se admiten discos compartidos, no es una práctica recomendada para una instancia independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="data-and-log-directories-for-a-failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Directorios de datos y de registro para una instancia de clúster de conmutación por error de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 En la tabla siguiente se enumera los tipos de almacenamiento admitidos y los directorios predeterminados para una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que son el usuario puede configurar durante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación.  
  
|Descripción|Tipo de almacenamiento compatible|Directorio predeterminado|Recomendaciones|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Directorio de datos de**tempdb** |Disco local, almacenamiento compartido y servidor de archivos SMB|\<Unidad: > \Program archivos\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\< InstanceID > \Data<br /><br /> Sugerencia: Si se seleccionó un disco compartido en la página **Selección de disco de clúster** , el valor predeterminado es el primer disco compartido. El valor predeterminado de este campo será en blanco si no se realizó ninguna selección en la página **Selección de disco de clúster** .|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]El programa de instalación configurará las ACL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directorios y anulará la herencia como parte de la configuración.<br /><br /> Asegúrese de que el directorio o los directorios (en caso de indicarse varios archivos) especificados son válidos para todos los nodos de clúster. Durante la conmutación por error, si los directorios **tempdb** no están disponibles en el nodo de destino de la conmutación por error, el recurso de SQL Server no podrá ponerse en línea.|  
|Directorio del registro de**tempdb** |Disco local, almacenamiento compartido y servidor de archivos SMB|\<Unidad: > \Program archivos\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\< InstanceID > \MSSQL\Data<br /><br /> Sugerencia: Si se seleccionó un disco compartido en la página **Selección de disco de clúster** , el valor predeterminado es el primer disco compartido. El valor predeterminado de este campo será en blanco si no se realizó ninguna selección en la página **Selección de disco de clúster** .|Las prácticas recomendadas para los directorios de datos del usuario dependen de los requisitos de carga de trabajo y rendimiento.<br /><br /> Asegúrese de que el directorio especificado sea válido para todos los nodos de clúster. Durante la conmutación por error, si los directorios **tempdb** no están disponibles en el nodo de destino de la conmutación por error, el recurso de SQL Server no podrá ponerse en línea.<br /><br /> Asegúrese de que el directorio de registro tenga espacio suficiente.|  
  
### <a name="uielement-list"></a>Lista de UIElement  
 Configure las opciones de **tempdb** según sus requisitos y la carga de trabajo. Las siguientes opciones se aplican a los archivos de datos de **tempdb** :  
  
-   El valor de**Número de archivos** equivale a la cantidad total de archivos de datos de **tempdb**. El valor predeterminado es el mínimo de los siguientes: bien 8, bien el número de núcleos lógicos detectados por el programa de instalación. Como regla general, si el número de procesadores lógicos es inferior o igual a 8, use el mismo número de archivos de datos que procesadores lógicos. Si el número de procesadores lógicos es superior a 8, utilice 8 archivos de datos y, después, si se mantiene la contención, aumente el número de archivos de datos en múltiplos de 4 (con el número de procesadores lógicos como máximo) hasta que la contención se reduzca a niveles aceptables, o bien modifique el código o la carga de trabajo. 
  
-   **Tamaño inicial (MB)** equivale al tamaño inicial en MB para cada archivo de datos de **tempdb** . El valor predeterminado es 8 MB (o 4 MB para [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]). [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]presenta un tamaño máximo de archivo inicial de 262.144 MB (256 GB). [!INCLUDE[sssql15](../../includes/sssql15-md.md)]tenía un tamaño máximo de archivo inicial de 1024 MB. Todos los archivos de datos de **tempdb** tienen el mismo tamaño inicial. Como **tempdb** se vuelve a crear cada vez que SQL Server se inicia o conmuta por error, debe especificar un valor parecido al tamaño requerido por la carga de trabajo para ofrecer un funcionamiento normal. Para optimizar aún más la creación de **tempdb** durante el inicio, habilite [Database Instant File Initialization](../../relational-databases/databases/database-instant-file-initialization.md).  
  
-   **Tamaño inicial total (MB)** es el tamaño acumulado de todos los archivos de datos de **tempdb** .  
  
-   **Crecimiento automático (MB)** es la cantidad de espacio en megabytes en la que cada archivo de datos de **tempdb** aumentará automáticamente cuando se quede sin espacio. En [!INCLUDE[sssql15](../../includes/sssql15-md.md)] y versiones posteriores todos los archivos de datos crecerá al mismo tiempo en la cantidad especificada en esta configuración.  
  
-   **Crecimiento automático total (MB)** es el tamaño acumulado de cada evento de crecimiento automático.  
  
-   **Directorios de datos** muestra todos los directorios que contienen archivos de datos de **tempdb** . Cuando hay varios directorios, los archivos de datos se colocan en ellos mediante un mecanismo round robin. Por ejemplo, si crea 3 directorios y especifica 8 archivos de datos, los archivos de datos 1, 4 y 7 se crearán en el primer directorio. En el segundo, se crearán los archivos de datos 2, 5 y 8. Por su parte, el 3 y el 6 se generarán en el tercer directorio.  
  
-   Para agregar directorios, haga clic en **Agregar**.  
  
-   Para quitar un directorio, seleccione el que desee y haga clic en **Quitar**.  
  
 **TempDB log file** (Archivo de registro de TempDB) es el nombre del archivo de registro. Se crea automáticamente. Las siguientes opciones se aplican únicamente a los archivos de registro de **tempdb** :  
  
-   **Tamaño inicial (MB)** es el tamaño inicial del archivo de registro de **tempdb** . El valor predeterminado es 8 MB (o 4 MB para [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]). [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)]presenta un tamaño máximo de archivo inicial de 262.144 MB (256 GB). [!INCLUDE[sssql15](../../includes/sssql15-md.md)]tenía un tamaño máximo de archivo inicial de 1024 MB. Como **tempdb** se vuelve a crear cada vez que SQL Server se inicia o conmuta por error, debe especificar un valor parecido al tamaño requerido por la carga de trabajo para ofrecer un funcionamiento normal. Para optimizar aún más la creación de **tempdb** durante el inicio, habilite [Database Instant File Initialization](../../relational-databases/databases/database-instant-file-initialization.md).  
  
-   **Nota: Tempdb** usa unos registros mínimos. No se puede realizar una copia de seguridad del registro de **tempdb** . Se crea de nuevo cada vez que SQL Server se inicia o una instancia de clúster efectúa una conmutación por error.  
  
-   **Crecimiento automático (MB)** equivale al valor en megabytes en el que aumentará el tamaño del registro de **tempdb** .  Con el valor predeterminado de 64 MB, se crea el número óptimo de archivos de registro virtuales durante la inicialización.  
  
-   **Nota: Los archivos de registro de Tempdb** no usan la inicialización instantánea de archivos.  
  
-   **Directorio de registro** es el directorio en el que se crean los archivos de registro de **tempdb** . Solo hay un directorio de registro de **tempdb** .  
  
### <a name="security-considerations"></a>Consideraciones de seguridad  
 El programa de instalación configurará las ACL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directorios y anulará la herencia como parte de la configuración.  

 Al servidor de archivos SMB se aplican las recomendaciones siguientes:  
  
-   Si se usa un servidor de archivos SMB, la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una cuenta de dominio.  
  
-   La cuenta que se usa para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe los tener permisos NTFS de CONTROL TOTAL en las carpetas de recurso compartido de archivos SMB que se usan como directorio de datos.  
  
-   Al a cuenta que se usa para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se le debe conceder los privilegios SeSecurityPrivilege en el servidor de archivos SMB. Para ello, utilice la consola de directiva de seguridad Local en el servidor de archivos para agregar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta para la instalación del **Administrar registro de auditoría y seguridad** directiva. Esta opción está disponible en la sección **Asignaciones de derechos de usuario** bajo **Directivas locales** de la consola **Directiva de seguridad local** .  
  
### <a name="notes"></a>Notas  
  
-   Si especifica los directorios de instalación no predeterminados, asegúrese de que las carpetas de instalación sean únicas para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ninguno de los directorios de este cuadro de diálogo se debe compartir con los de otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los componentes de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también deben instalarse en directorios independientes.  
  
### <a name="see-also"></a>Vea también  
 [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Los permisos NTFS en un servidor de archivos y recursos compartidos](http://go.microsoft.com/fwlink/?LinkID=206571)  

## <a name="database-engine-configuration---user-instance"></a>Configuración del motor de base de datos - Instancia de usuario
Utilice la página **Instancia de usuario** para generar una instancia independiente de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usuarios sin permisos de administrador, y para agregar usuarios al rol Administrador.  
  
### <a name="option"></a>Opción  
 Habilitar instancias de usuario  
 La opción predeterminada es activado. Para deshabilitar la funcionalidad de habilitar instancias de usuario, desactive la casilla.  
  
 La instancia de usuario, también denominada instancia secundaria o cliente, es una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generada por la instancia primaria (la instancia principal que se ejecuta como servicio, como [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) en nombre de un usuario. La instancia de usuario se ejecuta como un proceso de usuario en el contexto de seguridad de dicho usuario. La instancia de usuario está aislada de la instancia primaria y de las demás instancias de usuario que se ejecutan en el equipo. La característica de instancias de usuario también se denomina "Ejecutar como usuario normal" (RANU).  
  
> [!NOTE]  
>  Los inicios de sesión suministrados como miembros del rol fijo de servidor **sysadmin** durante la instalación se suministran como administradores en la base de datos de plantilla. Son miembros del rol fijo de servidor **sysadmin** en la instancia de usuario a menos que se quiten.  
  
 Agregar usuario al rol Administrador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 De forma predeterminada, esta casilla está desactivada. Para agregar el usuario del programa de instalación actual al rol Administrador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , active la casilla.  
  
 [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]los usuarios que sean miembros de BUILTIN\Administrators no se agregan automáticamente al rol fijo de servidor sysadmin al conectarse a [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Solo los usuarios de [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] que se hayan agregado de forma explícita a un rol Administrador de servidor pueden administrar [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Cualquier miembro del grupo BUILTIN\Users se puede conectar a la instancia de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , pero tendrá permisos limitados para realizar tareas de base de datos. Por este motivo, a los usuarios que hereden los privilegios de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] de los grupos BUILTIN\Administrators y BUILTIN\Users de versiones anteriores de Windows se les debe conceder de forma explícita privilegios administrativos a las instancias de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] que se ejecuten en [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)].  
  
 Para realizar cambios en los roles de usuario una vez finalizado este programa de instalación, utilice la Herramienta de configuración de área expuesta (SQLSAC.exe) de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . Para actualizar la lista de usuarios del rol Administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en el vínculo **Agregar nuevo administrador** .  
  
 Asegúrese de que en el campo **Usuario para aprovisionar** aparezca el nombreDeDominio\nombreDeUsuario del usuario cuyos permisos se deben actualizar. Seleccione el rol que se debe actualizar en la lista de instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del panel **Privilegios disponibles** y, a continuación, haga clic en la flecha que señala a la derecha. Para agregar el usuario a todos los roles disponibles para todas las instancias disponibles de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y todos los roles disponibles, haga clic en la flecha doble que señala a la derecha.  
  
 Para implementar los cambios una vez completadas las selecciones, [!INCLUDE[clickOK](../../includes/clickok-md.md)]. Para cerrar la herramienta sin realizar cambios, haga clic en **Cancelar**.  
  
  

