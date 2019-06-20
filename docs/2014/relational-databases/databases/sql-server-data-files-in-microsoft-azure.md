---
title: Archivos de datos SQL Server en Windows Azure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
ms.assetid: 38ffd9c2-18a5-43d2-b674-e425addec4e4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 588e656ca71bc5843e3483879f5a58951373aff5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62916589"
---
# <a name="sql-server-data-files-in-windows-azure"></a>Archivos de datos de SQL Server en Windows Azure
  Archivos de datos de SQL Server en Windows Azure habilita la compatibilidad nativa para los archivos de base de datos de SQL Server almacenados como Blobs de Windows Azure. Permite crear una base de datos de SQL Server que se ejecuta en el entorno local o en una máquina virtual de Microsoft Azure con una ubicación de almacenamiento dedicada para los datos de Microsoft Azure Blob Storage. Esta mejora simplifica especialmente el traslado de bases de datos entre equipos mediante operaciones de separar y adjuntar. Además, proporciona una ubicación de almacenamiento alternativa para los archivos de copia de seguridad de la base de datos, lo que permite realizar la restauración desde o hasta Azure Storage. Por tanto, habilita diversas soluciones híbridas al aportar varias ventajas en cuanto a virtualización de datos, movimiento de datos, seguridad y disponibilidad, así como costos y mantenimiento reducidos para lograr escalado flexible y alta disponibilidad.  
  
 En este tema se describen los conceptos y los factores básicos a la hora de almacenar archivos de datos de SQL Server en el Servicio de almacenamiento de Microsoft Azure.  
  
 Para experimentar de manera práctica cómo usar esta nueva característica, consulte el [Tutorial: Archivos de datos de SQL Server en el servicio de almacenamiento de Windows Azure](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
 En el diagrama siguiente se muestra que esta mejora permite almacenar archivos de base de datos de SQL Server como blobs de Microsoft Azure en Azure Storage, independientemente de dónde resida el servidor.  
  
 ![SQL Server Integration con almacenamiento de Azure](../../database-engine/media/sql-server-dbfiles-stored-as-blobs.gif "SQL Server Integration con almacenamiento de Azure")  
  
## <a name="benefits-of-using-sql-server-data-files-in-windows-azure"></a>Ventajas de utilizar Archivos de datos de SQL Server en Windows Azure  
  
-   **Ventajas de una migración rápida y sencilla:** Esta característica simplifica el proceso de migración al mover una base de datos cada vez entre equipos locales como así como entre local y entornos sin cambios en las aplicaciones en la nube. Por tanto, admite una migración incremental a la vez que conserva la infraestructura local existente. Además, tener acceso a un almacenamiento de datos centralizado simplifica la lógica de la aplicación en los casos en los que una aplicación deba ejecutarse en varias ubicaciones en un entorno local. En algunos casos, es posible que necesite configurar rápidamente centros informáticos en ubicaciones geográficamente dispersas, que recopilen datos de muchas fuentes diferentes. Con esta nueva mejora, en lugar de mover datos de una ubicación a otra, puede almacenar muchas bases de datos como Blobs de Windows Azure y, posteriormente, ejecutar scripts Transact-SQL para crear bases de datos en equipos locales o máquinas virtuales.  
  
-   **Ventajas económicas y de espacio de almacenamiento ilimitado:** Esta característica permite tener almacenamiento externo ilimitado en Windows Azure mientras aprovecha un entorno local de los recursos informáticos. Si usa Windows Azure como ubicación de almacenamiento, puede centrarse tranquilamente en la lógica de la aplicación sin la sobrecarga de administración de hardware. Si pierde un nodo de proceso local, puede configurar uno nuevo sin tener que mover datos.  
  
-   **Ventajas de la alta disponibilidad y recuperación ante desastres:** Uso de archivos de datos de SQL Server en la característica de Windows Azure puede simplificar las soluciones de recuperación ante desastres y disponibilidad alta. Por ejemplo, si se bloquea una máquina virtual en Windows Azure o una instancia de SQL Server, puede volver a crear las bases de datos en un equipo nuevo simplemente restableciendo vínculos en blobs de Windows Azure.  
  
-   **Ventajas de seguridad:** Esta nueva mejora le permite separar una instancia de proceso de una instancia de almacenamiento. Puede tener una base de datos completamente cifrada donde el descifrado solo se produce en una instancia de proceso, pero no en una instancia de almacenamiento. Es decir, con esta nueva mejora, puede cifrar todos los datos de la nube pública mediante certificados de cifrado de datos transparente (TDE), que están separados físicamente de los datos. Las claves TDE se pueden almacenar en la base de datos maestra, la cual se almacena localmente en el equipo local protegido físicamente y con copia de seguridad íntegra. Puede utilizar estas claves locales para cifrar los datos que se encuentran en Azure Storage. Si roban las credenciales de la cuenta de almacenamiento en la nube, los datos seguirán estando protegidos ya que los certificados TDE siempre se encuentran en el entorno local.  
  
## <a name="concepts-and-requirements"></a>Conceptos y requisitos  
  
### <a name="windows-azure-storage-concepts"></a>Conceptos de Almacenamiento de Windows Azure  
 Cuando use la característica Archivos de datos de SQL Server en Windows Azure, debe crear una cuenta de almacenamiento y un contenedor en Windows Azure. A continuación, debe crear una credencial de SQL Server, que incluye información sobre la directiva del contenedor así como una firma de acceso compartido, la cual resulta necesaria para tener acceso al contenedor.  
  
 En Windows Azure, una cuenta de almacenamiento representa el nivel superior del espacio de nombres para tener acceso a los blobs. Una cuenta de almacenamiento puede contener un número ilimitado de contenedores, siempre que su tamaño total sea inferior a 500 TB. Para obtener la información más reciente acerca de los límites de almacenamiento, vea [Suscripciones de Azure y límites de servicio, cuotas y restricciones](http://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/). Un contenedor proporciona una agrupación de un conjunto de blobs. Todos los blobs deben estar en un contenedor. Una cuenta puede contener un número ilimitado de contenedores. De forma similar, un contenedor puede almacenar un número ilimitado de blobs igualmente. Se pueden almacenar dos tipos de blobs en Almacenamiento de Windows Azure: blobs en bloques y blobs en páginas. Esta nueva característica utiliza blobs en páginas, que pueden tener un tamaño de hasta 1 TB y son más eficaces cuando los intervalos de bytes en el archivo se modifican con frecuencia. Puede obtener acceso a blobs mediante el siguiente formato de dirección URL: `http://storageaccount.blob.core.windows.net/<container>/<blob>`.  
  
### <a name="windows-azure-billing-considerations"></a>Consideraciones sobre la facturación de Windows Azure  
 Estimar el costo de usar los servicios de Windows Azure es una cuestión importante a la hora de tomar decisiones y en el proceso de planeamiento. Al almacenar archivos de datos de SQL Server en Almacenamiento de Windows Azure, deberá correr con los gastos asociados al almacenamiento y las transacciones. Además, la implementación de la característica Archivos de datos de SQL Server en Almacenamiento de Windows Azure requiere una renovación de la concesión de blobs cada 45-60 segundos de forma implícita. Esto también ocasiona costos de transacción por archivo de base de datos, como .mdf y .ldf. Según nuestras estimaciones, el costo por renovar las concesiones para dos archivos de base de datos (.mdf y .ldf) sería de unos 2 centavos al mes según el modelo actual de precios. Recomendamos usar la información de la página [Precios de Azure](http://azure.microsoft.com/pricing/) como ayuda para estimar los costos mensuales asociados al uso de Almacenamiento de Microsoft Azure y Máquinas virtuales de Microsoft Azure.  
  
### <a name="sql-server-concepts"></a>Conceptos de SQL Server  
 Cuando use esta nueva mejora, deberá hacer lo siguiente:  
  
-   Es preciso que cree una directiva en un contenedor y que genere una clave de firma de acceso compartido (SAS).  
  
-   Para cada contenedor utilizado por un archivo de datos o de registro, debe crear una credencial de SQL Server cuyo nombre coincida con la ruta de acceso del contenedor.  
  
-   Debe almacenar la información sobre el contenedor de Azure Storage, su nombre de directiva asociado y la clave SAS en el almacén de credenciales de SQL Server.  
  
 En el ejemplo siguiente se da por supuesto que se ha creado un contenedor de Azure Storage, así como una directiva con derechos de lectura, escritura y lista. Cuando se crea una directiva en un contenedor, se genera una clave SAS que podrá guardar en la memoria de forma segura sin cifrar y que necesita SQL Server para acceder a los archivos de blob en el contenedor. En el siguiente fragmento de código, reemplace `'your SAS key'` por una entrada similar a la siguiente: `'sr=c&si=<MYPOLICYNAME>&sig=<THESHAREDACCESSSIGNATURE>'`. Para obtener más información, consulte [crear y usar una firma de acceso compartido](https://msdn.microsoft.com/library/azure/jj721951.aspx)  
  
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
  
 **Nota importante:** Si hay referencias activas a archivos de datos en un contenedor, intenta eliminar el correspondiente se produce un error en la credencial de SQL Server.  
  
### <a name="security"></a>Seguridad  
 A continuación se describen las consideraciones y los requisitos relativos a la seguridad cuando se almacenan archivos de datos SQL Server en Almacenamiento de Windows Azure.  
  
-   Al crear un contenedor para el servicio de almacenamiento Blob de Windows Azure, se recomienda establecer el acceso en privado. Al establecer el acceso en privado, solo el propietario de la cuenta de Windows Azure puede leer el contenedor y los datos de blob.  
  
-   Cuando se almacenan archivos de la base de datos de SQL Server en Almacenamiento de Windows Azure, debe usar una firma de acceso compartido, un URI que concede derechos de acceso restringido a contenedores, blobs, colas y tablas. El uso de una firma de acceso compartido permite que SQL Server obtenga acceso a recursos de su cuenta de almacenamiento sin compartir la clave de su cuenta de almacenamiento de Windows Azure.  
  
-   Por otra parte, se recomienda que siga implementando los procedimientos habituales de seguridad locales para las bases de datos.  
  
### <a name="installation-prerequisites"></a>Requisitos previos de la instalación  
 A continuación se describen los requisitos previos de instalación cuando se almacenan archivos de datos de SQL Server en Windows Azure.  
  
-   **SQL Server local:** Versión de SQL Server 2014 incluye esta característica. Para obtener información sobre cómo descargar SQL Server 2014, vea [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx).  
  
-   SQL Server en una máquina virtual de Windows Azure: Si va a instalar a SQL Server en una máquina Virtual de Windows Azure, instale SQL Server 2014 o actualice la instancia existente. Del mismo modo, también puede crear una nueva máquina virtual de Windows Azure mediante una imagen de plataforma de SQL Server 2014. Para obtener información sobre cómo descargar SQL Server 2014, vea [SQL Server 2014](https://www.microsoft.com/sqlserver/sql-server-2014.aspx).  
  
###  <a name="bkmk_Limitations"></a> Limitaciones  
  
-   En la versión actual de esta característica, no se admite almacenar datos `FileStream` en Azure Storage. Puede almacenar datos `Filestream` en una base de datos local integrada de Azure Storage, pero no puede mover datos FILESTREAM entre equipos con Azure Storage. Para los datos `FileStream`, se recomienda que siga usando las técnicas tradicionales para mover archivos (.mdf, .ldf) asociadas con Filestream entre varios equipos.  
  
-   Actualmente, esta nueva mejora no admite que más de una instancia de SQL Server tenga acceso a los mismos archivos de base de datos de Azure Storage al mismo tiempo. Si el ServidorA está en línea con un archivo de base de datos activo y el ServidorB se inicia accidentalmente y tiene también una base de datos que apunta al mismo archivo de datos, el segundo servidor no podrá iniciar la base de datos y se generará un error con un código **5120 No se puede abrir el archivo físico "%.\*ls". Error del sistema operativo %d: "%ls"** .  
  
-   Solo los archivos .mdf, .ldf y .ndf se pueden almacenar en el almacenamiento de Microsoft Azure con la característica Archivos de datos de SQL Server en Microsoft Azure.  
  
-   Cuando se utiliza la característica Archivos de datos de SQL Server en Windows Azure, no se admite la replicación geográfica para la cuenta de almacenamiento. Si se realiza la replicación geográfica en la cuenta de almacenamiento y se produce una conmutación por error geográfica, se dañará la base de datos.  
  
-   Cada blob puede tener un tamaño máximo de 1 TB. Esto crea un límite superior en cuanto a los archivos de datos y de registro de base de datos individuales que se pueden almacenar en Azure Storage.  
  
-   No es posible almacenar datos de OLTP en memoria en el Blob de Microsoft Azure con la característica Archivos de datos de SQL Server en Microsoft Azure. Esto se debe a que OLTP en memoria tiene una dependencia de `FileStream` y, en la versión actual de esta característica, no se admite almacenar datos `FileStream` en Azure Storage.  
  
-   Cuando se utiliza la característica Archivos de datos de SQL Server en Windows Azure, SQL Server realiza todas las comparaciones de direcciones URL o de rutas de acceso de archivo mediante la Intercalación establecida en la base de datos `master`.  
  
-   Se admiten `AlwaysOn Availability Groups` siempre y cuando no agregue nuevos archivos de base de datos a la base de datos principal. Si una operación de base de datos requiere que se cree un nuevo archivo en la base de datos principal, en primer lugar, deshabilite los grupos de disponibilidad AlwaysOn en el nodo secundario. Posteriormente, realice la operación de base de datos en la base de datos principal y haga una copia de seguridad de la base de datos en el nodo principal. A continuación, restaure la base de datos al nodo secundario y habilite los grupos de disponibilidad AlwaysOn en el nodo secundario. Tenga en cuenta que las instancias de clúster de conmutación por error de AlwaysOn no se admiten cuando se utiliza la característica Archivos de datos de SQL Server de Windows Azure.  
  
-   Durante el funcionamiento normal, SQL Server utiliza concesiones temporales con el fin de reservar y almacenar blobs con una renovación de cada concesión de blob cada 45-60 segundos. Si se bloquea un servidor y se inicia otra instancia de SQL Server configurada para usar los mismos blobs, la instancia nueva esperará hasta 60 segundos para que expire la concesión existente del blob. Si desea adjuntar la base de datos a otra instancia y no puede esperar 60 segundos a que expire la concesión, puede detener explícitamente la concesión en el blob para evitar errores en las operaciones de adjuntar.  
  
## <a name="tools-and-programming-reference-support"></a>Herramientas y compatibilidad con referencia de programación  
 En esta sección se describen las herramientas y las bibliotecas de referencia de programación que se pueden utilizar al almacenar archivos de datos de SQL Server en Almacenamiento de Windows Azure.  
  
### <a name="powershell-support"></a>Compatibilidad con PowerShell  
 En SQL Server 2014, puede usar cmdlets de PowerShell para almacenar archivos de datos de SQL Server en el servicio de almacenamiento Blob de Windows Azure; para ello, se debe hacer referencia a una ruta de acceso de dirección URL de almacenamiento Blob en lugar de a una ruta de acceso de archivos. Puede obtener acceso a blobs mediante el siguiente formato de dirección URL:`: http://storageaccount.blob.core.windows.net/<container>/<blob>` .  
  
### <a name="sql-server-object-and-performance-counters-support"></a>Objetos de SQL Server y compatibilidad con contadores de rendimiento  
 A partir de SQL Server 2014, se ha agregado un nuevo objeto de SQL Server que se usará con la característica Archivos de datos de SQL Server en Azure Storage. El nuevo objeto de SQL Server se denomina [SQL Server, HTTP_STORAGE_OBJECT](../performance-monitor/sql-server-http-storage-object.md) y lo puede usar el Monitor de sistema para supervisar la actividad cuando se ejecuta SQL Server con Almacenamiento de Windows Azure.  
  
### <a name="sql-server-management-studio-support"></a>Compatibilidad con SQL Server Management Studio  
 SQL Server Management Studio le permite usar esta característica a través de varias ventanas de diálogo. Por ejemplo, puede escribir la ruta de acceso de la dirección URL del contenedor de almacenamiento, de esta forma: `https://teststorageaccnt.blob.core.windows.net/testcontainer/` como una **Ruta de acceso** en varias ventanas de diálogo, como **Nueva base de datos**, **Adjuntar base de datos**y **Restaurar base de datos**. Para más información, consulte el [Tutorial: Archivos de datos de SQL Server en el servicio de almacenamiento de Windows Azure](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
### <a name="sql-server-management-objects-support"></a>Compatibilidad con Objetos de administración de SQL Server  
 Cuando se usa la característica Archivos de datos de SQL Server en Windows Azure, se admiten todos los Objetos de administración de SQL Server (SMO). Si un objeto SMO requiere una ruta de acceso, use el formato de dirección URL BLOB en lugar de una ruta de acceso de archivos local, como `https://teststorageaccnt.blob.core.windows.net/testcontainer/`. Para obtener más información sobre Objetos de administración de SQL Server (SMO), vea [Guía de programación para objetos de administración de SQL Server &#40;SMO&#41;](../server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)en los Libros en pantalla de SQL Server.  
  
### <a name="transact-sql-support"></a>Compatibilidad con Transact-SQL  
 Esta nueva característica presenta el siguiente cambio en el área expuesta de Transact-SQL:  
  
-   Una nueva columna **int** , **credential_id**, en la vista del sistema **sys.master_files** . La columna **credential_id** se usa para permitir la referencia cruzada en sys.credentials de los archivos de datos habilitados en Almacenamiento de Windows Azure para las credenciales creadas para ellos. Puede usarla para solucionar problemas, como que una credencial no se puede eliminar cuando un archivo de base de datos la está usando.  
  
##  <a name="bkmk_Troubleshooting"></a> Solución de problemas de archivos de datos SQL Server en Windows Azure  
 Para evitar errores por funciones no admitidas o limitaciones, primero consulte [Limitations](sql-server-data-files-in-microsoft-azure.md#bkmk_Limitations).  
  
 La lista de errores que puede obtener cuando se usa la característica Archivos de datos de SQL Server en Azure Storage es la siguiente:  
  
 **Errores de autenticación**  
  
-   *No se puede quitar la credencial '%.\*ls' porque la usa un archivo de base de datos activo.*    
    Solución: puede ver este error si intenta quitar una credencial que todavía esté utilizando un archivo de base de datos activo en Azure Storage. Para quitar la credencial, en primer lugar, debe eliminar el blob asociado que tiene este archivo de base de datos. Para eliminar un blob que tiene una concesión activa, debe interrumpir primero la concesión.  
  
-   *No se ha creado correctamente la firma de acceso compartido en el contenedor.*    
     Solución: Asegúrese de que ha creado una firma de acceso compartido en el contenedor correctamente. Consulte las instrucciones de la lección 2 del [Tutorial: Archivos de datos de SQL Server en el servicio de almacenamiento de Windows Azure](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
-   *La credencial de SQL Server no se ha creado correctamente.*    
    Solución: asegúrese de que ha usado "Firma de acceso compartido" en el campo **Identidad** y que ha creado un secreto correctamente. Consulte las instrucciones de la lección 3 del [Tutorial: Archivos de datos de SQL Server en el servicio de almacenamiento de Windows Azure](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
 **Errores de concesión de blobs:**  
  
-   Error al intentar iniciar SQL Server después de que otra instancia que usa los mismos archivos de blob se haya bloqueado. Solución: Durante el funcionamiento normal, SQL Server utiliza concesiones temporales con el fin de reservar y almacenar blobs con una renovación de cada concesión de blob cada 45-60 segundos. Si se bloquea un servidor y se inicia otra instancia de SQL Server configurada para usar los mismos blobs, la instancia nueva esperará hasta 60 segundos para que expire la concesión existente del blob. Si desea adjuntar la base de datos a otra instancia y no puede esperar 60 segundos a que expire la concesión, puede detener explícitamente la concesión en el blob para evitar errores en las operaciones de adjuntar.  
  
 **Errores de base de datos:**  
  
1.  *Errores al crear una base de datos*   
    Solución: Consulte las instrucciones de la lección 4 del [Tutorial: Archivos de datos de SQL Server en el servicio de almacenamiento de Windows Azure](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
2.  *Errores al ejecutar la instrucción Alter*   
    Solución: Asegúrese de ejecutar la instrucción Alter Database cuando la base de datos está en línea. Cuando copie archivos de datos en Azure Storage, cree siempre un blob en páginas y no un blob en bloques. De lo contrario, ALTER DATABASE no se ejecutará correctamente. Consulte las instrucciones de la lección 7 del [Tutorial: Archivos de datos de SQL Server en el servicio de almacenamiento de Windows Azure](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md).  
  
3.  *Código de error 5120 No se puede abrir el archivo físico "%.\*ls". Error del sistema operativo %d: "%ls"*    
    Solución: Actualmente, esta nueva mejora no admite que más de una instancia de SQL Server tenga acceso a los mismos archivos de base de datos de Azure Storage al mismo tiempo. Si el ServidorA está en línea con un archivo de base de datos activo y el ServidorB se inicia accidentalmente y tiene también una base de datos que apunta al mismo archivo de datos, el segundo servidor no podrá iniciar la base de datos y se generará un error con un código *5120 No se puede abrir el archivo físico "%.\*ls". Error del sistema operativo %d: "%ls"* .  
  
     Para resolver este problema, determine en primer lugar si necesita que el ServidorA obtenga acceso al archivo de base de datos de Almacenamiento de Windows Azure o no. Si no es así, basta con quitar las conexiones entre el ServidorA y los archivos de base de datos de Almacenamiento de Windows Azure. Para ello, siga estos pasos:  
  
    1.  Establezca la ruta de acceso de ServidorA en una carpeta local mediante la instrucción ALTER DATABASE.  
  
    2.  Ponga la base de datos sin conexión en el ServidorA.  
  
    3.  Luego copie los archivos de base de datos del almacenamiento de Microsoft Azure en la carpeta local del ServidorA. Esto garantiza que el servidorA seguirá conservando localmente una copia de la base de datos.  
  
    4.  Ponga la base de datos en línea.  
  
## <a name="see-also"></a>Vea también  
 [Tutorial: Archivos de datos de SQL Server en el servicio de almacenamiento de Windows Azure](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)  
  
  
