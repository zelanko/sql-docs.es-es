---
title: Importar módulo de administración de SCOM
description: Siga estos pasos para importar los módulos de administración de System Center Operations Manager (SCOM) para Analytics Platform System (APS). Los módulos de administración son necesarios para supervisar el almacenamiento de datos paralelos de SCOM.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: bcb0e667424767fd53a5fc7e027e84d512022203
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401083"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>Importar el módulo de administración de SCOM-Analytics Platform System
Siga estos pasos para importar los módulos de administración de System Center Operations Manager (SCOM) para Analytics Platform System (APS). Los módulos de administración son necesarios para supervisar el almacenamiento de datos paralelos de SCOM. 
  
## <a name="before-you-begin"></a><a name="BeforeBegin"></a>Antes de empezar  
**Requisitos previos**  
  
System Center Operations Manager 2007 R2 debe estar instalado y en ejecución.  
  
Los módulos de administración deben estar instalados. Consulte [instalación de los módulos de administración de SCOM &#40;Analytics Platform System&#41;](install-the-scom-management-packs.md).  
  
## <a name="step-1-import-the-sql-server-appliance-base-management-pack"></a><a name="Step1"></a>Paso 1: importar el módulo de administración de la base de SQL Server Appliance  
  
1.  Inicie sesión en el equipo con una cuenta que tenga el rol Administradores de Operations Manager para el grupo de administración de Operations Manager 2007.  
  
2.  En la consola de Operations, haga clic en **Administración**.  
  
3.  Haga clic con el botón secundario en el nodo **Módulos de administración** y, a continuación, haga clic en **Importar módulos de administración**.  
  
    ![Haga clic en Importar módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM_IMP")  
  
4.  En la lista de módulos de administración, seleccione el que quiera importar, haga clic en **Seleccionar** y, luego, en **Agregar**.  
  
    ![Lista de módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  Busque el **dispositivo** y, a continuación, explore en profundidad SQL Server base del dispositivo y, a continuación, haga clic en **Agregar** las dos opciones.  
  
    ![Base de dispositivo SQL Server](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  Una vez que los dos módulos de administración estén en el panel de la parte inferior seleccionada, haga clic en **Aceptar**.  
  
    ![Seleccione ambos módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  Haga clic en **Instalar**.  
  
    ![Haga clic en instalar](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  Cuando haya terminado, haga clic en **cerrar**.  
  
    ![Una vez se haya completado, haga clic en Cerrar](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="import-the-monitoring-pack-for-microsoft-sql-server-2008-r2-parallel-data-warehouse-appliance"></a><a name="Step2"></a>Importar el módulo de supervisión para el dispositivo de almacenamiento de datos paralelos Microsoft SQL Server 2008 R2  
  
1.  Haga clic con el botón secundario en el nodo **Módulos de administración** y, a continuación, haga clic en **Importar módulos de administración**.  
  
2.  Elija **Agregar desde disco**....  
  
    ![Haga clic con el botón secundario en los módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  Vaya a la ubicación donde extrajo el PDW de SQL Server módulos de administración y elija los tres módulos de administración que se encuentran en la sección "módulos de administración seleccionados para importar". Para ello, seleccione el primero, haga clic en Mayús y seleccione el último. Una vez que todos estén seleccionados, haga clic en **abrir**.  
  
    ![Seleccionar módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  Haga clic en **Instalar**.  
  
    ![Haga clic en instalar](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  Haga clic en **Cerrar**.  
  
    ![Haga clic en cerrar](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>siguiente paso  
Ahora que ha importado los módulos de administración, continúe con el paso siguiente: [configurar SCOM para supervisar Analytics Platform system &#40;Analytics Platform system&#41;](configure-scom-to-monitor-analytics-platform-system.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
