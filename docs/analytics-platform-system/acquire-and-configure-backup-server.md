---
title: Adquirir & configurar el servidor de copia de seguridad
description: En este artículo se describe cómo configurar un sistema de Windows que no es de aplicación como un servidor de copia de seguridad para su uso con las características de copia de seguridad y restauración de Analytics Platform System (APS) y almacenamiento de datos paralelos (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b1d817bae593d4083f3e4873d626e147e58d5c28
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88767164"
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>Adquisición y configuración de un servidor de copia de seguridad para almacenamiento de datos paralelos
En este artículo se describe cómo configurar un sistema de Windows que no es de aplicación como un servidor de copia de seguridad para su uso con las características de copia de seguridad y restauración de Analytics Platform System (APS) y almacenamiento de datos paralelos (PDW).  
  
  
## <a name="backup-server-basics"></a><a name="Basics"></a>Aspectos básicos del servidor de copia de seguridad  
El servidor de copia de seguridad:  
  
-   Lo proporciona y administra su propio equipo de ti.  
  
-   No requiere software ni herramientas específicos de PDW. PDW no instala software en el servidor de copia de seguridad.  
  
-   Se encuentra en su propio bastidor que no es de dispositivo y no puede colocarse en el dispositivo APS.  
  
-   Se puede conectar a la red InfiniBand de la aplicación. Las copias de seguridad se pueden realizar a través de InfiniBand o Ethernet; InfiniBand se recomienda por motivos de rendimiento.  
  
-   Está en su propio dominio del cliente, no en el dominio del dispositivo. No hay ninguna relación de confianza entre el dominio del cliente y el dominio de la aplicación.  
  
-   Hospeda un recurso compartido de archivos de copia de seguridad, que es un recurso compartido de archivos de Windows que usa el protocolo de red de nivel de aplicación de bloque de mensajes del servidor (SMB). Los permisos de recurso compartido de archivos de copia de seguridad proporcionan a un usuario de dominio de Windows (normalmente, un usuario de copia de seguridad dedicado) la capacidad de realizar operaciones de copia de seguridad y restauración en el recurso compartido. Las credenciales de nombre de usuario y contraseña del usuario de dominio de Windows se almacenan en PDW para que PDW pueda realizar operaciones de copia de seguridad y restauración en el recurso compartido de archivos de copia de seguridad.  
  
## <a name="step-1-determine-capacity-requirements"></a><a name="Step1"></a>Paso 1: determinar los requisitos de capacidad  
Los requisitos del sistema para el servidor de copia de seguridad dependen casi por completo de su propia carga de trabajo. Antes de adquirir o aprovisionar un servidor de copia de seguridad, debe averiguar los requisitos de capacidad. No es necesario que el servidor de copia de seguridad esté dedicado únicamente a las copias de seguridad, siempre y cuando se controlen los requisitos de rendimiento y almacenamiento de la carga de trabajo. También puede tener varios servidores de copia de seguridad para hacer una copia de seguridad y restaurar cada base de datos en uno de varios servidores.  
  
Use la [hoja de cálculo de planeamiento](backup-capacity-planning-worksheet.md) de la capacidad del servidor de copia de seguridad para determinar los requisitos de capacidad.  
  
## <a name="step-2-acquire-the-backup-server"></a><a name="Step2"></a>Paso 2: adquisición del servidor de copia de seguridad  
Ahora que comprende mejor sus requisitos de capacidad, puede planear los servidores y los componentes de red que necesitará comprar o aprovisionar. Incorpore la siguiente lista de requisitos en el plan de compra y, a continuación, compre el servidor o aprovisione un servidor existente.  
  
### <a name="software-requirements"></a>Requisitos de software  
Cualquier servidor de archivos que use el protocolo de uso compartido de archivos de Windows (SMB).  
  
Se recomienda Windows Server 2012 o posterior para:  
  
-   Obtenga la ventaja de rendimiento de la asignación previa de archivos a través de SMB.  
  
-   Use la inicialización instantánea de archivos (IFI) para las operaciones de copia de seguridad. El equipo de ti administra esta configuración en el servidor de copia de seguridad. El Configuration Manager PDW (dwconfig.exe) no establece ni controla IFI en el servidor de copia de seguridad. Las versiones anteriores de Windows no tienen IFI, pero todavía se pueden usar como servidores de copia de seguridad.  
  
### <a name="networking-requirements"></a>Requisitos de red  
Aunque no es necesario, InfiniBand es el tipo de conexión recomendado para los servidores de copia de seguridad. Para preparar la conexión del servidor de carga a la red InfiniBand Network:  
  
1.  Planee el servidor lo suficientemente cerca del dispositivo para que pueda conectarlo a los conmutadores InfiniBand de la aplicación. Para obtener más información sobre las tecnologías de Mellanox sobre InfiniBand, consulte las notas del producto sobre la [Introducción a InfiniBand](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf).  
  
2.  Compre un adaptador de red Mellanox ConnectX-3 FDR InfiniBand single o dual port. Se recomienda adquirir el adaptador de red con dos puertos para la tolerancia a errores durante la transmisión de datos. Se requiere un adaptador de red de dos puertos para lograr alta disponibilidad.  
  
3.  Compre dos cables FDR InfiniBand para una tarjeta de puerto doble o un cable de 1 FDR InfiniBand para una tarjeta de puerto único. Los cables FDR InfiniBand conectarán el servidor de carga a la red InfiniBand de la aplicación. La longitud del cable depende de la distancia entre el servidor de carga y los conmutadores de la aplicación InfiniBand, de acuerdo con su entorno.  
  
## <a name="step-3-connect-the-server-to-the-infiniband-networks"></a><a name="Step3"></a>Paso 3: conectar el servidor a las redes InfiniBand  
Siga estos pasos para conectar el servidor de carga a la red InfiniBand. Si el servidor no está usando la red InfiniBand, omita este paso.  
  
1.  Bastidor el servidor lo suficientemente cerca del dispositivo para que pueda conectarlo a la red InfiniBand de la aplicación.  
  
2.  Instale el adaptador de red InfiniBand Mellanox ConnectX-3 FDR InfiniBand en el servidor de carga.  
  
3.  Use los cables FDR para conectar el adaptador de red InfiniBand a uno de los dos conmutadores InfiniBand en el bastidor del primer dispositivo.  
  
4.  Instale y configure el controlador de Windows adecuado para el adaptador de red InfiniBand.  
  
    -   Los controladores de InfiniBand para Windows son desarrollados por OpenFabrics Alliance, un consorcio del sector de InfiniBand vendors.  Es posible que se haya distribuido el controlador correcto con el adaptador de red InfiniBand. Si no es así, el controlador se puede descargar desde www.openfabrics.org.  
  
5.  Configure las opciones de InfiniBand y DNS para los adaptadores de red. Para obtener instrucciones de configuración, consulte Configuración de [adaptadores de red InfiniBand](configure-infiniband-network-adapters.md).  
  
## <a name="step-4-configure-the-backup-file-share"></a><a name="Step4"></a>Paso 4: configurar el recurso compartido de archivos de copia de seguridad  
PDW tendrá acceso al servidor de copia de seguridad a través de un recurso compartido de archivos UNC. Para configurar el recurso compartido de archivos:  
  
1.  Cree una carpeta en el servidor de copia de seguridad para almacenar las copias de seguridad.  
  
2.  Cree un recurso compartido de archivos, denominado recurso compartido de copia de seguridad, para la carpeta de copia de seguridad.  
  
3.  Designe o cree una cuenta de dominio de Windows en el dominio del cliente que desee usar con el fin de realizar copias de seguridad y restauraciones. Por motivos de seguridad, es mejor utilizar una cuenta dedicada como usuario de copia de seguridad.  
  
4.  Agregue permisos al recurso compartido de copia de seguridad para que solo las cuentas de confianza y una cuenta de copia de seguridad de dominio puedan tener acceso, leer y escribir en la ubicación del recurso compartido.  
  
5.  Agregue las credenciales de la cuenta de dominio de copia de seguridad a PDW.  
  
    Por ejemplo:  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    Para obtener más información, vea estos procedimientos almacenados:  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="step-5-start-backing-up-your-data"></a><a name="Step5"></a>Paso 5: Inicio de la copia de seguridad de los datos  
Ahora está listo para empezar a realizar copias de seguridad de los datos en el servidor de copia de seguridad.  
  
Para realizar una copia de seguridad de los datos, utilice un cliente de consultas para conectarse a PDW de SQL Server y, a continuación, enviar los comandos BACKUP DATABASE o RESTOre DATABASE. Utilice la cláusula DISK = para especificar el servidor de copia de seguridad y la ubicación de copia de seguridad.  
  
> [!IMPORTANT]  
> Recuerde usar la dirección IP InfiniBand del servidor de copia de seguridad. De lo contrario, los datos se copiarán a través de Ethernet en lugar de InfiniBand.  
  
Por ejemplo:  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
Para más información, consulte: 
  
-   [BACKUP DATABASE](../t-sql/statements/backup-transact-sql.md?view=aps-pdw-2016)   
  
-   [RESTAURAR BASE DE DATOS](../t-sql/statements/restore-statements-transact-sql.md?view=aps-pdw-2016)  
  
## <a name="security-notices"></a><a name="Security"></a>Avisos de seguridad  
El servidor de copia de seguridad no está unido al dominio privado del dispositivo. Está en su propia red y no hay ninguna relación de confianza entre su dominio y el dominio de la aplicación privada.  
  
Puesto que las copias de seguridad de PDW no se almacenan en el dispositivo, el equipo de ti es responsable de administrar todos los aspectos de la seguridad de copia de seguridad. Por ejemplo, esto incluye la administración de la seguridad de los datos de copia de seguridad, la seguridad del servidor usada para almacenar copias de seguridad y la seguridad de la infraestructura de red que conecta el servidor de copia de seguridad al dispositivo APS.  
  
### <a name="manage-network-credentials"></a>Administrar credenciales de red  
  
El acceso de red al directorio de copia de seguridad se basa en la seguridad del uso compartido de archivos de Windows estándar. Antes de realizar una copia de seguridad, debe crear o designar una cuenta de Windows que se usará para autenticar PDW en el directorio de copia de seguridad. Esta cuenta de Windows debe tener permiso para obtener acceso, crear y escribir en el directorio de copia de seguridad.  
  
> [!IMPORTANT]  
> Para reducir los riesgos de seguridad con los datos, se recomienda designar una cuenta de Windows exclusivamente para realizar las operaciones de copia de seguridad y restauración. Permita que esta cuenta tenga permisos para la ubicación de la copia de seguridad y ningún otro lugar más.  
  
Para almacenar el nombre de usuario y la contraseña en PDW, use el [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) procedimiento almacenado. PDW utiliza el administrador de credenciales de Windows para almacenar y cifrar nombres de usuario y contraseñas en el nodo de control y en los nodos de proceso. No se realiza una copia de seguridad de las credenciales con el comando BACKUP DATABASE.  
  
Para quitar las credenciales de red de PDW, use el [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md) procedimiento almacenado.  
  
Para enumerar todas las credenciales de red almacenadas en PDW de SQL Server, use la vista de administración dinámica [Sys. dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) .  
  
### <a name="secure-communications"></a>Comunicaciones seguras  
  
Las operaciones en el servidor de carga pueden usar una ruta de acceso UNC para extraer datos de fuera de la red interna de confianza. Un atacante de la red o con la capacidad de influir en la resolución de nombres puede interceptar o modificar los datos que se envían al PDW. Esto presenta un riesgo de manipulación y revelación de información. Para ayudar a mitigar el riesgo de alteración:

- Requerir la firma en la conexión. 
- En el servidor de carga, establezca la siguiente opción de directiva de grupo en configuración de Seguridad\directivas Locales\opciones de seguridad: cliente de red de Microsoft: firmar digitalmente las comunicaciones (siempre): habilitado.  
  
## <a name="see-also"></a>Consulte también  
[Copia de seguridad y restauración](backup-and-restore-overview.md)  
