---
title: Copias de tablas remotas
description: Describe cómo configurar el almacenamiento de datos paralelos para utilizar la característica de copia de tabla remota para copiar tablas en bases de datos de SMP SQL Server en servidores que no son de dispositivo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6c9a0a29b543eb287c7e233d6b1ea77bb2a0d45c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401265"
---
# <a name="configure-parallel-data-warehouse-for-remote-table-copies"></a>Configurar el almacenamiento de datos paralelo para copias de tablas remotas
Describe cómo configurar PDW de SQL Server para usar la característica de copia de tabla remota para copiar tablas en bases de datos de SMP SQL Server en servidores que no son de dispositivo.  
  
En este tema se describe uno de los pasos de configuración para configurar la copia de tabla remota. Para obtener una lista de todos los pasos de configuración, consulte [copia de tabla remota](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Antes de empezar  
Para configurar PDW de SQL Server para usar la copia de tabla remota, debe:  
  
-   Tener una cuenta de administrador del sistema de plataforma de análisis con la posibilidad de iniciar sesión directamente en los nodos <strong> *appliance_domain*-AD01</strong> y de <strong> *appliance_domain*AD02</strong> .  
  
-   Conozca el nombre de host o el nombre de IP del servidor de destino.  
  
## <a name="HowToPDW"></a>Configurar PDW de SQL Server para la copia de tabla remota: actualizar nombres de host en DNS  
La instrucción **Create REMOTE Table** , que se usa para copias de tablas remotas, especifica el servidor de destino mediante la dirección IP o el nombre de IP del sistema de Windows SMP. Para usar el nombre de IP, debe agregar entradas para la resolución de nombres correcta en el servidor DNS.  
  
En los pasos siguientes se describe cómo actualizar el servidor DNS.  
  
1.  Inicie sesión en el nodo Active Directory (normalmente <strong> *appliance_domain*-AD01</strong>).  
  
2.  Abra el administrador de DNS. Se encuentra en **herramientas administrativas** en el menú **Inicio** .  
  
3.  Use el administrador de DNS para agregar el nombre de IP.  
  
## <a name="see-also"></a>Consulte también  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Usar un reenviador DNS para resolver nombres DNS que no sean de aplicación](use-a-dns-forwarder-to-resolve-non-appliance-dns-names.md)  
<!-- MISSING LINKS 
[Security - Configure Domain Trusts &#40;SQL Server PDW&#41;](../sqlpdw/security-configure-domain-trusts-sql-server-pdw.md)  
-->
  
