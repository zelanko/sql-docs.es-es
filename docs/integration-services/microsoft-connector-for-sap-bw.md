---
description: Microsoft Connector for SAP BW
title: Microsoft Connector for SAP BW | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5281f080-53d5-4679-aa26-f4cd4ac7a2df
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 05fefa983f3b58f8ca8be95772d3fbc49f3e9afb
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194077"
---
# <a name="microsoft-connector-for-sap-bw"></a>Microsoft Connector for SAP BW

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW consta de un conjunto de tres componentes que le permiten tanto extraer datos de un sistema SAP NetWeaver BW versión 7 como cargarlos en él.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW para SQL Server 2016 es un componente de SQL Server 2016 Feature Pack. Para instalar Connector for SAP BW y su documentación, descargue y ejecute el instalador desde la [página web de SQL Server 2016 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=746297).  

> [!IMPORTANT]
> Microsoft no prevé proporcionar una versión actualizada del conector de SAP BW. Microsoft no posee el código fuente de los componentes de SAP BW, que fueron desarrollados por terceros, por lo que no puede actualizarlos. Sopese la posibilidad de adquirir los componentes de conectividad de SAP más recientes de un socio de Microsoft ISV, como [Theobald Software](https://theobald-software.com/en/xtract-is-productinfo.html). Los socios de ISV de Microsoft han adaptado sus componentes de conectividad de SAP para SSIS para su instalación en Azure.
 
> [!IMPORTANT]  
>  La documentación de Microsoft Connector for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
> [!IMPORTANT]  
>  La extracción de datos de SAP Netweaver BW requiere una licencia SAP adicional. Póngase en contacto con SAP para comprobar estos requisitos.  
  
## <a name="components"></a>Componentes  
 [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW tiene los siguientes componentes:  
  
-   **Origen de SAP BW**: el origen de SAP BW es un componente de origen de flujo de datos que le permite extraer datos de un sistema SAP Netweaver BW versión 7.  
  
-   **Destino de SAP BW**: el destino de SAP BW es un componente de destino de flujo de datos que le permite cargar datos en un sistema SAP Netweaver BW versión 7.  
  
-   **Administrador de conexiones de SAP BW**: el administrador de conexiones de SAP BW conecta un origen o un destino de SAP BW con un sistema SAP Netweaver BW versión 7.  
  
 Para obtener instrucciones sobre cómo configurar y utilizar el administrador de conexiones, el origen y el destino de SAP BW, vea las notas del producto, [Usar SQL Server Integration Services con SAP BI 7.0](/previous-versions/sql/sql-server-2008/dd299430(v=sql.100)). Estas notas del producto también muestran cómo configurar los objetos necesarios en SAP BW.  
  
## <a name="documentation"></a>Documentación  
 Este archivo de Ayuda de [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW contiene los temas y las secciones siguientes:  
  
 [Instalación de Microsoft Connector for SAP BW](../integration-services/installing-the-microsoft-connector-for-sap-bw.md)  
 Se describen los requisitos de instalación para [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW.  
  
 [Componentes de Microsoft Connector for SAP BW](../integration-services/microsoft-connector-for-sap-bw-components.md)  
 Se describen los componentes de [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW.  
  
 [Ayuda F1 de Microsoft Connector for SAP BW](../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
 Se describe la interfaz de usuario de los componentes de [!INCLUDE[msCoName](../includes/msconame-md.md)] Connector for SAP BW.  
  
