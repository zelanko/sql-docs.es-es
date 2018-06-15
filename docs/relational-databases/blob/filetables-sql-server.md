---
title: FileTables (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
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
- FileTables [SQL Server], overview
- FileTables [SQL Server]
- FileTable [SQL Server], see FileTables [SQL Server]
- FileTable [SQL Server]
ms.assetid: a57b629c-e9ed-48fd-9a48-ed3787d80c8f
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 41f348d83e3b48a0c9d1fbe0ea23ad863cd8a0e6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32921180"
---
# <a name="filetables-sql-server"></a>FileTables (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La característica FileTable proporciona compatibilidad con el espacio de nombres de archivo de Windows y con las aplicaciones Windows para los datos de archivo almacenados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. FileTable permite que una aplicación pueda integrar sus componentes de administración de datos y almacenamiento, así como proporcionar servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrados (incluidas la búsqueda de texto completo y la búsqueda semántica) en datos y metadatos no estructurados.  
  
 Es decir, ahora puede almacenar archivos y documentos en tablas especiales de FileTables denominadas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y tener acceso a ellos desde las aplicaciones Windows como si estuviesen almacenados en el sistema de archivos, sin efectuar cambios en las aplicaciones cliente.  
  
 La característica FileTable se basa en la tecnología de FILESTREAM de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información sobre FILESTREAM, vea [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
##  <a name="Goals"></a> Ventajas de la característica FileTable  
 Los objetivos de la característica FileTable incluyen los siguientes:  
  
-   Compatibilidad con la API de Windows para los datos de archivos almacenados en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La compatibilidad con la API de Windows incluye lo siguiente:  
  
    -   Acceso no transaccional de transmisión por secuencias y actualizaciones en contexto de datos FILESTREAM.  
  
    -   Espacio de nombres jerárquico de directorios y archivos.  
  
    -   Almacenamiento de atributos de archivo, como fecha de creación y fecha de modificación.  
  
    -   Compatibilidad con las API de administración de archivos y directorios de Windows.  
  
-   Compatibilidad con otras características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluidos herramientas de administración, servicios y capacidades de consultas relacionales en FILESTREAM y en datos de atributos de archivo.  
  
 De esta forma, FileTables quita una barrera importante respecto al uso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el almacenamiento y la administración de datos no estructurados que residan actualmente en los archivos y servidores de archivos. Las empresas pueden mover estos datos desde los servidores de archivo a FileTables para aprovechar la administración integrada y los servicios proporcionados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al mismo tiempo, pueden mantener la compatibilidad de las aplicaciones Windows para sus aplicaciones existentes de Windows que ven estos datos como archivos del sistema de archivos.  
 
  
##  <a name="Description"></a> ¿Qué es una FileTable?  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona una **tabla de archivos**especial, también denominada **FileTable**, para aplicaciones que requieren almacenamiento de archivos y directorios en la base de datos, con compatibilidad con la API de Windows y acceso no transaccional. La FileTable es una tabla de usuario especializada con un esquema predefinido que almacena los datos FILESTREAM, así como información de jerarquía de directorios y archivos e información de atributos de archivos.  
  
 Una FileTable proporciona la funcionalidad siguiente:  
  
-   Una FileTable representa una jerarquía de directorios y archivos. Almacena los datos relacionados con todos los nodos de esa jerarquía, tanto para los directorios como los archivos que contienen. Esta jerarquía se inicia en un directorio raíz que se especifica cuando se crea la FileTable.  
  
-   Cada fila de una FileTable representa un archivo o un directorio.  
  
-   Cada fila contiene los elementos siguientes. Para obtener más información acerca del esquema de una FileTable, vea [FileTable Schema](../../relational-databases/blob/filetable-schema.md).  
  
    -   Una columna **file_stream** para los datos de secuencia y un identificador **stream_id** (GUID). (El valor de la columna **file_stream** es NULL para un directorio).  
  
    -   Las dos columnas **path_locator** y **parent_path_locator** para representar y mantener el elemento actual (archivo o directorio) y la jerarquía de directorios.  
  
    -   10 atributos de archivo como fecha de creación y fecha de modificación que son útiles con las API de E/S de archivos.  
  
    -   Una columna de tipo compatible con las búsquedas de texto completo y semántica en archivos y documentos.  
  
-   Una FileTable aplica ciertos desencadenadores y restricciones definidos por el sistema para mantener la semántica del espacio de nombres de archivo.  
  
-   Cuando se configura la base de datos para el acceso no transaccional, la jerarquía de archivos y directorios representada en FileTable se en el recurso compartido de FILESTREAM configurado para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . De esta forma, se proporciona acceso al sistema de archivos para aplicaciones Windows.  
  
 Algunas características adicionales de FileTables incluyen las siguientes:  
  
-   Los datos de archivos y directorios almacenados en una FileTable se exponen a través de un recurso compartido de Windows para el acceso no transaccional a los archivos de las aplicaciones basadas en la API de Windows. Para una aplicación Windows, esto parece un recurso compartido normal con sus archivos y directorios. Las aplicaciones pueden usar un variado conjunto de API de Windows para administrar archivos y directorios del recurso compartido.  
  
-   La jerarquía de directorios que apareció a través del recurso compartido es simplemente una estructura de directorios lógica que se mantiene en FileTable.  
  
-   Un componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intercepta las llamadas para crear o cambiar un archivo o directorio a través del recurso compartido de Windows y las refleja en los datos relacionales correspondientes de la FileTable.  
  
-   Las operaciones de la API de Windows no son transaccionales por naturaleza y no se asocian con transacciones de usuario. No obstante, el acceso transaccional a los datos FILESTREAM almacenados en una FileTable son totalmente compatibles, como es el caso de cualquier columna FILESTREAM de una tabla normal.  
  
-   Las FileTables también se pueden consultar y actualizar mediante el acceso normal de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Además, se integran con las herramientas de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y características como la copia de seguridad.  
  
##  <a name="additional"></a> Consideraciones adicionales sobre el uso de FileTables  
  
###  <a name="DBA"></a> Consideraciones administrativas  
 **FILESTREAM y FileTables**  
  
-   Las FileTables se configuran independientemente de FILESTREAM. Por lo tanto, puede continuar usando la característica FILESTREAM sin habilitar el acceso no transaccional ni crear FileTables.  
  
-   No existe el acceso no transaccional a los datos FILESTREAM salvo a través de las FileTables. Por tanto, cuando se habilita el acceso no transaccional, el comportamiento de las columnas FILESTREAM y de las aplicaciones existentes no se ve afectado.  
  
 **FileTables y acceso no transaccional**  
  
-   Puede habilitar o deshabilitar el acceso no transaccional en el nivel de base de datos.  
  
-   Puede configurar o ajustar el acceso no transaccional en el nivel de base de datos desactivándolo, habilitando el acceso de solo lectura o el acceso completo de lectura y escritura.  
   
###  <a name="memory"></a> Las FileTables no admiten archivos asignados en memoria  
 Las FileTables no admiten archivos asignados en memoria. El Bloc de notas y Paint son dos ejemplos comunes de aplicaciones que utilizan archivos asignados en memoria. No puede utilizar estas aplicaciones en el mismo equipo que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para abrir archivos que se almacenan en una FileTable. No obstante, puede utilizar estas aplicaciones desde un equipo remoto para abrir archivos que se almacenan en una FileTable, porque en estas circunstancias no se utiliza la característica de asignación de memoria.  
   
##  <a name="reltasks"></a> Tareas relacionadas  
 [Habilitar los requisitos previos de FileTables](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)  
 Describe cómo habilitar los requisitos previos para crear y usar FileTables.  
  
 [Crear, modificar y quitar FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)  
 Describe cómo crear una nueva FileTable. O bien, modificar o quitar una FileTable existente.  
  
 [Cargar archivos en FileTables](../../relational-databases/blob/load-files-into-filetables.md)  
 Describe cómo se cargan o migran archivos en las FileTables.  
  
 [Trabajar con directorios y rutas de acceso de FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
 Describe la estructura de directorios en la que los archivos se almacenan en FileTables.  
  
 [Obtener acceso a FileTables con Transact-SQL](../../relational-databases/blob/access-filetables-with-transact-sql.md)  
 Describe el funcionamiento de los comandos del lenguaje de manipulación de datos (DML) de Transact-SQL con FileTables.  
  
 [Obtener acceso a FileTables con API de entrada-salida de archivo](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
 Describe el funcionamiento de E/S del sistema de archivos en una FileTable.  
  
 [Administrar FileTables](../../relational-databases/blob/manage-filetables.md)  
 Describe las tareas administrativas comunes para administrar FileTables.  
  
##  <a name="relcontent"></a> Contenido relacionado  
 [FileTable Schema](../../relational-databases/blob/filetable-schema.md)  
 Describe los esquemas predefinido y fijo de una FileTable.  
  
 [Compatibilidad de FileTable con otras características de SQL Server](../../relational-databases/blob/filetable-compatibility-with-other-sql-server-features.md)  
 Describe el funcionamiento de FileTables con otras características de SQL Server.  
  
 [DDL de FileTable, funciones, procedimientos almacenados y vistas](../../relational-databases/blob/filetable-ddl-functions-stored-procedures-and-views.md)  
 Enumera las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] y objetos de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se han agregado o se han cambiado para admitir la característica de FileTable.  

## <a name="see-also"></a>Ver también
[Vistas de administración dinámica de secuencia de archivo y FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Vistas de catálogo de secuencia de archivo y FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[Procedimientos almacenados del sistema de Filestream y FileTable (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)


  
  
