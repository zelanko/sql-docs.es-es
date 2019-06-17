---
title: 'Instalar módulos de administración de SCOM: Analytics Platform System | Microsoft Docs'
description: Siga estos pasos para descargar e instalar los módulos de administración de System Center Operations Manager (SCOM) para PDW de SQL Server. Los módulos de administración necesarias para supervisar SQL Server PDW desde SCOM.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f0acfa636a3432dcffb18cfec57ee7625c1eb01b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63215507"
---
# <a name="install-sql-server-operations-manager-scom-management-packs-for-analytics-platform-system"></a>Instalar los módulos de administración de SQL Server Operations Manager (SCOM) para Analytics Platform System
Siga estos pasos para descargar e instalar los módulos de administración de System Center Operations Manager (SCOM) para PDW de SQL Server. Los módulos de administración necesarias para supervisar SQL Server PDW desde SCOM.  
  
## <a name="BeforeBegin"></a>Antes de empezar  
**Requisitos previos**  
  
System Center Operations Manager debe estar instalado y ejecutándose. PDW de SQL Server 2012 requiere System Center Operations Manager 2007 R2, System Center Operations Manager 2012 o System Center Operations Manager 2012 service pack 1.  
  
## <a name="Step1"></a>Paso 1: Descargar los módulos de administración  
Para la carga de trabajo de APS PDW, descargue el [System Center Management Pack para Microsoft Analytics Platform System](https://go.microsoft.com/fwlink/?LinkId=396857).  
  
Para la administración de dispositivo, descargue el [Base Management Pack de SQL Server Appliance](https://www.microsoft.com/download/details.aspx?displaylang=en&id=11436).  
  
Para versiones anteriores de PDW sin APS, descargue el[módulo de supervisión de System Center para dispositivo de almacenamiento de Microsoft SQL Server 2012 paralelo datos](https://go.microsoft.com/fwlink/p/?LinkId=282661).  
  
<!-- MISSING LINKS - For the HDInsight workload, download the [System Center Management Pack for HDInsight](https://go.microsoft.com/fwlink/?LinkId=390208).  -->
  
## <a name="Step2"></a>Paso 2: Instalar los módulos de administración  
  
### <a name="install-the-sql-server-appliance-base-management-pack"></a>Instalar el módulo de administración de la Base de aplicación de SQL Server  
  
1.  Para ejecutar la instalación, haga doble clic en el módulo de administración de SQL Server Appliance Base descargado.  
  
2.  Acepte el contrato de licencia y haga clic en **siguiente**.  
  
    ![Acepte el contrato de licencia](./media/install-the-scom-management-packs/SCOM_licnse_agrmt.png "SCOM_licnse_agrmt")  
  
3.  Seleccione su propia carpeta de instalación o use la carpeta de instalación del módulo de administración predeterminado.  
  
    ![Seleccione la carpeta de instalación](./media/install-the-scom-management-packs/SCOM_licnse_agrmt2.png "SCOM_licnse_agrmt2")  
  
4.  Haga clic en **Instalar**.  
  
    ![Confirmar la instalación de](./media/install-the-scom-management-packs/SCOM_licnse_agrmt3.png "SCOM_licnse_agrmt3")  
  
5.  Haga clic en **Cerrar**.  
  
    ![Haga clic en Cerrar](./media/install-the-scom-management-packs/SCOM_licnse_agrmt4.png "SCOM_licnse_agrmt4")  
  
### <a name="install-the-monitoring-pack-for-sql-server-pdw-appliance"></a>Instalar el módulo de supervisión para SQL Server PDW Appliance  
  
1.  Para ejecutar la instalación, haga doble clic en el módulo de administración de SQL Server PDW Appliance descargado.  
  
2.  Acepte el contrato de licencia y haga clic en **siguiente**.  
  
    ![Acepte el contrato de licencia](./media/install-the-scom-management-packs/SCOM_licnse_agmtB.png "SCOM_licnse_agmtB")  
  
3.  Elija el directorio que contendrá los archivos extraídos. De forma predeterminada, se muestra la carpeta de instalación del módulo de administración predeterminado. Seleccione el valor predeterminado, o su propia carpeta de instalación.  
  
    ![Carpeta de instalación seleccione](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  Haga clic en **Instalar**.  
  
    ![Confirmar la instalación de](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  Haga clic en **Cerrar**.  
  
    ![Instalación completada](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>Paso siguiente  
Ahora que tiene instalados los módulos de administración, vaya al paso siguiente: [Importar el módulo de administración de SCOM para PDW &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-pdw.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
