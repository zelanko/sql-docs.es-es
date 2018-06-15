---
title: Adquirir y configurar un servidor de copia de seguridad - almacenamiento de datos paralelos | Documentos de Microsoft
description: En este artículo se describe cómo configurar un sistema de Windows no sea de dispositivo como un servidor de reserva para su uso con las características de copia de seguridad y restauración de Analytics Platform System (APS) y almacenamiento de datos paralelo (PDW).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4464857e2b1e71a96f87e95d45df0577df987176
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539585"
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>Adquirir y configurar un servidor de copia de seguridad para el almacenamiento de datos paralelos
En este artículo se describe cómo configurar un sistema de Windows no sea de dispositivo como un servidor de reserva para su uso con las características de copia de seguridad y restauración de Analytics Platform System (APS) y almacenamiento de datos paralelo (PDW).  
  
  
## <a name="Basics"></a>Conceptos básicos de copia de seguridad de servidor  
El servidor de copia de seguridad:  
  
-   Se proporciona y administra su propio equipo de TI.  
  
-   No requiere herramientas ni software PDW específicas. PDW no instalar el software en el servidor de copia de seguridad.  
  
-   Se encuentra en su propio bastidor no sea de dispositivo y no se puede colocar en el dispositivo de APS.  
  
-   Puede estar conectado a la red InfiniBand de dispositivo. Las copias de seguridad se pueden realizar sobre InfiniBand o Ethernet; InfiniBand es recomendable por razones de rendimiento.  
  
-   Está en su propio dominio de cliente, no el dominio del equipo. No hay ninguna relación de confianza entre el dominio del cliente y el dominio del equipo.  
  
-   Hospeda un recurso compartido de archivo de copia de seguridad, que es un recurso compartido de archivos de Windows que utiliza el protocolo de red de nivel de aplicación de bloque de mensajes del servidor (SMB). Los permisos de recurso compartido de archivo de copia de seguridad conceder a un usuario de dominio de Windows (normalmente es un usuario de copia de seguridad dedicado) la capacidad de realizar la copia de seguridad y restaurar las operaciones en el recurso compartido. Las credenciales de usuario y la contraseña del usuario de dominio de Windows se almacenan en PDW para que pueda realizar copia de seguridad y restaurar las operaciones en el recurso compartido de archivos de copia de seguridad PDW.  
  
## <a name="Step1"></a>Paso 1: Determinar los requisitos de capacidad  
Los requisitos del sistema para el servidor de copia de seguridad dependen casi por completo su propia carga de trabajo. Antes de comprar o aprovisionar un servidor de copia de seguridad debe determinar los requisitos de capacidad. El servidor de copia de seguridad no tiene se dediquen únicamente a las copias de seguridad, siempre que va a controlar los requisitos de almacenamiento y el rendimiento de la carga de trabajo. También puede tener varios servidores de copia de seguridad para copia de seguridad y restaurar cada base de datos a uno de varios servidores.  
  
Use la [hoja de cálculo de planeación de capacidad de servidor de copia de seguridad](backup-capacity-planning-worksheet.md) para ayudar a determinar los requisitos de capacidad.  
  
## <a name="Step2"></a>Paso 2: Adquirir el servidor de copia de seguridad  
Ahora que entender mejor los requisitos de capacidad, puede planear los servidores y los componentes de red que necesitará para adquirir o aprovisionar. Incorporar la siguiente lista de requisitos en el plan de compra y, a continuación, adquirir el servidor o aprovisionar un servidor existente.  
  
### <a name="software-requirements"></a>Requisitos de software  
Cualquier servidor de archivos que usa el protocolo de uso compartido de archivos (SMB) de Windows.  
  
Se recomienda Windows Server 2012 o versiones posteriores para:  
  
-   Obtiene la ventaja de rendimiento de preasignación de archivo a través de SMB.  
  
-   Use la inicialización instantánea de archivos (IFI) para las operaciones de copia de seguridad. El equipo de TI administra esta configuración en el servidor de copia de seguridad. El Administrador de configuración de PDW (dwconfig.exe) no establecido o controlar IFI en el servidor de copia de seguridad. Las versiones anteriores de Windows no tiene IFI, pero aún pueden usarse como servidores de copia de seguridad.  
  
### <a name="networking-requirements"></a>Requisitos de red  
Aunque no es necesario, InfiniBand es el tipo de conexión recomendado para servidores de copia de seguridad. Para prepararse para conectar el servidor de carga a la red InfiniBand de dispositivo:  
  
1.  Plan para el servidor en bastidor lo suficiente para el dispositivo para que se puedan conectarse al dispositivo cambia de InfiniBand. Para obtener más información de las tecnologías de Mellanox de InfiniBand, vea las notas del producto, [Introducción a InfiniBand](http://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf).  
  
2.  Adquirir un adaptador de red de uno o dos puertos Mellanox ConnectX-3 FDR InfiniBand. Se recomienda adquirir el adaptador de red con dos puertos de tolerancia a errores durante la transmisión de datos. Un adaptador de red de dos puerto es necesario para lograr alta disponibilidad.  
  
3.  Comprar 2 cables de InfiniBand FDR para una tarjeta de doble puerto, o 1 cable FDR InfiniBand para una tarjeta de puerto único. Los cables de InfiniBand FDR conectarán el servidor de carga a la red InfiniBand de dispositivo. La longitud del cable depende de la distancia entre el servidor de carga y los conmutadores de InfiniBand del equipo, según su entorno.  
  
## <a name="Step3"></a>Paso 3: Conectar el servidor a las redes InfiniBand  
Siga estos pasos para conectarse al servidor de carga a la red InfiniBand. Si el servidor no está usando la red InfiniBand, omita este paso.  
  
1.  Bastidor del servidor lo suficiente para el dispositivo para que se puedan conectarse a la red InfiniBand de dispositivo.  
  
2.  Instalar al adaptador de red InfiniBand Mellanox ConnectX-3 FDR InfiniBand en el servidor de carga.  
  
3.  Use los cables FDR para conectar el adaptador de red InfiniBand en uno de los dos conmutadores de InfiniBand en el primer bastidor de dispositivo.  
  
4.  Instalar y configurar el controlador de Windows adecuado para el adaptador de red InfiniBand.  
  
    -   InfiniBand controladores para Windows se desarrollan mediante el OpenFabrics Alliance, un consorcio de la industria de proveedores de InfiniBand.  Puede que el controlador correcto se han distribuido con el adaptador de red InfiniBand. De lo contrario, el controlador puede descargarse desde www.openfabrics.org.  
  
5.  Configurar las opciones de InfiniBand y DNS para los adaptadores de red. Para obtener instrucciones de configuración, consulte [configurar adaptadores de red InfiniBand](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Paso 4: Configurar el recurso compartido de archivos de copia de seguridad  
PDW obtendrá acceso al servidor de copia de seguridad a través de un recurso compartido de archivos UNC. Para configurar el recurso compartido de archivos:  
  
1.  Cree una carpeta en el servidor de copia de seguridad para almacenar las copias de seguridad.  
  
2.  Crear un recurso compartido de archivos, llamado a un recurso compartido de copia de seguridad, la carpeta de copia de seguridad.  
  
3.  Designar o crear una cuenta de dominio de Windows en el dominio del usuario que desea usar para los fines de realización de copias de seguridad y restauraciones. Por motivos de seguridad, es mejor usar una cuenta dedicada como usuario de la copia de seguridad.  
  
4.  Agregar permisos para la copia de seguridad compartan para que pueden acceder solo las cuentas de confianza y una cuenta de copia de seguridad de dominio, leer y escriben en la ubicación del recurso compartido.  
  
5.  Agregue las credenciales de cuenta de dominio de reserva a PDW.  
  
    Por ejemplo:  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    Para obtener más información, vea estos procedimientos almacenados:  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>Paso 5: Iniciar copia de seguridad de los datos  
Ahora está listo para iniciar la copia de seguridad de datos en el servidor de copia de seguridad.  
  
Comandos de datos de copia de seguridad, utilice a un cliente de la consulta para conectarse a SQL Server PDW y, a continuación, enviar la copia de seguridad o restaurar base de datos. Usar el disco = cláusula para especificar la ubicación de copia de seguridad y el servidor de copia de seguridad.  
  
> [!IMPORTANT]  
> Recuerde que debe usar la dirección IP de InfiniBand del servidor de copia de seguridad. En caso contrario, se copiarán los datos a través de Ethernet en lugar de InfiniBand.  
  
Por ejemplo:  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
Para obtener más información, vea: 
  
-   [BASE DE DATOS DE COPIA DE SEGURIDAD](../t-sql/statements/backup-database-parallel-data-warehouse.md)   
  
-   [RESTAURAR BASE DE DATOS](../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
## <a name="Security"></a>Avisos de seguridad  
El servidor de copia de seguridad no está unido al dominio privado para la aplicación. Se encuentra en su propia red y no hay ninguna relación de confianza entre su propio dominio y el dominio del equipo privada.  
  
Puesto que las copias de seguridad PDW no están almacenados en el dispositivo, su equipo de TI es responsable de administrar todos los aspectos de la seguridad de copia de seguridad. Por ejemplo, esto incluye administrar la seguridad de los datos de copia de seguridad, la seguridad del servidor utilizado para almacenar las copias de seguridad y la seguridad de la infraestructura de red que conecta el servidor de copia de seguridad con el dispositivo de APS.  
  
### <a name="manage-network-credentials"></a>Administrar credenciales de red  
  
El acceso de red al directorio de copia de seguridad se basa en la seguridad del uso compartido de archivos de Windows estándar. Antes de realizar una copia de seguridad, debe crear o designar una cuenta de Windows que se utilizará para la autenticación PDW en el directorio de copia de seguridad. Esta cuenta de Windows debe tener permiso para obtener acceso, crear y escribir en el directorio de copia de seguridad.  
  
> [!IMPORTANT]  
> Para reducir los riesgos de seguridad con los datos, se recomienda designar una cuenta de Windows exclusivamente para realizar las operaciones de copia de seguridad y restauración. Permita que esta cuenta tenga permisos para la ubicación de la copia de seguridad y ningún otro lugar más.  
  
Para almacenar el nombre de usuario y la contraseña en PDW, use la [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedimiento almacenado. PDW utiliza el Administrador de credenciales de Windows para almacenar y cifrar los nombres de usuario y contraseñas en el nodo de Control y nodos de proceso. No se realiza una copia de seguridad de las credenciales con el comando BACKUP DATABASE.  
  
Para quitar las credenciales de red de PDW, use la [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md) procedimiento almacenado.  
  
Para obtener una lista de las credenciales de red que se almacenan en SQL Server PDW, use la [sys.dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) vista de administración dinámica.  
  
### <a name="secure-communications"></a>Comunicaciones seguras  
  
Las operaciones en el servidor de carga pueden utilizar una ruta de acceso UNC para extraer datos desde fuera de la red interna de confianza. Un atacante en la red o con capacidad para influir en la resolución de nombres puede interceptar o modificar los datos enviados a PDW. Esto presenta un riesgo de divulgación de información y manipulación. Para ayudar a mitigar el riesgo de alteración:

- Requerir firma en la conexión. 
- En el servidor de carga, establezca la siguiente opción de directiva de grupo de seguridad de seguridad\Directivas Locales\opciones: cliente de red Microsoft: firmar digitalmente las comunicaciones (siempre): habilitado.  
  
## <a name="see-also"></a>Vea también  
[Copias de seguridad y restauración](backup-and-restore-overview.md)  
  
