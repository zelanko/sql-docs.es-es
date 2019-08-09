---
title: Instalar el Motor de base de datos de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 787c6b96d9f4bad7372a559a1282fa1252e5e97a
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419361"
---
# <a name="install-sql-server-database-engine"></a>Instalar el motor de base de datos de SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

## <a name="overview"></a>Información general
El componente [!INCLUDE[ssDE](../../includes/ssde-md.md)] de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el servicio principal para almacenar, procesar y proteger los datos. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] proporciona un acceso controlado y un procesamiento de transacciones rápido para cumplir los requisitos de las aplicaciones consumidoras de datos más exigentes de su empresa.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite hasta 50 instancias del [!INCLUDE[ssDE](../../includes/ssde-md.md)] en un solo equipo. Para crear una instalación típica de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Instalar SQL Server desde el Asistente para la instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
>[!IMPORTANT]
>En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.  

## <a name="features"></a>Características
Las siguientes características se instalan al seleccionar **Motor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** en la página Componentes para instalar del Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [Replicación de SQL Server](../../relational-databases/replication/sql-server-replication.md): es un componente opcional  

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions" 
-   [Machine Learning Services (en base de datos) con R, Python y Java](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md): es un componente opcional
::: moniker-end

::: monikerRange=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"
-   [Machine Learning Services (en base de datos) con R y Python](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md): es un componente opcional
::: moniker-end

-   Búsqueda de texto completo: es un componente opcional  
  
-   Data Quality Services: es un componente opcional  
  
    > [!NOTE]  
    >  En esta versión, al activar la casilla **Data Quality Services** en el programa de instalación, no se instala el servidor de Quality Data Services (DQS). Tendrá que realizar pasos adicionales después de la instalación para instalar el servidor DQS. Para más información, consulte [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
    
- [Servicio de consultas de PolyBase para datos externos](../../relational-databases/polybase/polybase-guide.md): es un componente opcional. A partir de SQL Server 2019, también está disponible el conector de Java para orígenes de datos HDFS.

  
 Las siguientes características adicionales son opciones para muchos escenarios de usuario habituales:  
  
-   Cliente de calidad de datos
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]
-   Componentes de conectividad
-   Modelos de programación
-   Herramientas de administración
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]
-   Componentes de documentación  
  

> [!NOTE]  
>  De forma predeterminada, las bases de datos y el código de ejemplo no se instalan como parte del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para instalar las bases de datos y el código de ejemplo, vea [Ejemplos de Microsoft SQL Server](../../sample/microsoft-sql-server-samples.md). Vea los ejemplos anteriores en [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843).  

  
## <a name="see-also"></a>Vea también  
 [Ediciones y características admitidas de SQL Server 2017](~/sql-server/editions-and-components-of-sql-server-2017.md)   
 [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Soluciones de alta disponibilidad &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Upgrade SQL Server Using the Installation Wizard &#40;Setup&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md) (Actualización de SQL Server mediante el Asistente para instalación [programa de instalación])  
  
  
