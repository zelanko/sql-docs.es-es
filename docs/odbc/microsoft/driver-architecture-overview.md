---
title: Descripción general de la arquitectura del conductor ( Driver Architecture Overview ) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], architecture
- FoxPro ODBC driver [ODBC], architecture
ms.assetid: ef5a91cd-158e-40bf-b5a8-8ba535c4705e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd55290e09fbd35f5a1559ce4209693ef8eaaf73
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303466"
---
# <a name="driver-architecture-overview"></a>Información general de la arquitectura de controlador
El controlador ODBC de Microsoft Visual FoxPro es un controlador de 32 bits que le permite abrir y consultar una base de datos de Microsoft Visual FoxPro o tablas FoxPro a través de la interfaz Open Database Connectivity (ODBC). Puede acceder a los datos de FoxPro utilizando los siguientes tipos de aplicaciones:  
  
-   Una aplicación de Microsoft Office, como Microsoft Excel o Microsoft Word, que usa Microsoft Query para comunicarse con ODBC.  
  
-   Una aplicación escrita en Microsoft Visual C++ o C que usa la API del SDK de ODBC.  
  
-   Una aplicación escrita en Microsoft Visual Basic o Microsoft Visual Basic para aplicaciones.  
  
 En cada caso, la solicitud de información utiliza la API ODBC. El Administrador de controladores ODBC funciona con el controlador ODBC de Visual FoxPro para abrir y recuperar datos de tablas y bases de datos de FoxPro.  
  
 La arquitectura se representa en el siguiente diagrama:  
  
 ![Muestra la arquitectura de controladores ODBC](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 Esta sección contiene los temas siguientes.  
  
-   [Terminología de Visual FoxPro](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [Instalación y configuración del controlador ODBC de Visual FoxPro](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Con el controlador ODBC de Visual FoxPro](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
