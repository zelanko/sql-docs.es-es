---
title: 'Configuración de Motor de base de datos: directorios de datos | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9b1fa0fc-623b-479a-afc3-4f13bd850487
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bfb62ec0bbd16a2b77e2f05f64d36ef31498a100
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66095900"
---
# <a name="database-engine-configuration---data-directories"></a>Configuración del motor de base de datos - Directorios de datos
  Use esta página para especificar la ubicación de instalación de los archivos de programa y datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]. Según el tipo de instalación, es posible que el almacenamiento compatible incluya un disco local, almacenamiento compartido o un servidor de archivos SMB.  
  
 Para especificar un recurso compartido de archivos SMB como directorio, deberá escribir manualmente la ruta UNC admitida. No se admite el desplazamiento a un recurso compartido de archivos SMB. Este es un formato de ruta de acceso UNC admitida para un recurso compartido de archivos SMB: \\\NombreServidor\NombreRecursoCompartido\\...  
  
## <a name="stand-alone-instance-of-ssnoversion"></a>Instancia independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 En la tabla siguiente se indican los tipos de almacenamiento admitidos y los directorios predeterminados para una instancia independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que el usuario puede configurar durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="uielement-list"></a>Lista de UIElement  
  
|Descripción|Tipo de almacenamiento compatible|Directorio predeterminado|Recomendaciones|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Directorio raíz de datos|Disco local, servidor de archivos SMB, almacenamiento compartido <sup>1</sup>|\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] C:\Archivos de programa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instalación configurará las ACL para los directorios y interrumpirá la herencia como parte de la configuración.[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \||  
|Directorio de base de datos de usuario|Disco local, servidor de archivos SMB, almacenamiento compartido <sup>1</sup>|C:\Archivos de programa[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] \<InstanceID> \mssql\data|Las prácticas recomendadas para los directorios de datos del usuario dependen de los requisitos de carga de trabajo y rendimiento.|  
|Directorio de registro de base de datos de usuario|Disco local, servidor de archivos SMB, almacenamiento compartido <sup>1</sup>|C:\Archivos de programa[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] \<InstanceID> \mssql\data|Asegúrese de que el directorio de registro tenga espacio suficiente.|  
|Directorio de base de datos temporales|Disco local, servidor de archivos SMB, almacenamiento compartido <sup>1</sup>|C:\Archivos de programa[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] \<InstanceID> \mssql\data|Las prácticas recomendadas para el directorio Temp dependen de los requisitos de carga de trabajo y rendimiento.|  
|Directorio del registro de base de datos temporales|Disco local, servidor de archivos SMB, almacenamiento compartido <sup>1</sup>|C:\Archivos de programa[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] \<InstanceID> \mssql\data|Asegúrese de que el directorio de registro tenga espacio suficiente.|  
|Directorio de copia de seguridad|Disco local, servidor de archivos SMB, almacenamiento compartido <sup>1</sup>|C:\Archivos de programa[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] \<InstanceID> \MSSQL\BACKUP|Establezca los permisos adecuados para evitar la pérdida de datos y asegúrese de que la cuenta de usuario para el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenga los permisos adecuados para escribir en el directorio de copia de seguridad. No se permite usar una unidad asignada para los directorios de copia de seguridad.|  
  
 <sup>1</sup> aunque se admiten los discos compartidos, no es una práctica recomendada para una instancia independiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de.  
  
## <a name="failover-cluster-instance-of-ssnoversion"></a>Instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 En la tabla siguiente se indican los tipos de almacenamiento admitidos y los directorios predeterminados para una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que el usuario puede configurar durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Descripción|Tipo de almacenamiento compatible|Directorio predeterminado|Recomendaciones|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Directorio raíz de datos|Almacenamiento compartido, servidor de archivos SMB|\<Unidad:>\Archivos de programa\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> Sugerencia: Si se seleccionó un disco compartido en la página **Selección de disco de clúster** , el valor predeterminado es el primer disco compartido. El valor predeterminado de este campo será en blanco si no se realizó ninguna selección en la página **Selección de disco de clúster** .|El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurará las ACL para los directorios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y anulará la herencia como parte de la configuración.|  
|Directorio de base de datos de usuario|Almacenamiento compartido, servidor de archivos SMB|\<Unidad: >archivos\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de programa \MSSQL12. \<InstanceID> \mssql\data<br /><br /> Sugerencia: Si se seleccionó un disco compartido en la página **Selección de disco de clúster** , el valor predeterminado es el primer disco compartido. El valor predeterminado de este campo será en blanco si no se realizó ninguna selección en la página **Selección de disco de clúster** .|Las prácticas recomendadas para los directorios de datos del usuario dependen de los requisitos de carga de trabajo y rendimiento.|  
|Directorio de registro de base de datos de usuario|Almacenamiento compartido, servidor de archivos SMB|\<Unidad: > \Archivos de\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]programa \MSSQL12. \<InstanceID> \mssql\data<br /><br /> Sugerencia: Si se seleccionó un disco compartido en la página **Selección de disco de clúster** , el valor predeterminado es el primer disco compartido. El valor predeterminado de este campo será en blanco si no se realizó ninguna selección en la página **Selección de disco de clúster** .|Asegúrese de que el directorio de registro tenga espacio suficiente.|  
|Directorio de base de datos temporales|Disco local, almacenamiento compartido, servidor de archivos SMB|\<Unidad: > \Archivos de\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]programa \MSSQL12. \<InstanceID> \mssql\data<br /><br /> Sugerencia: Si se seleccionó un disco compartido en la página **Selección de disco de clúster** , el valor predeterminado es el primer disco compartido. El valor predeterminado de este campo será en blanco si no se realizó ninguna selección en la página **Selección de disco de clúster** .|Asegúrese de que el directorio especificado sea válido para todos los nodos de clúster. Durante la conmutación por error, si los directorios de tempdb no están disponibles en el nodo de destino de la conmutación por error, el recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no podrá ponerse en línea.|  
|Directorio del registro de base de datos temporales|Disco local, almacenamiento compartido, servidor de archivos SMB|\<Unidad: > \Archivos de\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]programa \MSSQL12. \<InstanceID> \mssql\data<br /><br /> Sugerencia: Si se seleccionó un disco compartido en la página **Selección de disco de clúster** , el valor predeterminado es el primer disco compartido. El valor predeterminado de este campo será en blanco si no se realizó ninguna selección en la página **Selección de disco de clúster** .|Asegúrese de que el directorio especificado sea válido para todos los nodos de clúster. Durante la conmutación por error, si los directorios de tempdb no están disponibles en el nodo de destino de la conmutación por error, el recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no podrá ponerse en línea.|  
|Directorio de copia de seguridad|Disco local, almacenamiento compartido, servidor de archivos SMB|\<Unidad: > \Archivos de\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]programa \MSSQL12. \<InstanceID> \MSSQL\BACKUP<br /><br /> Sugerencia: Si se seleccionó un disco compartido en la página **Selección de disco de clúster** , el valor predeterminado es el primer disco compartido. El valor predeterminado de este campo será en blanco si no se realizó ninguna selección en la página **Selección de disco de clúster** .|Establezca los permisos apropiados para evitar la pérdida de datos y asegúrese de que la cuenta de usuario para el servicio de SQL Server tenga los permisos adecuados para escribir en el directorio de copia de seguridad. No se permite usar una unidad asignada para los directorios de copia de seguridad.|  
  
## <a name="security-considerations"></a>Consideraciones sobre la seguridad  
 El programa de instalación configurará las ACL para los directorios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y anulará la herencia como parte de la configuración.  
  
 Al servidor de archivos SMB se aplican las recomendaciones siguientes:  
  
-   Si se usa un servidor de archivos SMB, la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser una cuenta de dominio.  
  
-   La cuenta que se usa para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe los tener permisos NTFS de CONTROL TOTAL en las carpetas de recurso compartido de archivos SMB que se usan como directorio de datos.  
  
-   Al a cuenta que se usa para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se le debe conceder los privilegios SeSecurityPrivilege en el servidor de archivos SMB. Para ello, use la consola Directiva de seguridad local del servidor de archivos para agregar la cuenta de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la directiva **Administrar registro de seguridad y auditoría**. Esta opción está disponible en la sección **Asignaciones de derechos de usuario** bajo **Directivas locales** de la consola **Directiva de seguridad local** .  
  
## <a name="notes"></a>Notas  
  
-   Cuando agregue características a una instalación existente, no podrá cambiar la ubicación de una característica instalada anteriormente ni especificar dicha ubicación para una característica nueva.  
  
-   Si especifica los directorios de instalación no predeterminados, asegúrese de que las carpetas de instalación sean únicas para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ninguno de los directorios de este cuadro de diálogo se debe compartir con los de otras instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los componentes de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también deben instalarse en directorios independientes.  
  
-   Los archivos de programa y los archivos de datos no se pueden instalar en las situaciones siguientes:  
  
    -   En una unidad de disco extraíble  
  
    -   En un sistema de archivos que usa compresión  
  
    -   En un directorio que contiene archivos del sistema  
  
    -   En una unidad de red asignada en una instancia de clúster de conmutación por error  
  
## <a name="see-also"></a>Consulte también  
 [Ubicaciones de archivos para las instancias predeterminadas y con nombre de SQL Server](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)   
 [Permisos NTFS y de uso compartido en un servidor de archivos](https://go.microsoft.com/fwlink/?LinkID=206571)  
  
  
