---
title: Acerca de cómo el motor de base de datos SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Database Engine [SQL Server], installing
ms.assetid: d0876e7f-aa52-4dd7-bd5c-029e2ffded5f
caps.latest.revision: 44
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4316e91e465922ca1f7c428a9f25e781837ec6e4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112526"
---
# <a name="about-the-sql-server-database-engine"></a>Acerca del motor de base de datos de SQL Server
  El componente [!INCLUDE[ssDE](../../includes/ssde-md.md)] de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es el servicio principal para almacenar, procesar y proteger los datos. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] proporciona un acceso controlado y un procesamiento de transacciones rápido para cumplir los requisitos de las aplicaciones consumidoras de datos más exigentes de su empresa.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite hasta 50 instancias del [!INCLUDE[ssDE](../../includes/ssde-md.md)] en un solo equipo. Para crear una típica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalación, consulte [instalar SQL Server 2014 desde el Asistente para la instalación &#40;el programa de instalación&#41;](install-sql-server-from-the-installation-wizard-setup.md).  
  
 **Importante** : en las instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura y ejecución para dicho recurso.  
  
 Las siguientes características se instalan al seleccionar **Motor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** en la página Componentes para instalar del Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
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
>  De forma predeterminada, las bases de datos y el código de ejemplo no se instalan como parte del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para instalar las bases de datos y el código de ejemplo, vea el [sitio web de CodePlex](http://go.microsoft.com/fwlink/?LinkId=87843).  
  
## <a name="see-also"></a>Vea también  
 [Características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Ediciones y componentes de SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Soluciones de alta disponibilidad &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)   
 [Actualización a SQL Server 2014 mediante el Asistente para la instalación &#40;el programa de instalación&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  