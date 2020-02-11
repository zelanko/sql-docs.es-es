---
title: Adquirir & configurar el servidor de carga
description: En este artículo se describe cómo adquirir y configurar un servidor de carga como un sistema de Windows que no es de aplicación para enviar cargas de datos al almacenamiento de datos paralelos (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ef49bb86c8e16600f2ff1bf2d1c7a92ecc5af964
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401486"
---
# <a name="acquire-and-configure-a-loading-server-for-parallel-data-warehouse"></a>Adquisición y configuración de un servidor de carga para almacenamiento de datos paralelos
En este artículo se describe cómo adquirir y configurar un servidor de carga como un sistema de Windows que no es de aplicación para enviar cargas de datos al almacenamiento de datos paralelos (PDW).  
  
## <a name="Basics"></a>Conceptos básicos  
El servidor de carga:  
  
-   No tiene que ser un único servidor. Puede cargar simultáneamente con varios servidores de carga.  
  
-   Lo proporciona y administra su propio equipo de ti. Es posible que ya tenga un servidor o servidores que se puedan utilizar para cargar datos en PDW.  
  
-   Se encuentra en su propio bastidor que no es de dispositivo y no puede colocarse en el dispositivo de sistema de plataforma de análisis.  
  
-   Está conectado al dispositivo a través de la red InfiniBand del dispositivo o a través de Ethernet. En cuanto a rendimiento, se recomienda usar InfiniBand.  
  
-   Está en su propio dominio del cliente, no en el dominio del dispositivo. No hay ninguna relación de confianza entre el dominio del cliente y el dominio de la aplicación.  
  
## <a name="Step1"></a>Paso 1: determinar los requisitos de capacidad  
El sistema de carga se puede diseñar como uno o más servidores de carga que realizan cargas simultáneas. No es necesario que cada servidor de carga esté dedicado únicamente a la carga, siempre y cuando se controlen los requisitos de rendimiento y almacenamiento de la carga de trabajo.  
  
Los requisitos del sistema para un servidor de carga dependen casi por completo de su propia carga de trabajo. Use la [hoja de cálculo de planeamiento](loading-server-capacity-planning-worksheet.md) de la capacidad del servidor de carga para ayudar a determinar los requisitos de capacidad.  
  
## <a name="Step2"></a>Paso 2: adquirir el Server  
Ahora que comprende mejor sus requisitos de capacidad, puede planear los servidores y los componentes de red que necesitará comprar o aprovisionar. Incorpore la siguiente lista de requisitos en el plan de compra y, a continuación, compre el servidor o aprovisione un servidor existente.  
  
### <a name="R"></a>Requisitos de software  
Sistemas operativos admitidos:  
  
-   Windows Server 2012 o Windows Server 2012 R2. Estos sistemas operativos requieren el adaptador de red FDR.  
  
-   Windows Server 2008 R2. Este sistema operativo requiere el adaptador de red DDR.  
  
El servidor debe usar la configuración regional en-US para poder usar la herramienta de carga de línea de comandos dwloader. dwloader no admite otras configuraciones regionales.  
  
### <a name="networking-requirements-for-windows-server-2012-and-windows-server-2012-r2"></a>Requisitos de red para Windows Server 2012 y Windows Server 2012 R2  
Aunque no es necesario para cargar, InfiniBand es el tipo de conexión recomendado para cargar servidores. Para obtener el mejor rendimiento, use Windows Server 2012 o Windows Server 2012 R2 y el adaptador de red FDR InfiniBand para conectar el servidor de carga a la red InfiniBand.  
  
Para prepararse para una conexión de Windows Server 2012 o Windows Server 2012 R2 InfiniBand:  
  
1.  Planee el servidor lo suficientemente cerca del dispositivo para que pueda conectarlo a los conmutadores InfiniBand de la aplicación. Para obtener más información sobre las tecnologías de Mellanox sobre InfiniBand, consulte las notas del producto sobre la [Introducción a InfiniBand](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf).  
  
2.  Compre un adaptador de red Mellanox ConnectX-3 FDR InfiniBand single o dual port. Se recomienda adquirir el adaptador de red con dos puertos para la tolerancia a errores durante la transmisión de datos. Se requiere un adaptador de red de dos puertos para lograr alta disponibilidad.  
  
3.  Compre dos cables FDR InfiniBand para una tarjeta de puerto doble o un cable de 1 FDR InfiniBand para una tarjeta de puerto único. Los cables FDR InfiniBand conectarán el servidor de carga a la red InfiniBand de la aplicación. La longitud del cable depende de la distancia entre el servidor de carga y los conmutadores de la aplicación InfiniBand, de acuerdo con su entorno.  
  
## <a name="Step3"></a>Paso 3: conectar el servidor a las redes InfiniBand  
Siga estos pasos para conectar el servidor de carga a la red InfiniBand. Si el servidor no está usando la red InfiniBand, omita este paso.  
  
1.  Bastidor el servidor lo suficientemente cerca del dispositivo para que pueda conectarlo a la red InfiniBand de la aplicación.  
  
2.  Instale el adaptador de red InfiniBand Mellanox ConnectX-3 FDR InfiniBand en el servidor de carga.  
  
3.  Use los cables FDR para conectar el adaptador de red InfiniBand a uno de los dos conmutadores InfiniBand en el bastidor del primer dispositivo.  
  
4.  Instale y configure el controlador de Windows adecuado para el adaptador de red InfiniBand.  
  
    -   Los controladores de InfiniBand para Windows son desarrollados por OpenFabrics Alliance, un consorcio del sector de InfiniBand vendors.  Es posible que se haya distribuido el controlador correcto con el adaptador de red InfiniBand. Si no es así, el controlador se puede descargar desde www.openfabrics.org.  
  
5.  Configure las opciones de InfiniBand y DNS para los adaptadores de red. Para obtener instrucciones de configuración, consulte Configuración de [adaptadores de red InfiniBand](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Paso 4: instalar las herramientas de carga  
Las herramientas de cliente están disponibles para su descarga desde el centro de descarga de Microsoft. 

Para instalar dwloader, ejecute la instalación de dwloader desde las herramientas de cliente.
  
Si tiene previsto usar Integration Services para cargar, deberá instalar Integration Services y los adaptadores de destino de Integration Services. Los adaptadores están disponibles en las herramientas de cliente de.

<!-- To install the des[Install Integration Services Destination Adapters](install-integration-services-destination-adapters.md). 
--> 
  
## <a name="Step5"></a>Paso 5: iniciar la carga  
Ahora está listo para empezar a cargar datos. Para más información, consulte:  
  
1.  [Herramienta de carga de línea de comandos de dwloader](dwloader.md)  
  
2.  [Información general sobre la carga](load-overview.md)  
  
## <a name="performance"></a>Rendimiento  
Para obtener el mejor rendimiento de carga en Windows Server 2012 y versiones posteriores, active la inicialización instantánea de archivos para que cuando se sobrescriban los datos, el sistema operativo no sobrescriba los datos existentes con ceros. Si se trata de un riesgo para la seguridad porque todavía existen datos anteriores en los discos, asegúrese de desactivar la inicialización instantánea de archivos.  
  
## <a name="Security"></a>Avisos de seguridad  
Puesto que los datos que se van a cargar no se almacenan en el dispositivo, el equipo de ti es responsable de administrar todos los aspectos de la seguridad de los datos que se van a cargar. Por ejemplo, esto incluye la administración de la seguridad de los datos que se van a cargar, la seguridad del servidor que se usa para almacenar cargas y la seguridad de la infraestructura de red que conecta el servidor de carga al PDW de SQL Server dispositivo.  
  
> [!IMPORTANT]  
> Es especialmente importante proteger cada servidor de carga que usará la herramienta de carga de línea de comandos de dwloader. Cuando dwloader carga datos, primero se autentica con el nodo de control y, después, después de la autenticación correcta, mueve los datos del servidor de carga directamente a los nodos de proceso a través de los canales de datos. La validación de certificados no se lleva a cabo durante el agitador a mano entre cada servidor de carga y cada nodo de proceso. Esto deja los nodos de proceso expuestos a posibles ataques de tipo "Man in the Middle" en cada canal de datos durante la carga. Estos ataques pueden dar lugar a la divulgación de información o datos alterados.  
  
Para reducir los riesgos de seguridad con los datos, se recomienda lo siguiente:  
  
-   Designe una cuenta de Windows que se utilice únicamente con el fin de cargar datos en PDW. Permite que esta cuenta tenga permisos para la ubicación de carga y en ningún otro lugar.  
  
-   Designe un usuario PDW que tenga permisos para cargar datos. En función de los requisitos de seguridad, puede tener un usuario específico por cada base de datos.  
  
-   Las operaciones en el servidor de carga pueden aceptar una ruta de acceso UNC desde la que extraer datos desde fuera de la red interna de confianza. Y un atacante en la red o con la capacidad de influir en la resolución de nombres puede interceptar o modificar los datos que se envían al PDW de SQL Server. Esto presenta un riesgo de manipulación y revelación de información. La manipulación se debe mitigar requiriendo la firma en la conexión. Para ayudar a mitigar este riesgo, establezca la siguiente opción de directiva de grupo en configuración de **Seguridad\directivas locales\Opciones de seguridad** en el servidor de carga: **cliente de red de Microsoft: firmar digitalmente las comunicaciones (siempre): habilitado**  
  
-   Desactive la inicialización instantánea de archivos en Windows Server 2012 y versiones posteriores. Se trata de un equilibrio entre el rendimiento y la seguridad, como se indica en la sección rendimiento. Debe decidir qué es lo mejor según sus requisitos de seguridad.  
  
## <a name="see-also"></a>Consulte también  
[Información general sobre copias de seguridad y restauración](backup-and-restore-overview.md)  
  
