---
title: Adquirir y configurar un servidor de carga (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Adquirir y configurar un servidor de carga como un sistema de Windows no sea de dispositivo para el envío de cargas de datos para almacenamiento de datos paralelos de SQL Server."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: a434b174-a818-4f73-b218-264619bab664
caps.latest.revision: "19"
ms.openlocfilehash: 05747889f905e1f827a87cc0ad53ace62a911922
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="acquire-and-configure-a-loading-server"></a>Adquirir y configurar un servidor de carga
En este tema se describe cómo adquirir y configurar un servidor de carga como un sistema de Windows no sea de dispositivo para el envío de cargas de datos al almacenamiento de datos paralelo de SQL Server (PDW).  
  
## <a name="Basics"></a>Conceptos básicos  
El servidor de carga:  
  
-   No tiene que ser un único servidor. Puede cargar simultáneamente con varios servidores de carga.  
  
-   Se proporciona y administra su propio equipo de TI. Puede que ya tenga un servidor o servidores que se pueden usar para cargar datos en PDW.  
  
-   Se encuentra en su propio bastidor no sea de dispositivo y no se puede colocar en el dispositivo de sistema de la plataforma de análisis.  
  
-   Se conecta al dispositivo a través de la red InfiniBand de dispositivo o a través de Ethernet. Para obtener un rendimiento, se recomienda usar InfiniBand.  
  
-   Está en su propio dominio de cliente, no el dominio del equipo. No hay ninguna relación de confianza entre el dominio del cliente y el dominio del equipo.  
  
## <a name="Step1"></a>Paso 1: Determinar los requisitos de capacidad  
El sistema de carga puede diseñarse como uno o más servidores de carga que realizan cargas simultáneas. Cada servidor de carga no tiene a estar dedicados solo para cargar, siempre que va a controlar los requisitos de almacenamiento y el rendimiento de la carga de trabajo.  
  
Los requisitos del sistema para un servidor de carga dependen casi por completo su propia carga de trabajo. Use la [hoja de planeamiento de capacidad de carga de servidor](loading-server-capacity-planning-worksheet.md) para ayudar a determinar los requisitos de capacidad.  
  
## <a name="Step2"></a>Paso 2: Adquirir el servidor  
Ahora que entender mejor los requisitos de capacidad, puede planear los servidores y los componentes de red que necesitará para adquirir o aprovisionar. Incorporar la siguiente lista de requisitos en el plan de compra y, a continuación, adquirir el servidor o aprovisionar un servidor existente.  
  
### <a name="R"></a>Requisitos de software  
Sistemas operativos admitidos:  
  
-   Windows Server 2012 o Windows Server 2012 R2. Estos sistemas operativos requieren el adaptador de red FDR.  
  
-   Windows Server 2008 R2. Este sistema operativo requiere que el adaptador de red DDR.  
  
El servidor debe usar la configuración regional EN-US para usar la herramienta de línea de comandos de carga de dwloader. dwloader no es compatible con otras configuraciones regionales.  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Requisitos de red para Windows Server 2012 y Windows Server 2012 R2  
Aunque no es necesario para cargar, InfiniBand es el tipo de conexión recomendado para la carga de servidores. Para obtener el mejor rendimiento, utilice Windows Server 2012 o Windows Server 2012 R2 y el adaptador de red InfiniBand FDR para conectarse al servidor de carga a la red InfiniBand de dispositivo.  
  
Para prepararse para una conexión de Windows Server 2012 o Windows Server 2012 R2 InfiniBand:  
  
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
  
5.  Configurar las opciones de InfiniBand y DNS para los adaptadores de red. Para obtener instrucciones de configuración, consulte [adaptadores de red InfiniBand configurar](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Paso 4: Instalar las herramientas de carga  
Las herramientas de cliente están disponibles para su descarga desde Microsoft Download Center. 

Para instalar dwloader, ejecute la instalación de dwloader desde las herramientas de cliente.
  
Si planea utilizar Integration Services para la carga, debe instalar los servicios de integración y los adaptadores de destino de Integration Services. Los adaptadores están disponibles en las herramientas de cliente.

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>Paso 5: Iniciar la carga  
Ahora está listo para iniciar la carga de datos. Para obtener más información, vea:  
  
1.  [Herramienta de carga de la línea de comandos de dwloader](dwloader.md)  
  
2.  [Información general de carga](load-overview.md)  
  
## <a name="performance"></a>Rendimiento  
Para obtener mejor rendimiento en Windows Server 2012 y más allá de carga, active la inicialización instantánea de archivos para que cuando se sobrescriben los datos del sistema operativo no sobrescribe los datos existentes con ceros. Si se trata de un riesgo de seguridad porque los datos anteriores siguen existiendo en los discos, asegúrese de desactivar la inicialización instantánea de archivos.  
  
## <a name="Security"></a>Avisos de seguridad  
Puesto que los datos que se va a cargar no se almacenan en el dispositivo, su equipo de TI es responsable de administrar todos los aspectos de la seguridad de los datos cargar. Por ejemplo, esto incluye la administración de la seguridad de los datos que se va a cargar, la seguridad del servidor utilizado para almacenar las cargas y la seguridad de la infraestructura de red que conecta el servidor de carga con el dispositivo PDW de SQL Server.  
  
> [!IMPORTANT]  
> Es especialmente importante proteger cada servidor de carga que utilizará la herramienta de línea de comandos de carga de dwloader. Cuando dwloader carga los datos, primero se autentica con el nodo de Control y, a continuación, tras la autenticación correcta mueve los datos desde el servidor de carga directamente a los nodos de proceso a través de canales de datos. Validación de certificados no se produce durante la mano apretón entre cada servidor de carga y cada nodo de ejecución. Esto deja los nodos de cálculo expuestos a posibles ataques de man-in-the-middle en cada canal de datos mientras se carga. Estos ataques podrían producir datos alterados o divulgación de información.  
  
Para reducir los riesgos de seguridad con los datos, se recomienda lo siguiente:  
  
-   Designar una cuenta de Windows que se utiliza únicamente con el fin de cargar datos en PDW. Permitir que esta cuenta tenga permisos para la ubicación de carga y ningún otro lugar.  
  
-   Designar un usuario PDW que tenga permisos para cargar los datos. Dependiendo de los requisitos de seguridad, podría tener un usuario específico por base de datos.  
  
-   Operaciones en el servidor de carga pueden aceptar una ruta de acceso UNC desde el que extraer datos desde fuera de la red interna de confianza. Y un atacante en la red o con capacidad para influir en la resolución de nombres puede interceptar o modificar los datos enviados a SQL Server PDW. Esto presenta un riesgo de divulgación de información y manipulación. Manipulación debe reducirse al requerir firma en la conexión. Para mitigar este riesgo, establecer la siguiente opción de directiva de grupo en **seguridad seguridad\Directivas Locales\opciones** en el servidor de carga: **cliente de red Microsoft: firmar digitalmente las comunicaciones (siempre): Habilitado**  
  
-   Desactivar la inicialización instantánea de archivos en Windows Server 2012 y posteriores. Se trata de un equilibrio entre rendimiento y seguridad, como se indica en la sección de rendimiento. Debe decidir lo que es mejor según sus requisitos de seguridad.  
  
## <a name="see-also"></a>Vea también  
[Información general de copia de seguridad y restauración](backup-and-restore-overview.md)  
  
