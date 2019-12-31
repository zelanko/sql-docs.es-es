---
title: Instalar los módulos de administración de SCOM
description: Siga estos pasos para descargar e instalar los módulos de administración de System Center Operations Manager (SCOM) para PDW de SQL Server. Los módulos de administración son necesarios para supervisar PDW de SQL Server de SCOM.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f3652b767f4628b61f5dd363999838418ff933aa
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401070"
---
# <a name="install-sql-server-operations-manager-scom-management-packs-for-analytics-platform-system"></a>Instalación de los módulos de administración de SQL Server Operations Manager (SCOM) para Analytics Platform System
Siga estos pasos para descargar e instalar los módulos de administración de System Center Operations Manager (SCOM) para PDW de SQL Server. Los módulos de administración son necesarios para supervisar PDW de SQL Server de SCOM.  
  
## <a name="BeforeBegin"></a>Antes de empezar  
**Requisitos previos**  
  
System Center Operations Manager debe estar instalado y en ejecución. PDW de SQL Server 2012 requiere System Center Operations Manager 2007 R2, System Center Operations Manager 2012 o System Center Operations Manager 2012 Service Pack 1.  
  
## <a name="Step1"></a>Paso 1: descargar los módulos de administración  
Para la carga de trabajo PDW de APS, descargue el [módulo de administración de System Center para el Microsoft Analytics Platform System](https://go.microsoft.com/fwlink/?LinkId=396857).  
  
Para la administración del dispositivo, descargue el módulo de administración de la [base de SQL Server Appliance](https://docs.microsoft.com/previous-versions/system-center/packs/gg602398(v=technet.10)).  
  
Para versiones anteriores de PDW sin APS, descargue el[módulo de supervisión de System Center para el dispositivo de almacenamiento de datos paralelos Microsoft SQL Server 2012](https://go.microsoft.com/fwlink/p/?LinkId=282661).  
  
<!-- MISSING LINKS - For the HDInsight workload, download the [System Center Management Pack for HDInsight](https://go.microsoft.com/fwlink/?LinkId=390208).  -->
  
## <a name="Step2"></a>Paso 2: instalación de los módulos de administración  
  
### <a name="install-the-sql-server-appliance-base-management-pack"></a>Instalar el módulo de administración de la base de SQL Server Appliance  
  
1.  Para ejecutar la instalación, haga doble clic en el módulo de administración de la base del dispositivo SQL Server descargado.  
  
2.  Acepte el contrato de licencia y haga clic en **siguiente**.  
  
    ![Aceptar el contrato de licencia](./media/install-the-scom-management-packs/SCOM_licnse_agrmt.png "SCOM_licnse_agrmt")  
  
3.  Seleccione su propia carpeta de instalación o use la carpeta de instalación del módulo de administración predeterminado.  
  
    ![Seleccionar carpeta de instalación](./media/install-the-scom-management-packs/SCOM_licnse_agrmt2.png "SCOM_licnse_agrmt2")  
  
4.  Haga clic en **Instalar**.  
  
    ![Confirme la instalación](./media/install-the-scom-management-packs/SCOM_licnse_agrmt3.png "SCOM_licnse_agrmt3")  
  
5.  Haga clic en **Cerrar**.  
  
    ![Haga clic en cerrar](./media/install-the-scom-management-packs/SCOM_licnse_agrmt4.png "SCOM_licnse_agrmt4")  
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>Instalar el módulo de supervisión para PDW de SQL Server dispositivo  
  
1.  Para ejecutar la instalación, haga doble clic en el módulo de administración del dispositivo PDW de SQL Server descargado.  
  
2.  Acepte el contrato de licencia y haga clic en **siguiente**.  
  
    ![Acepte el contrato de licencia](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  Elija el directorio que contendrá los archivos extraídos. De forma predeterminada, se muestra la carpeta de instalación del módulo de administración predeterminado. Seleccione el valor predeterminado o seleccione su propia carpeta de instalación.  
  
    ![Seleccionar carpeta de instalación](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  Haga clic en **Instalar**.  
  
    ![Confirme la instalación](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  Haga clic en **Cerrar**.  
  
    ![Instalación completada](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>Paso siguiente  
Ahora que tiene instalados los módulos de administración, continúe con el paso siguiente: [importar el módulo de administración de SCOM para PDW &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
