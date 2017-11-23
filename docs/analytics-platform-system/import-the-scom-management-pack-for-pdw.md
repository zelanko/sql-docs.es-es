---
title: "Importar el módulo de administración de SCOM para PDW (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa735041-8e58-4886-ae3b-36f3c6298b12
caps.latest.revision: "6"
ms.openlocfilehash: 2766219fc98a1a3f0174b2c33846fcedb0b74022
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="import-the-scom-management-pack-for-pdw"></a>Importar el módulo de administración de SCOM para PDW
Siga estos pasos para importar los módulos de administración de System Center Operations Manager (SCOM) para SQL Server PDW. Los módulos de administración necesarias para supervisar SQL Server PDW de SCOM.  
  
## <a name="BeforeBegin"></a>Antes de comenzar  
**Requisitos previos**  
  
System Center Operations Manager 2007 R2 debe estar instalado y ejecutándose.  
  
Los módulos de administración deben estar instalados. Vea [instalar los módulos de administración de SCOM &#40; Sistema de la plataforma de análisis &#41; ](install-the-scom-management-packs.md).  
  
## <a name="Step1"></a>Paso 1: Importar el módulo de administración de la Base de aplicación de SQL Server  
  
1.  Inicie sesión en el equipo con una cuenta que sea miembro de la función Administradores de Operations Manager para el grupo de administración de Operations Manager 2007.  
  
2.  En la consola del operador, haga clic en **administración**.  
  
3.  Haga clic en el **módulos de administración** nodo y, a continuación, haga clic en **Importar módulos de administración**.  
  
    ![Haga clic en Importar módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM")  
  
4.  En la lista de módulos de administración, seleccione el módulo de administración que desea importar, haga clic en **seleccione**y, a continuación, haga clic en **agregar**.  
  
    ![Lista de módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  Busque **dispositivo** y, a continuación, profundizar en la Base de dispositivo de SQL Server y, a continuación, haga clic en **agregar** las dos opciones.  
  
    ![Base de dispositivo de SQL Server](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  Una vez que los dos módulos de administración se encontraban en la sección inferior seleccionado, a continuación, haga clic en **Aceptar**.  
  
    ![Seleccionar módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  Haga clic en **Instalar**.  
  
    ![Haga clic en instalar](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  Una vez que haya finalizado, haga clic en **cerrar**.  
  
    ![Una vez que haya finalizado, haga clic en Cerrar](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>Importe el módulo de supervisión para dispositivo de almacenamiento de datos paralelo de Microsoft SQL Server 2008 R2  
  
1.  Haga clic en el **módulos de administración** nodo y, a continuación, haga clic en **Importar módulos de administración**.  
  
2.  Elija **agregar del disco**...  
  
    ![Haga clic en módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  Vaya a la ubicación donde extrajo los módulos de administración de PDW de SQL Server y elija los tres módulos de administración que se encuentran en la sección "Seleccionados los módulos de administración para importar". Para ello, puede seleccionar la primera de ellas, haga clic en la tecla MAYÚS y seleccionar la última de ellas. Una vez que todos estén seleccionados, haga clic en **abiertos**.  
  
    ![Seleccionar módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  Haga clic en **Instalar**.  
  
    ![Haga clic en instalar](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  Haga clic en **Cerrar**.  
  
    ![Haga clic en Cerrar](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>Paso siguiente  
Ahora que ha importado los módulos de administración, vaya al paso siguiente: [configurar SCOM para supervisar Analytics Platform System &#40; Sistema de la plataforma de análisis &#41; ](configure-scom-to-monitor-analytics-platform-system.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
