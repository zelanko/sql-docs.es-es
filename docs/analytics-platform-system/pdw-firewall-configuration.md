---
title: Configuración del firewall PDW - Analytics Platform System | Documentos de Microsoft
description: La página de firewall de SQL Server PDW Configuration Manager permite habilitar o deshabilitar las reglas de firewall que permiten o impedir el acceso a puertos específicos en el dispositivo de sistema de la plataforma de análisis.
aauthor: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 8ccfd60aee7647c2421870a09ab5fa9b2653b99d
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539385"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>Configuración de firewall de almacenamiento de datos paralelo en el sistema de la plataforma de análisis
El **Firewall** página de SQL Server PDW Configuration Manager le permite habilitar o deshabilitar las reglas de firewall que permiten o impedir el acceso a puertos específicos en el dispositivo de sistema de la plataforma de análisis.  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>Para administrar los puertos y las reglas para los nodos de dispositivo de firewall  
  
1.  Inicie el Administrador de configuración. Para obtener más información, consulte [iniciar el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo del Administrador de configuración, expanda **topología de almacenamiento de datos paralelos**y, a continuación, haga clic en **Firewall**.  
  
3.  Localice la regla de puerto o el firewall para actualizar en la lista de configuración y, a continuación, active o desactive la casilla situada junto a ese elemento. Solo opciones configurables por el Administrador de SQL Server PDW se muestran en esta lista, como abrir y cerrar puertos en orientados externamente nodos.  
  
4.  Haga clic en **aplicar** para guardar los cambios.  
  
![Firewall PDW del dispositivo DWConfig](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>Puertos externos  
Se abren los puertos siguientes para las conexiones de cliente procedentes de fuera de PDW.  
  
|Finalidad|Número de puerto|Nodos|  
|-----------|-----------|---------|  
|Acceso de cliente de SQL para PDW (TDS)|17001|CTL|  
|Acceso de cliente de cargador (dwloader & SSIS)|8001|CTL|  
|Acceso al escritorio remoto|3389|CTL, CMP|  
|BinaryLoaderDataChannel SSIS|16551|CTL|  
|dwloader BinaryLoaderDataChannel|16551|CMP|  
|SSL cifra las conexiones (para las comunicaciones internas, para tener acceso a la consola de administración y tener acceso a servicios de clúster de HDInsight)|443|Todos los nodos|  
|Flujo de Control de carga SQL Server PDW - las credenciales de Windows|8002|CTL|  
|_Kerberos|88|AD01 y AD02,|  
|_ldap|389|AD01 y AD02|  
  
## <a name="internal-ports"></a>Puertos internos  
Los siguientes puertos PDW sirven para la comunicación interna, pero no se hayan abierto para las conexiones procedentes de fuera de la aplicación de PDW.  
  
|Finalidad|Número de puerto|Nodos|  
|-----------|-----------|---------|  
|Tráfico del canal de Control de DMS|16450|CTL, CMP|  
|Tráfico del canal de datos de DMS|16550|CTL, CMP|  
|Diagnósticos internos|16650|CTL, CMP|  
|Estado de conmutación por error (DMS)|15000|CTL, CMP|  
|Estado de conmutación por error (motor de)|15001|CMP|  
|Intervalo de puertos dinámicos (efímero)|20000-65535|CTL, CMP|  
|Intervalos de puertos de SQL Server (TDS)|1433, 1500-1508|CTL, CMP|  
  
> [!NOTE]  
> Crear tablas externas u orígenes de datos externos, usa el puerto TCP 8020 de forma predeterminada. Estas instrucciones pueden configurarse para utilizar otros puertos en su lugar. El puerto predeterminado de Hortonworks JOB_TRACKER_LOCATION es 50300. Integración con otros sistemas y herramientas requieran puertos adicionales.  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)  -->  
  
