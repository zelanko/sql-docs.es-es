---
title: Requisitos de hardware y Software (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- hardware requirements [ODBC], desktop database drivers
- software requirements [ODBC], desktop database drivers
- system requirements [ODBC], desktop database drivers
- requirements [ODBC], desktop database drivers
ms.assetid: 6df2e9cd-de10-4629-97bd-32f2782616c7
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 164ad4c1ac1c93367291046c2e74986e7b6dc6c2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="hardware-and-software-requirements-odbc"></a>Requisitos de hardware y Software (ODBC)
Este tema enumeran los requisitos para el uso de los controladores de base de datos de escritorio ODBC.  
  
## <a name="hardware-requirements"></a>Requisitos de hardware  
 Para usar los controladores de base de datos de escritorio ODBC, debe tener:  
  
-   Un equipo compatible con IBM.  
  
-   Un disco duro con 6 MB de espacio libre en disco.  
  
-   Al menos 16 MB de memoria de acceso aleatorio (RAM).  
  
## <a name="software-requirements"></a>Requisitos de software  
 Para obtener acceso a datos con un controlador ODBC, debe tener:  
  
-   El controlador ODBC.  
  
-   El Administrador de controladores de ODBC de 32 bits, versión 3.51 o posterior (Odbc32.dll).  
  
-   Microsoft Windows 95 o posterior, o Windows NT 4.0 o Windows 2000.  
  
-   Un tamaño de pila de al menos 20 KB para una aplicación con un controlador ODBC de Microsoft.  
  
 Al utilizar Microsoft Windows NT 4.0 o Windows 2000, el controlador de 32 bits es segura para subprocesos, pero solo mediante el uso de un semáforo global que controla el acceso al controlador. Uso simultáneo del controlador es muy limitada en Windows NT. Todo el acceso a la capa de Jet ISAM será un subproceso único para todas las aplicaciones mediante el motor de Microsoft Jet.  
  
 Al ejecutar varias aplicaciones de 16 bits en Windows on Windows (WOW) en Microsoft Windows NT 4.0, se deben ejecutar las aplicaciones en espacios de memoria distintos. (No se puede usar el mismo espacio de memoria porque ODBC no admite varios entornos en el mismo proceso). Para ejecutar una aplicación en un espacio de memoria independiente, seleccione el icono de la aplicación en el Administrador de programas, abra el **archivo** menú y haga clic en **propiedades**y, a continuación, haga clic en **ejecutar en memoria independiente Espacio**.  
  
 No se admite el uso de estos controladores por las aplicaciones de 16 bits en Windows 95.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>Requisitos de Software y Hardware específicos del controlador  
  
-   El MicrosoftAccess y dBASEdrivers pueden requerir cambios en los archivos Autoexec.bat y Config.sys.
