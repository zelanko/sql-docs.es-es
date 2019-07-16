---
title: Introducción a la arquitectura de controlador | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 833c953df3502eb7e5d5676da8df057734174619
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071924"
---
# <a name="driver-architecture-overview"></a>Información general de la arquitectura de controlador
El controlador ODBC de Microsoft Visual FoxPro es un controlador de 32 bits que permite abrir y consultar una base de datos de Microsoft Visual FoxPro o las tablas de FoxPro a través de la interfaz de conectividad abierta de base de datos (ODBC). Puede tener acceso a datos de FoxPro mediante los siguientes tipos de aplicaciones:  
  
-   Una aplicación de Microsoft Office, como Microsoft Excel o Microsoft Word, Microsoft Query que utiliza para comunicarse con ODBC.  
  
-   Una aplicación escrita en Microsoft Visual C++ o C que usa la API del SDK de ODBC.  
  
-   Una aplicación escrita en Microsoft Visual Basic o Visual Basic para aplicaciones de Microsoft.  
  
 En cada caso, la solicitud de información usa la API de ODBC. El Administrador de controladores ODBC funciona con el controlador ODBC de Visual FoxPro para abrir y recuperar datos de las bases de datos y tablas.  
  
 La arquitectura se representa en el diagrama siguiente:  
  
 ![Muestra la arquitectura de controladores ODBC](../../odbc/microsoft/media/vfparch.gif "vfparch")  
  
 Esta sección contiene los temas siguientes.  
  
-   [Terminología de Visual FoxPro](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
-   [Instalar y configurar el controlador ODBC de Visual FoxPro](../../odbc/microsoft/installing-and-configuring.md)  
  
-   [Con el controlador ODBC de Visual FoxPro](../../odbc/microsoft/using-the-visual-foxpro-odbc-driver.md)
