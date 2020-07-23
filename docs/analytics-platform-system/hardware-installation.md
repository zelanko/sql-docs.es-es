---
title: Instalación de hardware
description: En este artículo se describe cómo migrar, desempaquetar e instalar el hardware para el dispositivo PDW de SQL Server. Este artículo es meramente informativo y está pensado para ayudarle a comprender el proceso. El dispositivo debe desempaquetarse, instalarse y comprobarse antes de que se le convierta. La participación del cliente es necesaria para elementos como el acceso al centro de datos, la alimentación eléctrica y las conexiones Ethernet.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2e6a0d89b4976076f14fe567b7a95e7cbb47c9f9
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942337"
---
# <a name="hardware-installation-for-analytics-platform-system-aps-appliance"></a>Instalación de hardware para el dispositivo de Analytics Platform System (APS)
En este artículo se describe cómo migrar, desempaquetar e instalar el hardware para el dispositivo PDW de SQL Server. Este artículo es meramente informativo y está pensado para ayudarle a comprender el proceso. El dispositivo debe desempaquetarse, instalarse y comprobarse antes de que se le convierta. La participación del cliente es necesaria para elementos como el acceso al centro de datos, la alimentación eléctrica y las conexiones Ethernet.  
  
## <a name="before-you-move-any-components-from-the-loading-dock"></a><a name="BeforeMoving"></a>Antes de trasladar los componentes del muelle de carga  
Realice las tareas siguientes antes de trasladar, desempaquetar o colocar en bastidor cualquiera de los componentes del dispositivo.  
  
|Tarea|Descripción|  
|--------|---------------|  
|Comprobar que han llegado todos los componentes|Use la lista de materiales (BOM) para comprobar que todos los componentes han llegado y se encuentran en sus pallets en el muelle de recepción de su centro de datos.|  
|Comprobar que el centro de datos cumple todos los requisitos del dispositivo|Para iniciar esta tarea, revise las especificaciones de hardware y los diagramas de cableado que proporciona el IHV. En los pasos siguientes se proporcionan detalles sobre el espacio del bastidor y los requisitos de conectividad.|  
|Compruebe que el centro de datos tiene el espacio en bastidor adecuado|Compruebe que el centro de datos tiene suficiente espacio para todos los bastidores del dispositivo.<br /><br />Compruebe que el espacio del bastidor está vacío y listo para recibir los bastidores del dispositivo.|  
|Comprobar que el centro de datos cumple los requisitos de conectividad|Compruebe que el centro de datos cumple los requisitos de cableado en los diagramas de cableado.<br /><br />Compruebe que habrá espacio para todos los cables y cables de alimentación una vez que los nodos del dispositivo estén en bastidor.|  
|Comprobación de que las plantas entre el muelle y los bastidores cumplen los requisitos de peso|Compruebe que todo el suelo entre los palets y los bastidores puede admitir el peso de los nodos del dispositivo, especialmente en centros de datos con pisos elevados.<br /><br />Póngase en contacto con el IHV para obtener información sobre el peso de cada componente.|  
|Proteger el bastidor del centro de datos|Proteja el bastidor del centro de datos mediante equipos adicionales según sea necesario para la ubicación del centro de datos, como las correas de los terremotos en las zonas geográficas propensas a terremotos.|  
|Preparación para la ayuda con el transporte de componentes|Determine de antemano la asistencia, los equipos y las herramientas que necesitará para controlar cada componente de forma segura y sin causar daños.|  
  
## <a name="move-the-racks-from-the-loading-dock-into-the-data-center"></a><a name="Moving"></a>Mueva los bastidores del muelle de carga al centro de datos  
Cada pallet contiene todos los componentes de un bastidor de dispositivo, incluidos nodos, cables, cables, etc.  
  
Use la siguiente lista de comprobación para desplace cada bastidor del dispositivo desde el palet en el muelle de carga hasta la ubicación del bastidor en el centro de datos. Mueva el bastidor del control primero y, a continuación, mueva los demás bastidores de datos del dispositivo.  
  
> [!WARNING]  
> Si no se realizan estos pasos tal y como se describe, se podría producir un daño corporal, daños en el dispositivo PDW de SQL Server u otros problemas.  
>   
> Nunca intente levantar o trasladar un nodo del dispositivo u otro componente pesado sin necesidad de asistencia o un equipo adecuado. Póngase en contacto con el IHV para obtener información sobre el peso de cada componente, de modo que pueda determinar de antemano qué ayuda, equipo y herramientas necesitarán para administrar cada componente de forma segura y sin causar daños.  
  
|Tarea|Descripción|  
|--------|---------------|  
|Comprobar que el pallet es el nivel|Antes de empezar a migrar o desempaquetar el pallet, asegúrese de que se encuentra en el nivel de suelo.|  
|Quitar el perno de un nodo del pallet|Empezando en la parte superior del pallet, desbolt el nodo superior del pallet.|  
|Mueva el nodo a un Dolly o un carro que pueda admitir el peso|Use rampas y técnicas de traslado y movimiento adecuadas para mover el nodo a un Dolly o un carro que pueda admitir el peso.|  
|Transporte del nodo en el centro de datos|Utilice técnicas adecuadas de elevación y movimiento para mover el nodo a la posición en el bastidor del centro de datos.|  
|Protección del nodo en el bastidor del centro de datos|Proteja el nodo en su lugar en el bastidor del centro de datos.|  
|Repita estos pasos para el siguiente nodo o componente|Repita estos pasos para trasladar el siguiente nodo u otro componente del dispositivo al centro de datos.|  
  
## <a name="install-additional-components"></a><a name="AfterMoving"></a>Instalar componentes adicionales  
Use la siguiente lista de comprobación para instalar los componentes adicionales.  
  
|Tarea|Descripción|
|--------|---------------|
|Desempaquetar y conmutadores de red en bastidor y PDU|Use los diagramas de bastidor para colocar los conmutadores de red y PDU en la ubicación adecuada del bastidor.|
|Conexión de los cables de InfiniBand y Ethernet según las etiquetas de cable|Vea el diagrama de cableado. Cada cable tiene una etiqueta en cada extremo que especifica dónde debe estar conectado.|
|Conectar todos los cables de alimentación|Vea el diagrama de cableado.|
|Encienda la fuente de alimentación en los bastidores y las PDU|Conecte la fuente de alimentación a los bastidores y desde los bastidores a las PDU. **En este momento, no encienda ninguno de los demás componentes del dispositivo.**|
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
