---
title: Alta disponibilidad en SQL Server Reporting Services | Microsoft Docs
description: Obtenga información sobre la mejor manera de garantizar la disponibilidad de la funcionalidad de Reporting Services en SQL Server.
ms.date: 10/05/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7cac05af8a930b6926ca1b643a9eaef6d198e86a
ms.sourcegitcommit: 66a0672e47415dbd5cfd8d19075102c8c3973e70
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2020
ms.locfileid: "83766999"
---
# <a name="high-availability-in-sql-server-reporting-services"></a>Alta disponibilidad en SQL Server Reporting Services

Un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es un servidor sin estado que almacena dato de la aplicación, contenido, propiedades e información de la sesión en dos bases de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relacionales. Como tal, la mejor manera de asegurarse la disponibilidad de la funcionalidad de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es hacer el siguiente:  
  
-   Use las características de alta disponibilidad del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] para maximizar el tiempo de funcionamiento de las bases de datos del servidor de informes. Si configura una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que se ejecute en un clúster de conmutación por error, puede seleccionar dicha instancia al crear una base de datos del servidor de informes.  
  
-   Use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] con los orígenes de datos y las bases de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], según sea posible. Para más información, vea [Reporting Services con grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/reporting-services-with-always-on-availability-groups-sql-server.md).  
  
-   Configure varios servidores de informes para que se ejecuten en una implementación escalada, en la que todos los servidores comparten una única base de datos de servidor de informes. La implementación de varias instancias del servidor de informes, preferentemente en servidores diferentes, en una implementación escalada puede ayudar a proporcionar un servicio ininterrumpido en el caso de que se bloquee una de las instancias del servidor de informes.  
  
 Una implementación escalada proporciona una manera de compartir una base de datos. Si un servidor de informes se bloquea, otros servidores de la misma implementación continuarán funcionando.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no detecta los clústeres. Por sí sola, una implementación escalada no proporciona equilibrio de carga; no detecta las cargas de procesamiento en un servidor de informes y enruta las nuevas solicitudes de procesamiento al servidor menos ocupado. No vuelve a enrutar las solicitudes de procesamiento que no fueron correctas antes de la finalización. Para obtener características de equilibrio de carga, debe configurar el equilibrio de carga para los servidores web que hospedan los servidores de informes y, a continuación, obtener los servidores de informes en una implementación escalada de manera que compartan la misma base de datos del servidor de informes.  
  
 El servicio de Windows y el servicio web del servidor de informes están estrechamente integrados y se ejecutan en conjunto como una instancia del servidor de informes única. No puede configurar la disponibilidad para un servicio de manera independiente del otro.  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
