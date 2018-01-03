---
title: "Información general de la arquitectura de controlador | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], architecture
- FoxPro ODBC driver [ODBC], architecture
ms.assetid: ef5a91cd-158e-40bf-b5a8-8ba535c4705e
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2778161fa117e164a4c49e57a5511b0682507b37
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="driver-architecture-overview"></a>Información general de la arquitectura de controlador
El controlador ODBC de Microsoft Visual FoxPro es un controlador de 32 bits que permite abrir y consultar una base de datos de Microsoft Visual FoxPro o tablas de FoxPro a través de la interfaz de conectividad abierta de base de datos (ODBC). Puede tener acceso a datos de FoxPro utilizando los siguientes tipos de aplicaciones:  
  
-   Una aplicación de Microsoft Office, como Microsoft Excel o Microsoft Word, que utiliza Microsoft Query para comunicarse con ODBC.  
  
-   Una aplicación escrita en Microsoft Visual C++ o C que usa la API del SDK de ODBC.  
  
-   Una aplicación escrita en Microsoft Visual Basic o Microsoft Visual Basic para aplicaciones.  
  
 En cada caso, la solicitud para obtener información utiliza la API de ODBC. El Administrador de controladores ODBC funciona con el controlador ODBC de Visual FoxPro para abrir y recuperar datos de las bases de datos y tablas de FoxPro.  
  
 La arquitectura se representa en el diagrama siguiente:  
  
 ![Muestra la arquitectura de controlador ODBC](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 Esta sección contiene los temas siguientes.  
  
-   [Terminología de Visual FoxPro](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [Instalar y configurar el controlador ODBC de Visual FoxPro](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Con el controlador ODBC de Visual FoxPro](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
