---
title: Importar el módulo de administración de SCOM - Analytics Platform System | Microsoft Docs
description: Siga estos pasos para importar los módulos de administración de System Center Operations Manager (SCOM) para Analytics Platform System (APS). Los módulos de administración necesarias para supervisar el almacenamiento de datos paralelos de SCOM.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: c4280fb257147f3c401badc6eaec18929f6d69b4
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52512647"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>Importar el módulo de administración de SCOM - Analytics Platform System
Siga estos pasos para importar los módulos de administración de System Center Operations Manager (SCOM) para Analytics Platform System (APS). Los módulos de administración necesarias para supervisar el almacenamiento de datos paralelos de SCOM. 
  
## <a name="BeforeBegin"></a>Antes de empezar  
**Requisitos previos**  
  
System Center Operations Manager 2007 R2 debe estar instalado y ejecutándose.  
  
Los módulos de administración deben estar instalados. Consulte [instalar los módulos de administración de SCOM &#40;Analytics Platform System&#41;](install-the-scom-management-packs.md).  
  
## <a name="Step1"></a>Paso 1: Importar el módulo de administración de la Base de aplicación de SQL Server  
  
1.  Inicie sesión en el equipo con una cuenta que sea miembro del rol administradores de Operations Manager para el grupo de administración de Operations Manager 2007.  
  
2.  En la consola del operador, haga clic en **administración**.  
  
3.  Haga clic en el **módulos de administración** nodo y, a continuación, haga clic en **Importar módulos de administración**.  
  
    ![Haga clic en Importar módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM")  
  
4.  En la lista de módulos de administración, seleccione el módulo de administración que desea importar, haga clic en **seleccione**y, a continuación, haga clic en **agregar**.  
  
    ![Lista de módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  Busque **dispositivo** y, a continuación, explorar en profundidad de la Base de aplicación de SQL Server y, a continuación, haga clic en **agregar** las dos opciones.  
  
    ![Dispositivo de SQL Server base](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  Una vez que los dos módulos de administración se encontraban en el panel inferior seleccionado, a continuación, haga clic en **Aceptar**.  
  
    ![Seleccione ambos módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  Haga clic en **Instalar**.  
  
    ![Haga clic en instalar](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  Una vez que haya terminado, haga clic en **cerrar**.  
  
    ![Una vez que haya terminado, haga clic en Cerrar](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>Importar el módulo de supervisión para el dispositivo de almacenamiento de datos paralelos de Microsoft SQL Server 2008 R2  
  
1.  Haga clic en el **módulos de administración** nodo y, a continuación, haga clic en **Importar módulos de administración**.  
  
2.  Elija **agregar del disco**...  
  
    ![Haga clic en los módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  Vaya a la ubicación donde extrajo los módulos de administración de PDW de SQL Server y elija los tres módulos de administración que se encuentran en la sección "Módulos de administración seleccionado para importar". Para ello, seleccione la primera de ellas, al hacer clic en la tecla MAYÚS y seleccione la última de ellas. Una vez que todos estén seleccionados, haga clic en **abierto**.  
  
    ![Seleccionar módulos de administración](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  Haga clic en **Instalar**.  
  
    ![Haga clic en instalar](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  Haga clic en **Cerrar**.  
  
    ![Haga clic en Cerrar](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>Paso siguiente  
Ahora que ha importado los módulos de administración, vaya al paso siguiente: [Configuración de SCOM para supervisar Analytics Platform System &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
