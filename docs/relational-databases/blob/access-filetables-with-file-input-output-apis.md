---
title: Obtener acceso a FileTables con API de entrada-salida de archivo | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: blob
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], accessing files with file APIs
ms.assetid: fa504c5a-f131-4781-9a90-46e6c2de27bb
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9e222e28f0a669985185756bc5ef77bf1d127fa7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="access-filetables-with-file-input-output-apis"></a>Obtener acceso a FileTables con API de entrada-salida de archivo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Describe el funcionamiento de E/S del sistema de archivos en una FileTable.  
  
##  <a name="accessing"></a> Empezar a usar API de E/S con FileTables  
 El principal uso previsto para las FileTables se realizará a través del sistema de archivos de Windows y las API de E/S de archivos. Las FileTables no admiten el acceso no transaccional a través del variado conjunto de API de E/S de archivos disponibles.  
  
1.  El acceso de las API de E/S de archivos se inicia normalmente mediante la obtención de una ruta de acceso UNC lógica del archivo o directorio. Las aplicaciones pueden usar una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] con la función [GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md) para obtener la ruta de acceso lógica del archivo o directorio. Para más información, consulte [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
2.  A continuación la aplicación usa esta ruta de acceso lógica para obtener un identificador del archivo o directorio y hacer algo con el objeto. La ruta de acceso se puede pasar a cualquier función de API admitida, como CreateFile () o CreateDirectory (), para crear o abrir un archivo y obtener un identificador. El identificador se puede usar después para transmitir datos, enumerar u organizar directorios, obtener o establecer atributos de archivo, eliminar archivos o directorios, etc.  
  
##  <a name="create"></a> Crear los archivos y directorios de una FileTable  
 Un archivo o directorio se puede crear en una FileTable llamando a las API de E/S de archivos, como CreateFile o CreateDirectory.  
  
-   Se admiten todas las marcas de disposición de creación, todos los modos de uso compartido y todos los modos de acceso, incluidas la creación, eliminación y modificación en contexto de archivos. Asimismo, se admiten las actualizaciones del espacio de nombres de archivos. Es decir, las operaciones de creación y eliminación, cambio de nombre y movimiento de directorios.  
  
-   La creación de un nuevo archivo o directorio se corresponde con la creación de una nueva fila en la FileTable subyacente.  
  
-   En los archivos, los datos de flujo se almacenan en la columna **file_stream** mientras que, en los directorios, esta columna tiene el valor NULL.  
  
-   En los archivos, la columna **is_directory** contiene **false**. En los directorios, esta columna contiene **true**.  
  
-   El uso compartido y la simultaneidad de acceso se aplican cuando varias operaciones de E/S de archivos o varias operaciones [!INCLUDE[tsql](../../includes/tsql-md.md)] simultáneas afectan al mismo archivo o directorio de la jerarquía.  
  
##  <a name="read"></a> Leer los archivos y directorios de una FileTable  
 La semántica de aislamiento de lectura confirmada se aplica en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a todas las operaciones de acceso de E/S de archivos, para datos de atributo y de flujo.  
  
##  <a name="write"></a> Escribir y actualizar los archivos y directorios de una FileTable  
  
-   Todas las operaciones de lectura y escritura de E/S de los archivos de una FileTable son no transaccionales; es decir, no hay ninguna transacción de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enlazada a estas operaciones, y no se proporcionan garantías ACID.  
  
-   Todas las actualizaciones de transmisión de datos o en contexto de E/S de archivos son compatibles con la FileTable.  
  
-   Las actualizaciones de los atributos o datos de FILESTREAM a través de las API de E/S de archivos tendrán como resultado la actualización de las columnas de atributos de archivos y la columna **file_stream** correspondiente de la FileTable.  
  
##  <a name="delete"></a> Eliminar los archivos y directorios de una FileTable  
 Toda la semántica de las API de E/S de archivos de Windows se aplica cuando se elimina un archivo o directorio.  
  
-   Se produce un error al eliminar un directorio si este contiene archivos o subdirectorios.  
  
-   Al eliminar un archivo o directorio, se quita la fila correspondiente de la FileTable. Esto es equivalente a eliminar la fila mediante una operación [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
##  <a name="supported"></a> Operaciones compatibles del sistema de archivos  
 Las FileTables admiten las API del sistema de archivos relacionadas con las siguientes operaciones del sistema de archivos:  
  
-   Administración de directorios  
  
-   Administración de archivos  
  
 Las FileTables no admiten las operaciones siguientes:  
  
-   Administración del disco  
  
-   Administración del volumen  
  
-   NTFS de transacciones  
  
##  <a name="considerations"></a> Consideraciones adicionales sobre el acceso de E/S de archivos a FileTables  
  
###  <a name="vnn"></a> Usar nombres de red virtual (VNN) con grupos de disponibilidad AlwaysOn  
 Cuando la base de datos que contiene datos de FILESTREAM o FileTable pertenece a un grupo de disponibilidad AlwaysOn, todo acceso a los datos de FILESTREAM o FileTable a través de las API del sistema de archivos debe usar los VNN en lugar de nombres de equipo. Para obtener más información, vea [FILESTREAM y FileTable con grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md).  
  
###  <a name="partial"></a> Actualizaciones parciales  
 Se puede usar un identificador de escritura obtenido para los datos de FILESTREAM en una FileTable mediante la función [GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md) para llevar a cabo actualizaciones parciales en contexto del contenido de FILESTREAM. Este comportamiento es diferente al acceso de FILESTREAM con transacciones a través del identificador que se obtiene llamando a **OpenSQLFILESTREAM()** y pasando un contexto de transacción explícita.  
  
###  <a name="trans"></a> Semántica transaccional  
 Cuando se obtiene acceso a los archivos de una FileTable con las API de E/S de archivos, estas operaciones no están asociadas con ninguna transacción de usuario y tienen las características adicionales siguientes:  
  
-   Como el acceso sin transacciones de los datos de FILESTREAM de una FileTable no está asociado a ninguna transacción, no tiene una semántica específica de aislamiento. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede usar transacciones internas para aplicar la semántica de bloqueo o simultaneidad en los datos de FileTable. Cualquier transacción interna de este tipo se realiza con el aislamiento de lectura confirmada.  
  
-   No existen garantías ACID para estas operaciones sin transacciones de los datos de FILESTREAM. Las garantías de coherencia son similares a las de las actualizaciones de archivos efectuadas por las aplicaciones del sistema de archivos.  
  
-   Estos cambios no se pueden revertir.  
  
 Pero también se puede obtener acceso a la columna FILESTREAM de una FileTable a través de FILESTREAM con transacciones llamando a **OpenSqlFileStream ()**. Este tipo de acceso puede ser totalmente transaccional y respetará todos los niveles de coherencia transaccional que se admiten actualmente.  
  
###  <a name="concurrency"></a> Control de simultaneidad  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica el control de simultaneidad para el acceso de FileTable entre las aplicaciones del sistema de archivos, así como entre las aplicaciones del sistema de archivos y las aplicaciones [!INCLUDE[tsql](../../includes/tsql-md.md)] . Este control de simultaneidad se logra aplicando los bloqueos adecuados en las filas de la FileTable.  
  
###  <a name="triggers"></a> Desencadenadores  
 La creación, modificación o eliminación de archivos o directorios o de sus atributos a través del sistema de archivos tendrán como resultado las operaciones de inserción, actualización o eliminación correspondientes en la FileTable. Los desencadenadores DML de [!INCLUDE[tsql](../../includes/tsql-md.md)] asociados se activarán como parte de estas operaciones.  
  
##  <a name="funclist"></a> Funcionalidad del sistema de archivos admitida en FileTables  
  
|Capacidad|Compatible|Comentarios|  
|----------------|---------------|--------------|  
|**Oplocks**|Sí|Se admiten los bloqueos oportunistas de nivel 2, nivel 1, lote y filtro.|  
|**Atributos extendidos**|no||  
|**Puntos de análisis**|no||  
|**ACL persistentes**|no||  
|**Flujos con nombre**|no||  
|**Archivos dispersos**|Sí|La dispersión se puede establecer solo en archivos y afecta al almacenamiento del flujo de datos. Dado que los datos de FILESTREAM se almacenan en volúmenes NTFS, la característica FileTable admite archivos dispersos reenviando las solicitudes al sistema de archivos NTFS.|  
|**Compresión**|Sí||  
|**Cifrado**|Sí||  
|**TxF**|no||  
|**Identificadores de archivo**|no||  
|**Identificadores de objeto**|no||  
|**Vínculos simbólicos**|no||  
|**Vínculos físicos**|no||  
|**Nombres cortos**|no||  
|**Notificaciones de cambio de directorio**|no||  
|**Bloqueo de intervalo de bytes**|Sí|Las solicitudes de bloqueo de intervalo de butes se pasan al sistema de archivos NTFS.|  
|**Archivos asignados en memoria**|no||  
|**Cancelar E/S**|Sí||  
|**Seguridad**|no|Se aplica la seguridad de nivel de recursos compartidos de Windows y la seguridad de nivel de tabla y columna de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**Diario USN**|no|Los cambios de metadatos en archivos y directorios de una FileTable son operaciones DML en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por consiguiente, se registran en el archivo de registro de la base de datos correspondiente. Sin embargo, no se registran en el diario de NTFS USN (salvo los cambios de tamaño).<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se pueden usar para capturar información similar.|  
  
## <a name="see-also"></a>Ver también  
 [Cargar archivos en FileTables](../../relational-databases/blob/load-files-into-filetables.md)   
 [Trabajar con directorios y rutas de acceso de FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)   
 [Obtener acceso a FileTables con Transact-SQL](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [DDL de FileTable, funciones, procedimientos almacenados y vistas](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
  
  
