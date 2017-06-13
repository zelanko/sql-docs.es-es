---
title: Archivos de datos de SQL Server en Microsoft Azure | Microsoft Docs
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 38ffd9c2-18a5-43d2-b674-e425addec4e4
caps.latest.revision: 26
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: c0e55c0e35039490f0ce4cd8a7fb6d7e232c05aa
ms.openlocfilehash: c105f4fae3b3fffb61ef892cecbbe75754ccfd28
ms.contentlocale: es-es
ms.lasthandoff: 04/15/2017

---
# <a name="sql-server-data-files-in-microsoft-azure"></a>Archivos de datos de SQL Server en Microsoft Azure
  ![Archivos de datos en Azure](../../relational-databases/databases/media/data-files-on-azure.png "Archivos de datos en Azure")  
  
 Archivos de datos de SQL Server en Microsoft Azure habilita la compatibilidad nativa para los archivos de base de datos de SQL Server almacenados como blobs de Microsoft Azure. Permite crear una base de datos de SQL Server que se ejecuta en el entorno local o en una máquina virtual de Microsoft Azure con una ubicación de almacenamiento dedicada para los datos de almacenamiento de blobs de Microsoft Azure. Esta mejora simplifica especialmente el traslado de bases de datos entre equipos mediante operaciones de separar y adjuntar. Además, proporciona una ubicación de almacenamiento alternativa para los archivos de copia de seguridad de la base de datos, lo que permite realizar la restauración desde o hasta Almacenamiento de Microsoft Azure. Por tanto, habilita diversas soluciones híbridas al aportar varias ventajas en cuanto a virtualización de datos, movimiento de datos, seguridad y disponibilidad, así como costos y mantenimiento reducidos para lograr escalado flexible y alta disponibilidad.
 
> [AZURE.IMPORTANT]Almacenar bases de datos del sistema en Blob Storage de Azure no es recomendable y no se admite. 
  
 En este tema se describen los conceptos y los factores básicos a la hora de almacenar archivos de datos de SQL Server en el Servicio de almacenamiento de Microsoft Azure.  
  
 Para ver una experiencia práctica sobre cómo usar esta nueva característica, consulte [Tutorial: Using the Microsoft Azure Blob storage service with SQL Server 2016 databases ](https://msdn.microsoft.com/library/dn466438.aspx)(Tutorial: Uso del servicio Blob Storage de Microsoft Azure con bases de datos de SQL Server 2016).  
  
## <a name="why-use-sql-server-data-files-in-microsoft-azure"></a>¿Por qué usar archivos de datos de SQL Server en Microsoft Azure? 
  
-   **Ventajas de una migración fácil y rápida:** esta característica simplifica el proceso de migración, para lo cual mueve una base de datos cada vez entre equipos locales así como entre entornos locales y entornos en la nube sin cambios de la aplicación. Por tanto, admite una migración incremental a la vez que conserva la infraestructura local existente. Además, tener acceso a un almacenamiento de datos centralizado simplifica la lógica de la aplicación en los casos en los que una aplicación deba ejecutarse en varias ubicaciones en un entorno local. En algunos casos, es posible que necesite configurar rápidamente centros informáticos en ubicaciones geográficamente dispersas, que recopilen datos de muchas fuentes diferentes. Con esta nueva mejora, en lugar de mover datos de una ubicación a otra, puede almacenar muchas bases de datos como blobs de Microsoft Azure y después ejecutar scripts Transact-SQL para crear bases de datos en equipos locales o máquinas virtuales.  
  
-   **Ventajas en el costo y almacenamiento ilimitado:** esta característica le permite disponer de almacenamiento externo ilimitado en Microsoft Azure mientras aprovecha los recursos informáticos locales. Si usa Microsoft Azure como ubicación de almacenamiento, puede centrarse tranquilamente en la lógica de la aplicación sin la sobrecarga de administración de hardware. Si pierde un nodo de proceso local, puede configurar uno nuevo sin tener que mover datos.  
  
-   **Ventajas de alta disponibilidad y recuperación ante desastres:** el uso de la característica Archivos de datos de SQL Server en Microsoft Azure puede simplificar las soluciones de alta disponibilidad y recuperación ante desastres. Por ejemplo, si se bloquea una máquina virtual en Microsoft Azure o una instancia de SQL Server, puede volver a crear las bases de datos en una instancia nueva de SQL Server simplemente restableciendo vínculos a los blobs de Microsoft Azure.  
  
-   **Ventajas de seguridad:** esta nueva mejora le permite separar una instancia de proceso de una instancia de almacenamiento. Puede tener una base de datos completamente cifrada donde el descifrado solo se produce en una instancia de proceso, pero no en una instancia de almacenamiento. Es decir, con esta nueva mejora, puede cifrar todos los datos de la nube pública mediante certificados de cifrado de datos transparente (TDE), que están separados físicamente de los datos. Las claves TDE se pueden almacenar en la base de datos maestra, la cual se almacena localmente en el equipo local protegido físicamente y con copia de seguridad local. Puede usar estas claves locales para cifrar los datos que se encuentran en Almacenamiento de Microsoft Azure. Si roban las credenciales de la cuenta de almacenamiento en la nube, los datos seguirán estando protegidos ya que los certificados TDE siempre se encuentran en el entorno local.  
  
-   **Copia de seguridad de instantánea:**  esta característica le permite usar las instantáneas de Azure para proporcionar copias de seguridad prácticamente instantáneas y restauraciones más rápidas de los archivos de base de datos almacenados mediante el servicio de almacenamiento de blobs de Azure. Esta función permite simplificar las directivas de copia de seguridad y restauración. Para obtener más información, vea [Copias de seguridad de instantánea de archivos para archivos de base de datos de Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md).  
  
## <a name="concepts-and-requirements"></a>Conceptos y requisitos  
  
### <a name="azure-storage-concepts"></a>Conceptos de Azure Storage  
 Cuando use la característica Archivos de datos de SQL Server en Windows Azure, debe crear una cuenta de almacenamiento y un contenedor en Windows Azure. A continuación, debe crear una credencial de SQL Server, que incluye información sobre la directiva del contenedor así como una firma de acceso compartido, la cual resulta necesaria para tener acceso al contenedor.  
  
 En [Microsoft Azure](https://azure.microsoft.com), una cuenta de [Azure Storage](https://azure.microsoft.com/services/storage/) representa el nivel superior del espacio de nombres para tener acceso a los blobs. Una cuenta de almacenamiento puede contener un número ilimitado de contenedores, siempre que su tamaño total sea inferior a 500 TB. Para obtener la información más reciente acerca de los límites de almacenamiento, vea [Azure Subscription and Service Limits, Quotas, and Constraints](http://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/). Un contenedor proporciona una agrupación de un conjunto de [blobs](https://azure.microsoft.com/documentation/articles/storage-introduction/#blob-storage). Todos los blobs deben estar en un contenedor. Una cuenta puede contener un número ilimitado de contenedores. De forma similar, un contenedor puede almacenar un número ilimitado de blobs igualmente. Se pueden almacenar dos tipos de blobs en Azure Storage: blobs en bloques y blobs en páginas. Esta nueva característica utiliza blobs en páginas, que pueden tener un tamaño de hasta 1 TB y son más eficaces cuando los intervalos de bytes en el archivo se modifican con frecuencia. Puede obtener acceso a blobs mediante el siguiente formato de dirección URL: `http://storageaccount.blob.core.windows.net/<container>/<blob>`.  
  
### <a name="azure-billing-considerations"></a>Consideraciones sobre la facturación de Azure  
 Estimar el costo de usar los servicios de Azure es una cuestión importante a la hora de tomar decisiones y en el proceso de planeamiento. Al almacenar archivos de datos de SQL Server en Azure Storage, deberá correr con los gastos asociados al almacenamiento y las transacciones. Además, la implementación de la característica Archivos de datos de SQL Server en Azure Storage requiere una renovación de la concesión de blobs cada 45-60 segundos de forma implícita. Esto también ocasiona costos de transacción por archivo de base de datos, como .mdf y .ldf. Según nuestras estimaciones, el costo por renovar las concesiones para dos archivos de base de datos (.mdf y .ldf) sería de unos 2 centavos al mes según el modelo actual de precios. Recomendamos usar la información de la página [Precios de Azure](http://azure.microsoft.com/pricing/) como ayuda para estimar los costos mensuales asociados al uso de Azure Storage y Máquinas virtuales de Azure.  
  
### <a name="sql-server-concepts"></a>Conceptos de SQL Server  
 Cuando use esta nueva mejora, deberá hacer lo siguiente:  
  
-   Es preciso que cree una directiva en un contenedor y que genere una clave de firma de acceso compartido (SAS).  
  
-   Para cada contenedor utilizado por un archivo de datos o de registro, debe crear una credencial de SQL Server cuyo nombre coincida con la ruta de acceso del contenedor.  
  
-   Debe almacenar la información sobre el contenedor de Azure Storage, su nombre de directiva asociado y la clave SAS en el almacén de credenciales de SQL Server.  
  
 En el ejemplo siguiente se da por supuesto que se ha creado un contenedor de almacenamiento de Azure, así como una directiva con derechos de lectura, escritura y lista. Cuando se crea una directiva en un contenedor, se genera una clave SAS que podrá guardar en la memoria de forma segura sin cifrar y que necesita SQL Server para acceder a los archivos de blob en el contenedor. En el siguiente fragmento de código, reemplace `'your SAS key'` por una entrada similar a la siguiente: `'sr=c&si=<MYPOLICYNAME>&sig=<THESHAREDACCESSSIGNATURE>'`. Para obtener más información, consulte [Manage anonymous read access to containers and blobs (Administración del acceso de lectura anónimo a contenedores y blobs)](http://azure.microsoft.com/en-us/documentation/articles/storage-manage-access-to-resources/).  
  
```  
  
-- Create a credential  
CREATE CREDENTIAL [https://testdb.blob.core.windows.net/data]  
WITH IDENTITY='SHARED ACCESS SIGNATURE',  
SECRET = 'your SAS key'  
  
-- Create database with data and log files in Windows Azure container.  
CREATE DATABASE testdb   
ON  
( NAME = testdb_dat,  
    FILENAME = 'https://testdb.blob.core.windows.net/data/TestData.mdf' )  
 LOG ON  
( NAME = testdb_log,  
    FILENAME =  'https://testdb.blob.core.windows.net/data/TestLog.ldf')  
  
```  
  
 **Nota importante:** si hay referencias activas a archivos de datos de un contenedor, cualquier intento de eliminar la credencial correspondiente de SQL Server generará un error.  
  
### <a name="security"></a>Seguridad  
 A continuación se describen las consideraciones y los requisitos relativos a la seguridad cuando se almacenan archivos de datos de SQL Server en Azure Storage.  
  
-   Al crear un contenedor para el servicio Blob Storage de Azure, se recomienda establecer el acceso en privado. Al establecer el acceso en privado, solo el propietario de la cuenta de Azure puede leer el contenedor y los datos de blob.  
  
-   Cuando se almacenan archivos de la base de datos de SQL Server en Azure Storage, debe usar una firma de acceso compartido, un URI que concede derechos de acceso restringido a contenedores, blobs, colas y tablas. El uso de una firma de acceso compartido permite que SQL Server obtenga acceso a recursos de su cuenta de almacenamiento sin compartir la clave de su cuenta de Azure Storage.  
  
-   Por otra parte, se recomienda que siga implementando los procedimientos habituales de seguridad locales para las bases de datos.  
  
### <a name="installation-prerequisites"></a>Requisitos previos de la instalación  
 A continuación se describen los requisitos previos de instalación cuando se almacenan archivos de datos de SQL Server en Azure.  
  
-   **SQL Server local:** la versión SQL Server 2016 incluye esta característica. Para obtener información sobre cómo descargar SQL Server 2016, consulte [SQL Server 2016](https://www.microsoft.com/en-us/cloud-platform/sql-server).  
  
-   SQL Server que se ejecuta en una máquina virtual de Azure: si va a instalar [SQL Server en una máquina virtual de Azure](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm), instale SQL Server 2016 o actualice la instancia existente. Del mismo modo, también puede crear una nueva máquina virtual de Azure mediante una imagen de plataforma de SQL Server 2016.

  
###  <a name="bkmk_Limitations"></a> Limitaciones  
  
-   En la versión actual de esta característica, no se admite almacenar datos **FileStream** en Azure Storage. Puede almacenar datos de **FILESTREAM** en una base de datos local integrada de Azure Storage, pero no puede mover datos de FILESTREAM entre equipos con Azure Storage. Para los datos **FileStream** , se recomienda que siga usando las técnicas tradicionales para mover archivos (.mdf, .ldf) asociadas con Filestream entre varios equipos.  
  
-   Actualmente, esta nueva mejora no admite que más de una instancia de SQL Server tenga acceso a los mismos archivos de base de datos de Azure Storage al mismo tiempo. Si el ServidorA está en línea con un archivo de base de datos activo y el ServidorB se inicia accidentalmente y tiene también una base de datos que apunta al mismo archivo de datos, el segundo servidor no podrá iniciar la base de datos y se generará un error con un código **5120 No se puede abrir el archivo físico "%.\*ls". Error del sistema operativo %d: "%ls"**.  
  
-   Solo los archivos .mdf, .ldf y .ndf se pueden almacenar en Azure Storage con la característica Archivos de datos de SQL Server en Azure.  
  
-   Cuando se utiliza la característica Archivos de datos de SQL Server en Azure, no se admite la replicación geográfica para la cuenta de almacenamiento. Si se realiza la replicación geográfica en la cuenta de almacenamiento y se produce una conmutación por error geográfica, se dañará la base de datos.  
  
-   Cada blob puede tener un tamaño máximo de 1 TB. Esto crea un límite superior en cuanto a los archivos de datos y de registro de base de datos individuales que se pueden almacenar en Azure Storage.  
  
-   No es posible almacenar datos de OLTP en memoria en el Blob de Azure con la característica Archivos de datos de SQL Server en Azure Storage. Esto se debe a que OLTP en memoria tiene una dependencia de **FileStream** y, en la versión actual de esta característica, no se admite almacenar datos **FileStream** en Azure Storage.  
  
-   Cuando se utiliza la característica Archivos de datos de SQL Server en Azure, SQL Server realiza todas las comparaciones de direcciones URL o de rutas de acceso de archivo mediante la Intercalación establecida en la base de datos **master** .  
  
-   Se admiten**grupos de disponibilidad AlwaysOn** siempre y cuando no agregue nuevos archivos de base de datos a la base de datos principal. Si una operación de base de datos requiere que se cree un nuevo archivo en la base de datos principal, en primer lugar, deshabilite los grupos de disponibilidad AlwaysOn en el nodo secundario. Posteriormente, realice la operación de base de datos en la base de datos principal y haga una copia de seguridad de la base de datos en el nodo principal. Después, restaure la base de datos al nodo secundario y habilite los grupos de disponibilidad AlwaysOn en el nodo secundario. Tenga en cuenta que las instancias de clúster de conmutación por error de AlwaysOn no se admiten cuando se usa la característica Archivos de datos de SQL Server en Azure.  
  
-   Durante el funcionamiento normal, SQL Server utiliza concesiones temporales con el fin de reservar y almacenar blobs con una renovación de cada concesión de blob cada 45-60 segundos. Si se bloquea un servidor y se inicia otra instancia de SQL Server configurada para usar los mismos blobs, la instancia nueva esperará hasta 60 segundos para que expire la concesión existente del blob. Si desea adjuntar la base de datos a otra instancia y no puede esperar 60 segundos a que expire la concesión, puede detener explícitamente la concesión en el blob para evitar errores en las operaciones de adjuntar.  
  
## <a name="tools-and-programming-reference-support"></a>Herramientas y compatibilidad con referencia de programación  
 En esta sección se describen las herramientas y las bibliotecas de referencia de programación que se pueden utilizar al almacenar archivos de datos de SQL Server en Azure Storage.  
  
### <a name="powershell-support"></a>Compatibilidad con PowerShell  
 Use cmdlets de PowerShell para almacenar archivos de datos de SQL Server en el servicio Blob Storage de Azure; para ello, se debe hacer referencia a una ruta de acceso de dirección URL de Blob Storage en lugar de a una ruta de acceso de archivos. Acceso a Blobs mediante el formato de dirección URL siguiente: `http://storageaccount.blob.core.windows.net/<container>/<blob>` .  
  
### <a name="sql-server-object-and-performance-counters-support"></a>Objetos de SQL Server y compatibilidad con contadores de rendimiento  
 A partir de SQL Server 2014, se ha agregado un nuevo objeto de SQL Server que se usará con la característica Archivos de datos de SQL Server en Azure Storage. El nuevo objeto de SQL Server se denomina [SQL Server, HTTP_STORAGE_OBJECT](../../relational-databases/performance-monitor/sql-server-http-storage-object.md) y lo puede usar el Monitor de sistema para supervisar la actividad cuando se ejecuta SQL Server con Almacenamiento de Windows Azure.  
  
### <a name="sql-server-management-studio-support"></a>Compatibilidad con SQL Server Management Studio  
 SQL Server Management Studio le permite usar esta característica a través de varias ventanas de diálogo. Por ejemplo, puede escribir la ruta de acceso de dirección URL del contenedor de almacenamiento, como > https://teststorageaccnt.blob.core.windows.net/testcontainer/ :
 
 como una **Ruta de acceso** en varias ventanas de diálogo, como **Nueva base de datos**, **Adjuntar base de datos** y **Restaurar base de datos**. Para obtener más información, consulte [Tutorial: Using the Microsoft Azure Blob storage service with SQL Server 2016 databases](https://msdn.microsoft.com/library/dn466438.aspx)(Tutorial: Uso del servicio Blob Storage de Microsoft Azure con bases de datos de SQL Server 2016).  
  
### <a name="sql-server-management-objects-support"></a>Compatibilidad con Objetos de administración de SQL Server  
 Cuando se usa la característica Archivos de datos de SQL Server en Azure, se admiten todos los Objetos de administración de SQL Server (SMO). Si un objeto SMO requiere una ruta de acceso, use el formato de dirección URL BLOB en lugar de una ruta de acceso de archivos local, como `https://teststorageaccnt.blob.core.windows.net/testcontainer/`. Para obtener más información sobre Objetos de administración de SQL Server (SMO), vea [Guía de programación para objetos de administración de SQL Server &#40;SMO&#41;](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)en los Libros en pantalla de SQL Server.  
  
### <a name="transact-sql-support"></a>Compatibilidad con Transact-SQL  
 Esta nueva característica presenta el siguiente cambio en el área expuesta de Transact-SQL:  
  
-   Una nueva columna **int** , **credential_id**, en la vista del sistema **sys.master_files** . La columna **credential_id** se usa para permitir la referencia cruzada en sys.credentials de los archivos de datos habilitados en Almacenamiento de Windows Azure para las credenciales creadas para ellos. Puede usarla para solucionar problemas, como que una credencial no se puede eliminar cuando un archivo de base de datos la está usando.  
  
##  <a name="bkmk_Troubleshooting"></a> Solución de problemas de Archivos de datos de SQL Server en Microsoft Azure  
 Para evitar errores por funciones no admitidas o limitaciones, primero consulte [Limitations](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md#bkmk_Limitations).  
  
 La lista de errores que puede obtener cuando se usa la característica Archivos de datos de SQL Server en Azure Storage es la siguiente:  
  
 **Errores de autenticación**  
  
-   *No se puede quitar la credencial '%.\*ls' porque la usa un archivo de base de datos activo.*   
    Solución: puede ver este error si intenta quitar una credencial que todavía esté utilizando un archivo de base de datos activo en Azure Storage. Para quitar la credencial, en primer lugar, debe eliminar el blob asociado que tiene este archivo de base de datos. Para eliminar un blob que tiene una concesión activa, debe interrumpir primero la concesión.  
  
-   *No se ha creado correctamente la firma de acceso compartido en el contenedor.*   
     Solución: asegúrese de haber creado correctamente una firma de acceso compartido en el contenedor. Revise las instrucciones de la lección 2 de [Tutorial: Using the Microsoft Azure Blob storage service with SQL Server 2016 databases ](https://msdn.microsoft.com/library/dn466435.aspx)(Tutorial: Uso del servicio Blob Storage de Microsoft Azure con bases de datos de SQL Server 2016).  
  
-   *La credencial de SQL Server no se ha creado correctamente.*   
    Solución: asegúrese de que ha usado "Firma de acceso compartido" para el campo **Identidad** y que ha creado un secreto correctamente. Revise las instrucciones de la lección 3 de [Tutorial: Using the Microsoft Azure Blob storage service with SQL Server 2016 databases](https://msdn.microsoft.com/library/dn466436.aspx)(Tutorial: Uso del servicio Blob Storage de Microsoft Azure con bases de datos de SQL Server 2016).  
  
 **Errores de concesión de blobs:**  
  
-   Error al intentar iniciar SQL Server después de que otra instancia que usa los mismos archivos de blob se haya bloqueado. Solución: durante el funcionamiento normal, SQL Server utiliza concesiones temporales con el fin de reservar y almacenar blobs con una renovación de cada concesión de blob cada 45-60 segundos. Si se bloquea un servidor y se inicia otra instancia de SQL Server configurada para usar los mismos blobs, la instancia nueva esperará hasta 60 segundos para que expire la concesión existente del blob. Si desea adjuntar la base de datos a otra instancia y no puede esperar 60 segundos a que expire la concesión, puede detener explícitamente la concesión en el blob para evitar errores en las operaciones de adjuntar.  
  
 **Errores de base de datos:**  
  
1.  *Errores al crear una base de datos*   
    Solución: revise las instrucciones de la lección 4 de [Tutorial: Using the Microsoft Azure Blob storage service with SQL Server 2016 databases](https://msdn.microsoft.com/library/dn466431.aspx)(Tutorial: Uso del servicio Blob Storage de Microsoft Azure con bases de datos de SQL Server 2016).  
  
2.  *Errores al ejecutar la instrucción Alter*   
    Solución: asegúrese de ejecutar la instrucción ALTER DATABASE cuando la base de datos esté en línea. Cuando copie archivos de datos en Azure Storage, cree siempre un blob en páginas y no un blob en bloques. De lo contrario, ALTER DATABASE no se ejecutará correctamente. Revise las instrucciones de la lección 7 de [Tutorial: Using the Microsoft Azure Blob storage service with SQL Server 2016 databases](https://msdn.microsoft.com/library/dn466438.aspx)(Tutorial: Uso del servicio Blob Storage de Microsoft Azure con bases de datos de SQL Server 2016).  
  
3.  *Código de error 5120 No se puede abrir el archivo físico "%.\*ls". Error del sistema operativo %d: "%ls"*   
    Solución: actualmente, esta nueva mejora no admite que más de una instancia de SQL Server tenga acceso a los mismos archivos de base de datos de Azure Storage al mismo tiempo. Si el ServidorA está en línea con un archivo de base de datos activo y el ServidorB se inicia accidentalmente y tiene también una base de datos que apunta al mismo archivo de datos, el segundo servidor no podrá iniciar la base de datos y se generará un error con un código *5120 No se puede abrir el archivo físico "%.\*ls". Error del sistema operativo %d: "%ls"*.  
  
     Para resolver este problema, determine en primer lugar si necesita que el Servidor A obtenga acceso al archivo de base de datos de Azure Storage o no. Si no es así, basta con quitar las conexiones entre el Servidor A y los archivos de base de datos de Azure Storage. Para ello, siga estos pasos:  
  
    1.  Establezca la ruta de acceso de ServidorA en una carpeta local mediante la instrucción ALTER DATABASE.  
  
    2.  Ponga la base de datos sin conexión en el ServidorA.  
  
    3.  Luego copie los archivos de base de datos de Azure Storage en la carpeta local del Servidor A. Esto garantiza que el Servidor A siga conservando localmente una copia de la base de datos.  
  
    4.  Ponga la base de datos en línea.  

  
  

