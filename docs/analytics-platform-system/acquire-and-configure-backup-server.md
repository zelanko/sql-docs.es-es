---
title: Adquirir y configurar un servidor de copia de seguridad - almacenamiento de datos paralelos | Microsoft Docs
description: En este artículo se describe cómo configurar un sistema de Windows que no sea de dispositivo como un servidor de copia de seguridad para su uso con las características de copia de seguridad y restauración en Analytics Platform System (APS) y almacenamiento de datos paralelos (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f79cb13658328927cab81bbf8d559066c5a4d5cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961646"
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>Adquirir y configurar un servidor de copia de seguridad para el almacenamiento de datos paralelos
En este artículo se describe cómo configurar un sistema de Windows que no sea de dispositivo como un servidor de copia de seguridad para su uso con las características de copia de seguridad y restauración en Analytics Platform System (APS) y almacenamiento de datos paralelos (PDW).  
  
  
## <a name="Basics"></a>Conceptos básicos de copia de seguridad de servidor  
El servidor de copia de seguridad:  
  
-   Se proporciona y administra su propio equipo de TI.  
  
-   No requiere herramientas ni software específico de PDW. PDW no instale el software en el servidor de copia de seguridad.  
  
-   Se encuentra en su propio bastidor que no sea de dispositivo y no se pueden colocar dentro del dispositivo APS.  
  
-   Puede estar conectado a la red InfiniBand de dispositivo. Se pueden realizar copias de seguridad a través de InfiniBand, Ethernet; InfiniBand es recomendable por razones de rendimiento.  
  
-   Está en su propio dominio de cliente, no el dominio del equipo. No hay ninguna relación de confianza entre el dominio del cliente y el dominio del equipo.  
  
-   Hospeda un recurso compartido de archivos de copia de seguridad, que es un recurso compartido de archivos de Windows que utiliza el protocolo de red de nivel de aplicación de bloque de mensajes del servidor (SMB). Los permisos de recurso compartido de archivos de copia de seguridad conceder a un usuario de dominio de Windows (normalmente es un usuario de copia de seguridad dedicado) la capacidad de realizar la copia de seguridad y restaurar las operaciones en el recurso compartido. Las credenciales de usuario y la contraseña del usuario de dominio de Windows se almacenan en PDW para que pueda realizar copia de seguridad y restaurar las operaciones en el recurso compartido de archivos de copia de seguridad PDW.  
  
## <a name="Step1"></a>Paso 1: Determinar los requisitos de capacidad  
Los requisitos del sistema para el servidor de copia de seguridad dependen casi por completo su propia carga de trabajo. Antes de comprar o aprovisionar un servidor de copia de seguridad deberá averiguar los requisitos de capacidad. El servidor de copia de seguridad no tiene que ser dedicado exclusivamente a las copias de seguridad, siempre que va a controlar los requisitos de almacenamiento y rendimiento de la carga de trabajo. También puede tener varios servidores de copia de seguridad con el fin de copia de seguridad y restaurar cada base de datos a uno de varios servidores.  
  
Use la [hoja de cálculo de planeación de capacidad de servidor de copia de seguridad](backup-capacity-planning-worksheet.md) para ayudar a determinar los requisitos de capacidad.  
  
## <a name="Step2"></a>Paso 2: Adquirir el servidor de copia de seguridad  
Ahora que comprende mejor sus requisitos de capacidad, puede planear los servidores y los componentes de red que necesitará adquirir o aprovisionar. Incorporar la siguiente lista de los requisitos de su plan de compra y el servidor de la compra o aprovisionar un servidor existente.  
  
### <a name="software-requirements"></a>Requisitos de software  
Cualquier servidor de archivos que utiliza el protocolo de uso compartido de archivos de Windows (SMB).  
  
Se recomienda Windows Server 2012 o más allá para:  
  
-   Obtenga la ventaja de rendimiento de la asignación previa de archivo a través de SMB.  
  
-   Use la inicialización instantánea de archivos (IFI) para las operaciones de copia de seguridad. El equipo de TI administra esta configuración en el servidor de copia de seguridad. El Administrador de configuración de PDW (dwconfig.exe) no establezca o controlar IFI en el servidor de copia de seguridad. Las versiones anteriores de Windows no tiene IFI, pero pueden usarse como servidores de copia de seguridad.  
  
### <a name="networking-requirements"></a>Requisitos de red  
Aunque no es necesario, InfiniBand es el tipo de conexión recomendado para servidores de copia de seguridad. Para prepararse para conectar el servidor de carga a la red InfiniBand de dispositivo:  
  
1.  Plan para el servidor en bastidor cerrar lo suficiente como para el dispositivo de manera que puede conectarse al dispositivo cambia de InfiniBand. Para obtener más información de las tecnologías de Mellanox de InfiniBand, vea las notas del producto, [Introducción a InfiniBand](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf).  
  
2.  Adquiera un adaptador de red Mellanox ConnectX-3 FDR InfiniBand puerto único o doble. Se recomienda adquirir el adaptador de red con dos puertos para tolerancia a errores durante la transmisión de datos. Falta un adaptador de red de dos puertos para alta disponibilidad.  
  
3.  Adquirir 2 cables FDR InfiniBand para una tarjeta de puerto dual o 1 cable FDR InfiniBand para una tarjeta de puerto único. Los cables de InfiniBand FDR conectarán el servidor de carga a la red InfiniBand de dispositivo. La longitud del cable depende de la distancia entre el servidor de carga y los conmutadores de InfiniBand del equipo, según su entorno.  
  
## <a name="Step3"></a>Paso 3: Conecte el servidor a las redes InfiniBand  
Siga estos pasos para conectarse al servidor de carga a la red InfiniBand. Si el servidor no está usando la red InfiniBand, omita este paso.  
  
1.  Bastidor del servidor se cierre suficiente para el dispositivo para que se puede conectar a la red InfiniBand de dispositivo.  
  
2.  Instalar al adaptador de red InfiniBand FDR de InfiniBand Mellanox ConnectX-3 en el servidor de carga.  
  
3.  Use los cables FDR para conectar el adaptador de red InfiniBand a uno de los dos conmutadores de InfiniBand en el primer bastidor del dispositivo.  
  
4.  Instale y configure el controlador de Windows adecuado para el adaptador de red InfiniBand.  
  
    -   Controladores de InfiniBand para Windows se desarrollan por OpenFabrics Alliance, un consorcio del sector de los proveedores de InfiniBand.  Es posible que el controlador correcto se han distribuido con el adaptador de red InfiniBand. Si no es así, el controlador puede descargarse desde www.openfabrics.org.  
  
5.  Configurar las opciones de InfiniBand y DNS para los adaptadores de red. Para obtener instrucciones de configuración, consulte [configurar adaptadores de red de InfiniBand](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Paso 4: Configure el recurso compartido de archivos de copia de seguridad  
PDW obtendrá acceso al servidor de copia de seguridad a través de un recurso compartido UNC. Para configurar el recurso compartido de archivos:  
  
1.  Cree una carpeta en el servidor de copia de seguridad para almacenar las copias de seguridad.  
  
2.  Crear un recurso compartido de archivos, llama a un recurso compartido de copia de seguridad, para la carpeta de copia de seguridad.  
  
3.  Designe o cree una cuenta de dominio de Windows en el dominio de cliente que desea usar para los fines de realización de copias de seguridad y restauraciones. Por motivos de seguridad, es mejor usar una cuenta dedicada, como el usuario de copia de seguridad.  
  
4.  Agregar permisos para la copia de seguridad compartan para que puedan acceder solo cuentas de confianza y una cuenta de copia de seguridad de dominio, leer y escriben en la ubicación del recurso compartido.  
  
5.  Agregue las credenciales de cuenta de dominio de reserva a PDW.  
  
    Por ejemplo:  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    Para obtener más información, vea estos procedimientos almacenados:  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>Paso 5: Iniciar la copia de seguridad de los datos  
Ahora está listo para comenzar la copia de seguridad de datos al servidor de copia de seguridad.  
  
Los comandos para datos de copia de seguridad, use un cliente de consulta para conectarse a SQL Server PDW y, a continuación, enviar copia de seguridad o restauración de base de datos. Usar el disco = cláusula para especificar la ubicación de copia de seguridad y el servidor de copia de seguridad.  
  
> [!IMPORTANT]  
> Recuerde que debe usar la dirección de InfiniBand IP del servidor de copia de seguridad. En caso contrario, se copiarán los datos a través de Ethernet en lugar de InfiniBand.  
  
Por ejemplo:  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
Para obtener más información, vea: 
  
-   [BASE DE DATOS DE COPIA DE SEGURIDAD](../t-sql/statements/backup-database-parallel-data-warehouse.md)   
  
-   [RESTORE DATABASE](../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
## <a name="Security"></a>Avisos de seguridad  
El servidor de copia de seguridad no está unido al dominio privado para el dispositivo. Se encuentra en su propia red y no hay ninguna relación de confianza entre su propio dominio y privadas del dispositivo.  
  
Puesto que no se almacenan las copias de seguridad PDW del dispositivo, su equipo de TI es responsable de administrar todos los aspectos de la seguridad de copia de seguridad. Por ejemplo, esto incluye la administración de la seguridad de los datos de copia de seguridad, la seguridad del servidor utilizado para almacenar las copias de seguridad y la seguridad de la infraestructura de red que conecta el servidor de copia de seguridad para el dispositivo APS.  
  
### <a name="manage-network-credentials"></a>Administrar credenciales de red  
  
El acceso de red al directorio de copia de seguridad se basa en la seguridad del uso compartido de archivos de Windows estándar. Antes de realizar una copia de seguridad, debe crear o designar una cuenta de Windows que se usará para la autenticación en el directorio de copia de seguridad de PDW. Esta cuenta de Windows debe tener permiso para obtener acceso, crear y escribir en el directorio de copia de seguridad.  
  
> [!IMPORTANT]  
> Para reducir los riesgos de seguridad con los datos, se recomienda designar una cuenta de Windows exclusivamente para realizar las operaciones de copia de seguridad y restauración. Permita que esta cuenta tenga permisos para la ubicación de la copia de seguridad y ningún otro lugar más.  
  
Para almacenar el nombre de usuario y la contraseña en PDW, use el [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedimiento almacenado. PDW usa Administrador de credenciales de Windows para almacenar y cifrar los nombres de usuario y contraseñas en el nodo de Control y los nodos de proceso. No se realiza una copia de seguridad de las credenciales con el comando BACKUP DATABASE.  
  
Para quitar las credenciales de red de PDW, use el [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md) procedimiento almacenado.  
  
Para obtener una lista de las credenciales de red almacenadas en PDW de SQL Server, utilice el [sys.dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) vista de administración dinámica.  
  
### <a name="secure-communications"></a>Comunicaciones seguras  
  
Operaciones en el servidor de carga pueden usar una ruta de acceso UNC para extraer datos desde fuera de la red interna de confianza. Un atacante en la red o con la capacidad de influir en la resolución de nombres puede interceptar o modificar los datos enviados a PDW. Esto presenta un riesgo de divulgación de manipulación y la información. Para ayudar a mitigar el riesgo de alteración:

- Requerir firma en la conexión. 
- En el servidor de carga, establezca la siguiente opción de directiva de grupo de seguridad Settings\Local Policies\Security opciones:  Cliente de red Microsoft: Firmar digitalmente las comunicaciones (siempre): habilitada.  
  
## <a name="see-also"></a>Vea también  
[Copias de seguridad y restauración](backup-and-restore-overview.md)  
  
