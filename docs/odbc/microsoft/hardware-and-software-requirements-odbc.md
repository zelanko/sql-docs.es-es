---
description: Requisitos de hardware y Software (ODBC)
title: Requisitos de hardware y software (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- hardware requirements [ODBC], desktop database drivers
- software requirements [ODBC], desktop database drivers
- system requirements [ODBC], desktop database drivers
- requirements [ODBC], desktop database drivers
ms.assetid: 6df2e9cd-de10-4629-97bd-32f2782616c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0f88c8877161122c11fb65bcdb62fd4e7b684c3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412491"
---
# <a name="hardware-and-software-requirements-odbc"></a>Requisitos de hardware y Software (ODBC)
En este tema se enumeran los requisitos para usar los controladores de base de datos de escritorio ODBC.  
  
## <a name="hardware-requirements"></a>Requisitos de hardware  
 Para usar los controladores de base de datos de escritorio ODBC, debe tener:  
  
-   Un equipo personal compatible con IBM.  
  
-   Un disco duro con 6 MB de espacio libre en disco.  
  
-   Al menos 16 MB de memoria de acceso aleatorio (RAM).  
  
## <a name="software-requirements"></a>Requisitos de software  
 Para tener acceso a los datos con un controlador ODBC, debe tener:  
  
-   El controlador ODBC.  
  
-   El administrador de controladores ODBC de 32 bits, versión 3,51 o posterior (Odbc32.dll).  
  
-   Microsoft Windows 95 o posterior, o Windows NT 4,0 o Windows 2000.  
  
-   Un tamaño de pila de al menos 20 KB para una aplicación que usa un controlador ODBC de Microsoft.  
  
 Cuando se usa Microsoft Windows NT 4,0 o Windows 2000, el controlador de 32 bits es seguro para subprocesos, pero solo mediante el uso de un semáforo global que controla el acceso al controlador. El uso simultáneo del controlador está muy limitado en Windows NT. Todo el acceso a la capa de ISAM de jet será de un solo subproceso para todas las aplicaciones que usen el motor de Microsoft Jet.  
  
 Al ejecutar varias aplicaciones de 16 bits en Windows en Windows (WOW) en Microsoft Windows NT 4,0, las aplicaciones se deben ejecutar en espacios de memoria independientes. (No se puede usar el mismo espacio de memoria porque ODBC no admite varios entornos en el mismo proceso). Para ejecutar una aplicación en un espacio de memoria independiente, seleccione el icono de la aplicación en el administrador de programas, abra el menú **archivo** , haga clic en **propiedades**y, a continuación, haga clic en **ejecutar en un espacio de memoria independiente**.  
  
 No se admite el uso de estos controladores por parte de aplicaciones de 16 bits en Windows 95.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>Requisitos de hardware y software específicos del controlador  
  
-   MicrosoftAccess y dBASEdrivers pueden requerir cambios en los archivos Autoexec.bat o Config.sys.
