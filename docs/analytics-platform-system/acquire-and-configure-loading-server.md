---
title: Adquirir y configurar un servidor de carga - almacenamiento de datos paralelos | Microsoft Docs
description: En este artículo se describe cómo adquirir y configurar un servidor de carga como un sistema de Windows que no sea de dispositivo para enviar cargas de datos con el almacén de datos paralelos (PDW).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: da404aa881f3ff7af26a681751aae12a45f2628f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63231104"
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>Adquirir y configurar un servidor de carga para el almacenamiento de datos paralelos
En este artículo se describe cómo adquirir y configurar un servidor de carga como un sistema de Windows que no sea de dispositivo para enviar cargas de datos con el almacén de datos paralelos (PDW).  
  
## <a name="Basics"></a>Conceptos básicos  
El servidor de carga:  
  
-   No tiene que ser un solo servidor. Se pueden cargar simultáneamente con varios servidores de carga.  
  
-   Se proporciona y administra su propio equipo de TI. Puede que ya tenga uno o varios servidores que se pueden usar para cargar datos en PDW.  
  
-   Se encuentra en su propio bastidor que no sea de dispositivo y no se pueden colocar dentro de la aplicación Analytics Platform System.  
  
-   Se conecta al dispositivo a través de la red InfiniBand de dispositivo o a través de Ethernet. Para obtener un rendimiento, se recomienda usar InfiniBand.  
  
-   Está en su propio dominio de cliente, no el dominio del equipo. No hay ninguna relación de confianza entre el dominio del cliente y el dominio del equipo.  
  
## <a name="Step1"></a>Paso 1: Determinar los requisitos de capacidad  
El sistema de carga puede diseñarse como uno o más servidores de carga que realizan cargas simultáneas. Cada servidor de carga no es necesario que se emplea en exclusiva para cargar, siempre que va a controlar los requisitos de almacenamiento y rendimiento de la carga de trabajo.  
  
Los requisitos del sistema para un servidor de carga dependen casi por completo su propia carga de trabajo. Use la [hoja de planeamiento de capacidad de cargar Server](loading-server-capacity-planning-worksheet.md) para ayudar a determinar los requisitos de capacidad.  
  
## <a name="Step2"></a>Paso 2: Adquirir el servidor  
Ahora que comprende mejor sus requisitos de capacidad, puede planear los servidores y los componentes de red que necesitará adquirir o aprovisionar. Incorporar la siguiente lista de los requisitos de su plan de compra y el servidor de la compra o aprovisionar un servidor existente.  
  
### <a name="R"></a>Requisitos de software  
Sistemas operativos compatibles:  
  
-   Windows Server 2012 o Windows Server 2012 R2. Estos sistemas operativos requieren el adaptador de red FDR.  
  
-   Windows Server 2008 R2. Este sistema operativo requiere que el adaptador de red DDR.  
  
El servidor debe usar la configuración regional EN-US para poder usar la herramienta de línea de comandos de carga dwloader. dwloader no es compatible con otras configuraciones regionales.  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Requisitos de red para Windows Server 2012 y Windows Server 2012 R2  
Aunque no es necesario para la carga, InfiniBand es el tipo de conexión recomendado para cargar los servidores. Para obtener el mejor rendimiento, use Windows Server 2012 o Windows Server 2012 R2 y el adaptador de red InfiniBand FDR para conectarse al servidor de carga a la red InfiniBand de dispositivo.  
  
Para preparar una conexión de Windows Server 2012 o Windows Server 2012 R2 InfiniBand:  
  
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
  
5.  Configurar las opciones de InfiniBand y DNS para los adaptadores de red. Para obtener instrucciones de configuración, consulte [adaptadores de red InfiniBand configurar](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Paso 4: Instalar las herramientas de carga  
Las herramientas de cliente están disponibles para su descarga desde Microsoft Download Center. 

Para instalar dwloader, ejecute la instalación de dwloader desde las herramientas de cliente.
  
Si tiene previsto usar Integration Services para cargar, deberá instalar Integration Services y los adaptadores de destino de Integration Services. Los adaptadores están disponibles en las herramientas de cliente.

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>Paso 5: Iniciar carga  
Ahora está listo para iniciar la carga de datos. Para obtener más información, vea:  
  
1.  [Herramienta de carga de la línea de comandos de dwloader](dwloader.md)  
  
2.  [Información general de carga](load-overview.md)  
  
## <a name="performance"></a>Rendimiento  
Para obtener mejor rendimiento en Windows Server 2012 y versiones posteriores de carga, active la inicialización instantánea de archivo para que cuando se sobrescriben los datos del sistema operativo no sobrescribirá los datos existentes con ceros. Si esto supone un riesgo de seguridad porque los datos anteriores todavía existen en los discos, asegúrese de desactivar la inicialización instantánea de archivos.  
  
## <a name="Security"></a>Avisos de seguridad  
Dado que no se almacenan los datos que se va a cargar en el dispositivo, su equipo de TI es responsable de administrar todos los aspectos de la seguridad de los datos cargar. Por ejemplo, esto incluye la administración de la seguridad de los datos que se va a cargar, la seguridad del servidor usada para almacenar cargas y la seguridad de la infraestructura de red que conecta el servidor de carga con el dispositivo PDW de SQL Server.  
  
> [!IMPORTANT]  
> Es especialmente importante proteger cada servidor de carga que se usará la herramienta de línea de comandos de carga dwloader. Cuando dwloader carga los datos, primero se autentica con el nodo de Control y, a continuación, tras una autenticación correcta mueve los datos desde el servidor carga directamente a los nodos de proceso a través de canales de datos. Validación de certificados no se produce durante la vibración mano entre cada servidor de carga y cada nodo de proceso. Esto deja los nodos de proceso expuestos a posibles ataques man-in-the-middle en cada canal de datos mientras se carga. Estos ataques podrían alterados datos o la divulgación de información.  
  
Para reducir los riesgos de seguridad con los datos, se recomienda lo siguiente:  
  
-   Designar una cuenta de Windows que se usa exclusivamente para cargar datos en PDW. Permita que esta cuenta tiene permisos para la ubicación de carga y ningún otro lugar.  
  
-   Designar un usuario PDW que tenga permisos para cargar los datos. Dependiendo de los requisitos de seguridad, podría tener un usuario específico por base de datos.  
  
-   Operaciones en el servidor de carga pueden aceptar una ruta de acceso UNC desde la que extraer datos desde fuera de la red interna de confianza. Y un atacante en la red o con la capacidad de influir en la resolución de nombres puede interceptar o modificar los datos enviados a SQL Server PDW. Esto presenta un riesgo de divulgación de manipulación y la información. Manipulación debe reducirse al requerir firma en la conexión. Para ayudar a mitigar este riesgo, establezca la siguiente opción de directiva de grupo **seguridad Settings\Local Policies\Security opciones** en el servidor de carga:  **Cliente de red Microsoft: Firmar digitalmente las comunicaciones (siempre): Habilitado**  
  
-   Desactivar la inicialización instantánea de archivos en Windows Server 2012 y versiones posteriores. Se trata de un equilibrio entre rendimiento y seguridad, como se indicó en la sección rendimiento. Debe decidir lo que es mejor según sus requisitos de seguridad.  
  
## <a name="see-also"></a>Vea también  
[Información general de copia de seguridad y restauración](backup-and-restore-overview.md)  
  
