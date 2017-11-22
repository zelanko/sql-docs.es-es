---
title: "Instalar los módulos de administración de SCOM (Analytics Platform System)"
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
ms.assetid: ab3985d8-0a71-4b28-9d28-9886ae2a110f
caps.latest.revision: "16"
ms.openlocfilehash: f20048a70ef04bba475f9e8e6b58b24095f23f1a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="install-the-scom-management-packs"></a>Instalar los módulos de administración de SCOM
Siga estos pasos para descargar e instalar los módulos de administración de System Center Operations Manager (SCOM) para SQL Server PDW. Los módulos de administración necesarias para supervisar SQL Server PDW de SCOM.  
  
## <a name="BeforeBegin"></a>Antes de comenzar  
**Requisitos previos**  
  
System Center Operations Manager debe estar instalado y ejecutándose. PDW de SQL Server 2012 requiere System Center Operations Manager 2007 R2, System Center Operations Manager 2012 o System Center Operations Manager 2012 service pack 1.  
  
## <a name="Step1"></a>Paso 1: Descargar los módulos de administración  
Para la carga de trabajo de APS PDW, descargue el [System Center Management Pack para Microsoft Analytics Platform System](http://go.microsoft.com/fwlink/?LinkId=396857).  
  
Para la administración del equipo, descargue el [módulo de administración de SQL Server Appliance Base](http://www.microsoft.com/en-us/download/details.aspx?displaylang=en&id=11436).  
  
Para versiones anteriores de PDW sin APS, descargue el[módulo de supervisión de System Center para el dispositivo de almacenamiento de Microsoft SQL Server 2012 paralelo datos](http://go.microsoft.com/fwlink/p/?LinkId=282661).  
  
Para la carga de trabajo de HDInsight, descargue el [System Center Management Pack para HDInsight](http://go.microsoft.com/fwlink/?LinkId=390208).  
  
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
  
3.  Elija el directorio que contendrá los archivos extraídos. La carpeta de instalación de módulo de administración de forma predeterminada se muestra de forma predeterminada. Seleccione el valor predeterminado, o su propia carpeta de instalación.  
  
    ![Carpeta de instalación seleccione](./media/install-the-scom-management-packs/SCOM_licnse_agmtB1.png "SCOM_licnse_agmtB1")  
  
4.  Haga clic en **Instalar**.  
  
    ![Confirmar la instalación de](./media/install-the-scom-management-packs/SCOM_licnse_agmtB2.png "SCOM_licnse_agmtB2")  
  
5.  Haga clic en **Cerrar**.  
  
    ![Se completó la instalación](./media/install-the-scom-management-packs/SCOM_licnse_agmtB3.png "SCOM_licnse_agmtB3")  
  
## <a name="next-step"></a>Paso siguiente  
Ahora que tiene los módulos de administración instalados, vaya al paso siguiente: [importar el módulo de administración de SCOM para PDW &#40; Sistema de la plataforma de análisis &#41; ](import-the-scom-management-pack-for-pdw.md).  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
