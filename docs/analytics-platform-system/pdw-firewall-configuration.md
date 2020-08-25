---
title: Configuración de firewall de PDW
description: La página Firewall de la PDW de SQL Server Configuration Manager le permite habilitar o deshabilitar las reglas de firewall que permiten o impiden el acceso a puertos específicos en el dispositivo de sistema de plataforma de análisis.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ed739ce12170aa6d0ab79b996de0075cd6723ee
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400882"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>Configuración del firewall de almacenamiento de datos paralelos en Analytics Platform System

La página **firewall** de la PDW de SQL Server Configuration Manager le permite habilitar o deshabilitar las reglas de firewall que permiten o impiden el acceso a puertos específicos en el dispositivo de sistema de plataforma de análisis.  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>Para administrar los puertos y las reglas de Firewall de los nodos del dispositivo  
  
1.  Inicie el Configuration Manager. Para obtener más información, consulte [Inicio del&#41;de &#40;de Configuration Manager de la plataforma de análisis ](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo del Configuration Manager, expanda **topología de almacenamiento de datos paralelo**y, a continuación, haga clic en **firewall**.  
  
3.  Busque el puerto o la regla de firewall que desea actualizar en la lista configuración y, a continuación, Active o desactive la casilla situada junto a ese elemento. En esta lista solo se muestran las opciones configurables por el administrador de PDW de SQL Server, incluidos puertos de apertura y cierre en nodos orientados externamente.  
  
4.  Haga clic en **aplicar** para guardar los cambios.  
  
![Firewall PDW del dispositivo DWConfig](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>Puertos externos  
Los puertos siguientes se abren para las conexiones de cliente que proceden de fuera de PDW.  
  
|Propósito|Casilla #|Nodos|  
|-----------|-----------|---------|  
|Acceso de cliente SQL para PDW (TDS)|17001|RECIÉN|  
|Acceso de cliente del cargador (dwloader & SSIS)|8001|RECIÉN|  
|Acceso de Escritorio remoto|3389|CTL, CMP|  
|BinaryLoaderDataChannel de SSIS|16551|RECIÉN|  
|dwloader BinaryLoaderDataChannel|16551|CMP|  
|Conexiones SSL cifradas (para las comunicaciones internas, para tener acceso a la consola de administración)|443|Todos los nodos|  
|PDW de SQL Server cargar el flujo de control: credenciales de Windows|8002|RECIÉN|  
|_Kerberos|88|AD01 y AD02,|  
|_ldap|389|AD01 y AD02|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="internal-ports"></a>Puertos internos  
PDW usa los siguientes puertos para la comunicación interna, pero no se abren para las conexiones que proceden de fuera de la aplicación PDW.  
  
|Propósito|Casilla #|Nodos|  
|-----------|-----------|---------|  
|Tráfico de canal de control DMS|16450|CTL, CMP|  
|Tráfico del canal de datos DMS|16550|CTL, CMP|  
|Diagnósticos internos|16650|CTL, CMP|  
|Estado de conmutación por error (DMS)|15000|CTL, CMP|  
|Estado de conmutación por error (motor)|15001|CMP|  
|Intervalo de puertos dinámico (efímero)|20000-65535|CTL, CMP|  
|Intervalos de puertos de SQL Server (TDS)|1433, 1500-1508|CTL, CMP|  
| &nbsp; | &nbsp; | &nbsp; |
  
> [!NOTE]  
> Al crear tablas externas o orígenes de datos externos se usa el puerto TCP 8020 de forma predeterminada. Estas instrucciones se pueden configurar para usar otros puertos en su lugar. El puerto predeterminado de Hortonworks JOB_TRACKER_LOCATION es 50300. La integración con otros sistemas y herramientas puede requerir puertos adicionales.  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)
-->
  
