---
title: 'Instalación de hardware: Analytics Platform System | Microsoft Docs'
description: En este artículo se describe cómo mover, desempaquetar e instalar el hardware de su dispositivo PDW de SQL Server. En este artículo es solo informativo y está pensado para ayudarle a entender el proceso. El dispositivo se debe desempaquetar, instalado y comprobar antes de que se traspase a usted. Participación del cliente es obligatorio para los elementos como los datos del centro de acceso, suministro eléctrico y conexiones Ethernet.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 169b38a1228f909a79d7866eba20b85b4a56c30b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63157317"
---
# <a name="hardware-installation-for-analytics-platform-system-appliance"></a>Instalación del hardware de dispositivo de Analytics Platform System
En este artículo se describe cómo mover, desempaquetar e instalar el hardware de su dispositivo PDW de SQL Server. En este artículo es solo informativo y está pensado para ayudarle a entender el proceso. El dispositivo se debe desempaquetar, instalado y comprobar antes de que se traspase a usted. Participación del cliente es obligatorio para los elementos como los datos del centro de acceso, suministro eléctrico y conexiones Ethernet.  
  
## <a name="BeforeMoving"></a>Antes de mover todos los componentes del muelle de carga  
Realice las tareas siguientes antes de mover, desempaquetar o cualquiera de los componentes del dispositivo en bastidor.  
  
|Tarea|Descripción|  
|--------|---------------|  
|Compruebe que han llegado todos los componentes|Use la lista de materiales (BOM) para comprobar que todos los componentes han llegado y están en sus paletas en la zona de recepción para su centro de datos.|  
|Compruebe que el centro de datos cumple todos los requisitos para el dispositivo|Iniciar esta tarea al revisar las especificaciones de hardware y proporcionar a los IHV de diagramas de cableado. Los pasos siguientes proporcionan información específica acerca de bastidor requisitos de conectividad y el espacio.|  
|Compruebe que el centro de datos tiene espacio en el bastidor correcto|Compruebe que el centro de datos tiene suficiente espacio para todos los bastidores de dispositivo.<br /><br />Compruebe que el espacio en el bastidor está vacío y listo para recibir los bastidores de dispositivo.|  
|Compruebe que el centro de datos cumple los requisitos de conectividad|Compruebe que el centro de datos cumple los requisitos de cableado en los diagramas de cableado.<br /><br />Compruebe que haya espacio para todos los cables y cables de alimentación después de los nodos del dispositivo se montó.|  
|Compruebe que los pisos entre el acoplamiento y los bastidores cumplen los requisitos de peso|Compruebe que todos los suelos entre los bastidores y de las paletas de carga pueden admitir el peso de los nodos del dispositivo, especialmente en los centros de datos con suelos.<br /><br />Para obtener información sobre el peso de cada componente, póngase en contacto con el IHV.|  
|Proteger el centro de datos en bastidor|Proteger el centro de datos bastidor en lugar de mediante un equipo adicional según sea necesario para su ubicación de centro de datos, como bandas a terremoto en áreas geográficas propensas a terremotos.|  
|Prepararse para obtener ayuda con el transporte de los componentes|Determinar de antemano qué asistencia, equipos y las herramientas que necesitará para controlar cada componente de forma segura y sin causar daños.|  
  
## <a name="Moving"></a>Mover los bastidores del muelle de carga en el centro de datos  
Cada pallet contiene todos los componentes de bastidor de uno de los dispositivos, incluidos los nodos, cables, cables, etcetera.  
  
Use la siguiente lista de comprobación para mover cada bastidor del dispositivo desde el pallet en el muelle de carga a su ubicación de bastidor del centro de datos. Mover primero el bastidor de control y, a continuación, mueva los otros bastidores de datos de dispositivo.  
  
> [!WARNING]  
> No llevar a cabo estos pasos exactamente como se describe se podría producir daños corporales, daños en su dispositivo PDW de SQL Server u otros problemas.  
>   
> Nunca intenta levantar o mover un nodo de dispositivo u otro componente pesado sin asistencia o dispositivos adecuados. Póngase en contacto con el IHV para obtener información sobre el peso de cada componente para que pueda determinar de antemano qué asistencia, equipos y las herramientas que necesitará para controlar cada componente de forma segura y sin causar daños.  
  
|Tarea|Descripción|  
|--------|---------------|  
|Compruebe que el pallet es nivel|Antes de empezar a mover o desempaquete el pallet, asegúrese de que está en nivelado.|  
|Unbolt un nodo de la paleta|A partir de la parte superior de la paleta, unbolt el nodo superior de la paleta.|  
|Mover el nodo a una plataforma de mantenimiento o el carro de la que puede admitir el peso|Usar rampas y técnicas de levantar y mover adecuadas para mover el nodo a una plataforma de mantenimiento o el carro de la que puede admitir el peso.|  
|El nodo de transporte en el centro de datos|Usar técnicas de levantar y mover adecuadas para mover el nodo en la posición en el bastidor del centro de datos.|  
|Proteger el nodo en el centro de datos en bastidor|Proteja el nodo en lugar del centro de datos de bastidor.|  
|Repita estos pasos para el nodo o el componente siguiente|Repita estos pasos para mover el nodo siguiente u otro componente de dispositivo en el centro de datos.|  
  
## <a name="AfterMoving"></a>Instalar componentes adicionales  
Utilice la siguiente lista de comprobación para instalar los componentes adicionales.  
  
|Tarea|Descripción||  
|--------|---------------|-|  
|Desempaquetar y conmutadores de red y PDU en bastidor|Utilice los diagramas de bastidor para colocar la PDU y conmutadores de red en la ubicación apropiada en el bastidor.||  
|Conecte los cables Ethernet y de Infiniband según las etiquetas de cable|Consulte el diagrama de cableado. Cada cable tiene una etiqueta en cada extremo que especifica donde es necesario estar conectado.||  
|Conecte todos los cables de alimentación|Consulte el diagrama de cableado.||  
|Activar la fuente de alimentación a los bastidores y la PDU.|Conecte la fuente de alimentación a los bastidores y desde los bastidores de la PDU. **No encender cualquiera de los demás componentes del dispositivo en este momento.**||  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
