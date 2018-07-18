---
title: Configuración del firewall PDW - Analytics Platform System | Microsoft Docs
description: La página de firewall de SQL Server PDW Configuration Manager permite habilitar o deshabilitar las reglas de firewall que permiten o impiden el acceso a puertos específicos de la aplicación Analytics Platform System.
aauthor: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3195007b4346c6010b416fae833643f3a80136fb
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909845"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>Configuración de firewall de almacenamiento de datos paralelo de Analytics Platform System
El **Firewall** página de SQL Server PDW Configuration Manager le permite habilitar o deshabilitar las reglas de firewall que permiten o impiden el acceso a puertos específicos de la aplicación Analytics Platform System.  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>Para administrar los puertos y reglas para los nodos del dispositivo de firewall  
  
1.  Inicie el Administrador de configuración. Para obtener más información, consulte [iniciar el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  
  
2.  En el panel izquierdo del Administrador de configuración, expanda **topología de almacenamiento de datos paralela**y, a continuación, haga clic en **Firewall**.  
  
3.  Busque la regla de puerto o un firewall para actualizar en la lista de configuración y, a continuación, active o desactive la casilla situada junto a ese elemento. Solo opciones configurables por el Administrador de PDW de SQL Server se muestran en esta lista, incluyendo abrir y cerrar los puertos en orientado externamente a nodos.  
  
4.  Haga clic en **aplicar** para guardar los cambios.  
  
![Firewall PDW del dispositivo DWConfig](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>Puertos externos  
Se abren los puertos siguientes para las conexiones de cliente procedentes de fuera de PDW.  
  
|Finalidad|Número de puerto|Nodos|  
|-----------|-----------|---------|  
|Acceso de cliente de SQL para PDW (TDS)|17001|CTL|  
|Acceso de cliente del cargador (dwloader & SSIS)|8001|CTL|  
|Acceso a Escritorio remoto|3389|CTL, CMP|  
|SSIS BinaryLoaderDataChannel|16551|CTL|  
|BinaryLoaderDataChannel dwloader|16551|CMP|  
|SSL cifra las conexiones (para las comunicaciones internas, para tener acceso a la consola de administración)|443|Todos los nodos|  
|Flujo de Control de carga SQL Server PDW - las credenciales de Windows|8002|CTL|  
|_Kerberos|88|AD01 y AD02,|  
|_ldap|389|AD01 y AD02|  
  
## <a name="internal-ports"></a>Puertos internos  
Los siguientes puertos se usan con PDW para la comunicación interna, pero no están abiertos para las conexiones procedentes de fuera de la aplicación de PDW.  
  
|Finalidad|Número de puerto|Nodos|  
|-----------|-----------|---------|  
|Tráfico del canal de Control de DMS|16450|CTL, CMP|  
|Tráfico del canal de datos de DMS|16550|CTL, CMP|  
|Diagnóstico interno|16650|CTL, CMP|  
|Estado de conmutación por error (DMS)|15000|CTL, CMP|  
|Estado de conmutación por error (motor de)|15001|CMP|  
|Intervalo de puertos dinámicos (efímero)|20000-65535|CTL, CMP|  
|Intervalos de puertos de SQL Server (TDS)|1433, 1500-1508|CTL, CMP|  
  
> [!NOTE]  
> Creación de tablas externas u orígenes de datos externos, usa el puerto TCP 8020 de forma predeterminada. Estas instrucciones pueden configurarse para utilizar otros puertos en su lugar. El puerto predeterminado de Hortonworks JOB_TRACKER_LOCATION es 50300. La integración con otras herramientas y sistemas puede requerir puertos adicionales.  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)  -->  
  
