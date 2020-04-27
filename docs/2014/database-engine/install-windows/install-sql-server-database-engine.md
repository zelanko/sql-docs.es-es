---
title: Acerca del Motor de base de datos de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6373f67d40b9da97f652f3bcb05b3414deab5c8d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62779366"
---
# <a name="about-the-sql-server-database-engine"></a>Acerca del motor de base de datos de SQL Server
  El componente [!INCLUDE[ssDE](../../includes/ssde-md.md)] de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el servicio principal para almacenar, procesar y proteger los datos. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] proporciona un acceso controlado y un procesamiento de transacciones rápido para cumplir los requisitos de las aplicaciones consumidoras de datos más exigentes de su empresa.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite hasta 50 instancias del [!INCLUDE[ssDE](../../includes/ssde-md.md)] en un solo equipo. Para crear una instalación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] típica, consulte instalación [de SQL Server 2014 desde el Asistente para la instalación &#40;&#41;de instalación ](install-sql-server-from-the-installation-wizard-setup.md).  
  
 **Importante** : en las instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.  
  
 Las siguientes características se instalan al seleccionar ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos** en la página componentes para instalar del asistente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la instalación de:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   Replicación: es un componente opcional  
  
-   Búsqueda de texto completo: es un componente opcional  
  
-   Data Quality Services: es un componente opcional  
  
    > [!NOTE]  
    >  En esta versión, al activar la casilla **Data Quality Services** en el programa de instalación, no se instala el servidor de Quality Data Services (DQS). Tendrá que realizar pasos adicionales después de la instalación para instalar el servidor DQS. Para más información, consulte [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
 Las siguientes características adicionales son opciones para muchos escenarios de usuario habituales:  
  
-   Cliente de calidad de datos  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Componentes de conectividad  
  
-   Modelos de programación  
  
-   Herramientas de administración  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]  
  
-   Componentes de documentación  
  
> [!NOTE]  
>  De forma predeterminada, las bases de datos y el código de ejemplo no se instalan como parte del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para instalar las bases de datos y el código de ejemplo, vea el [sitio web de CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843).  
  
## <a name="see-also"></a>Consulte también  
 [Características admitidas por las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Ediciones y componentes de SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Planeación de una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Soluciones de alta disponibilidad &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Actualice a SQL Server 2014 mediante el Asistente para la instalación &#40;la instalación&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
