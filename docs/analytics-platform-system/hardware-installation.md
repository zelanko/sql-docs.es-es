---
title: 'Instalación de hardware: Analytics Platform System | Documentos de Microsoft'
description: Este artículo describe cómo mover, desempaquetar e instalar el hardware de su dispositivo PDW de SQL Server. Este artículo es solo informativo y está diseñada para ayudarle a entender el proceso. Debe desempaquetar, instalarse y comprobar antes de se dedica a la el dispositivo. Participación del cliente es obligatorio para los elementos como los datos del centro de acceso, energía eléctrica y conexiones Ethernet.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 169b38a1228f909a79d7866eba20b85b4a56c30b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="hardware-installation-for-analytics-platform-system-appliance"></a>Instalación de hardware de dispositivo de sistema de la plataforma de análisis
Este artículo describe cómo mover, desempaquetar e instalar el hardware de su dispositivo PDW de SQL Server. Este artículo es solo informativo y está diseñada para ayudarle a entender el proceso. Debe desempaquetar, instalarse y comprobar antes de se dedica a la el dispositivo. Participación del cliente es obligatorio para los elementos como los datos del centro de acceso, energía eléctrica y conexiones Ethernet.  
  
## <a name="BeforeMoving"></a>Antes de mover todos los componentes del muelle de carga  
Realice las tareas siguientes antes de mover, desempaquete o cualquiera de los componentes del dispositivo en bastidor.  
  
|Tarea|Description|  
|--------|---------------|  
|Compruebe que han llegado todos los componentes|Use la lista de materiales (BOM) para comprobar que todos los componentes han llegado y se encuentran en sus paletas en el muelle de recepción para su centro de datos.|  
|Compruebe que el centro de datos cumple todos los requisitos para el dispositivo|Esta tarea de inicio revisando las especificaciones de hardware y proporcionar a los IHV de diagramas de cableado. Los pasos siguientes proporcionan información específica acerca de bastidor requisitos de espacio y la conectividad.|  
|Compruebe que el centro de datos tiene espacio en el bastidor correcto|Compruebe que el centro de datos tiene suficiente espacio para todos los bastidores de dispositivo.<br /><br />Compruebe que el espacio de bastidor está vacío y está listo para recibir los bastidores de dispositivo.|  
|Compruebe que el centro de datos cumple los requisitos de conectividad|Compruebe que el centro de datos cumple los requisitos de cableado en los diagramas de cableado.<br /><br />Compruebe que haya espacio para todos los cables y cables de alimentación después de que se racks con los nodos de dispositivo.|  
|Compruebe que las plantas entre el acoplamiento y los racks cumplen los requisitos de peso|Compruebe que todos los suelo entre las paletas de carga y las perchas puede admitir el peso de los nodos de dispositivo, especialmente en los centros de datos con plantas elevados.<br /><br />Para obtener información sobre el peso de cada componente, póngase en contacto con el IHV.|  
|Proteger el centro de datos en bastidor|Proteger el centro de datos en bastidor en su lugar mediante un equipo adicional según sea necesario para la ubicación de centro de datos, como bandas a terremoto en zonas geográficas propensas a terremotos.|  
|Preparar para obtener ayuda con el transporte de los componentes|Determinar de antemano qué asistencia, equipos y herramientas que necesitará para administrar cada componente de forma segura y sin causar daños.|  
  
## <a name="Moving"></a>Mover los bastidores de muelle de carga en el centro de datos  
Cada palet contiene todos los componentes de bastidor de uno de los dispositivos, incluidos los nodos, cables, cables, etcetera.  
  
Utilice la siguiente lista de comprobación para mover cada bastidor de dispositivo de la paleta en el muelle de carga a su ubicación de bastidor en el centro de datos. Primero mueva el bastidor de control y, a continuación, mueva otros soportes de datos de aplicación.  
  
> [!WARNING]  
> Error al realizar estos pasos exactamente como se describe podría provocar lesiones, daños en el equipo de SQL Server PDW u otros problemas.  
>   
> Nunca ha intentado elevación o mover un nodo de dispositivo u otro componente pesada sin asistencia o dispositivos adecuados. Póngase en contacto con el IHV para obtener información sobre el peso de cada componente para que pueda determinar de antemano qué asistencia, equipos y herramientas que necesitará para administrar cada componente de forma segura y sin causar daños.  
  
|Tarea|Description|  
|--------|---------------|  
|Compruebe que el palet es nivel|Antes de empezar a mover o Desembale el paquete, asegúrese de que esté en nivelado.|  
|Unbolt un nodo de la paleta|A partir de la parte superior de la paleta, unbolt el nodo superior de la paleta.|  
|Mover el nodo a una plataforma de mantenimiento o el carro de la que puede admitir el peso|Utilice las pendientes y las técnicas apropiadas levantar y mover para mover el nodo a una plataforma de mantenimiento o el carro de la que puede admitir el peso.|  
|El nodo de transporte en el centro de datos|Utilizar técnicas de levantar y mover adecuadas para mover el nodo en su posición en el bastidor de centro de datos.|  
|Proteger el nodo en el centro de datos en bastidor|Proteja el nodo en lugar del centro de datos bastidor.|  
|Repita estos pasos para el nodo o el componente siguiente|Repita estos pasos para mover el nodo siguiente u otro componente de dispositivo en el centro de datos.|  
  
## <a name="AfterMoving"></a>Instalar componentes adicionales  
Utilice la siguiente lista de comprobación para instalar los componentes adicionales.  
  
|Tarea|Description||  
|--------|---------------|-|  
|Desempaquetar y conmutadores de red y PDU en bastidor|Utilice los diagramas de bastidor para colocar la PDU y conmutadores de red en la ubicación adecuada en el bastidor.||  
|Conecte los cables de Infiniband y Ethernet según las etiquetas de cable|Consulte el diagrama de cableado. Cada cable tiene una etiqueta en cada extremo que especifica donde es necesario estar conectado.||  
|Conecte todos los cables de alimentación|Consulte el diagrama de cableado.||  
|Activar el sistema de alimentación a las perchas y la PDU|Conecte la fuente de alimentación de los armarios y de la estantería de la PDU. **No encender cualquiera de los demás componentes de dispositivo en este momento.**||  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
