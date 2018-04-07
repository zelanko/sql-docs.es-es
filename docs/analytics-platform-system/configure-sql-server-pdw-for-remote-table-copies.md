---
title: Configurar SQL Server PDW para copias de la tabla remota (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 496b4214-5891-404c-8237-c2a1e09db6d5
caps.latest.revision: 11
ms.openlocfilehash: 46fdb88ce3a244946b89f14320229905793564ac
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="configure-sql-server-pdw-for-remote-table-copies"></a>Configurar SQL Server PDW para copias de la tabla remota
Describe cómo configurar SQL Server PDW para usar la característica de copia de la tabla remota para copiar tablas a las bases de datos de SMP de SQL Server en los servidores no sea de dispositivo.  
  
En este tema se describe uno de los pasos de configuración para configurar la copia de la tabla remota. Para obtener una lista de todos los pasos de configuración, consulte [copia de tabla remota](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Antes de comenzar  
Para configurar SQL Server PDW para usar copia de la tabla remota, debe:  
  
-   Tener una cuenta de administrador de sistema de la plataforma de análisis con la capacidad de iniciar sesión directamente en el ***appliance_domain *-AD01** y ***appliance_domain *-AD02** nodos.  
  
-   Conocer el nombre de host o el nombre IP del servidor de destino.  
  
## <a name="HowToPDW"></a>Configurar SQL Server PDW para copia de la tabla remota: actualizar los nombres de Host en DNS  
El **crear tabla remota** instrucción, que se utiliza para las copias de la tabla remota, especifica el servidor de destino mediante el uso de la dirección IP o el nombre IP del sistema de Windows de SMP. Para utilizar el nombre IP, debe agregar entradas para la resolución de nombres correcta para el servidor DNS.  
  
Los pasos siguientes describen cómo actualizar el servidor DNS.  
  
1.  Inicie sesión en el nodo activo de AD (normalmente ***appliance_domain *-AD01**).  
  
2.  Abra el Administrador de DNS. Esto se encuentra en **herramientas administrativas** en el **iniciar** menú.  
  
3.  Use el Administrador de DNS para agregar el nombre IP.  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Usar un reenviador DNS para resolver nombres DNS no sea de dispositivo](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
