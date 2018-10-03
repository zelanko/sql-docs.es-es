---
title: Requisitos de hardware y Software (ODBC) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3f40621645aad2d1e52cb0a89baa8ff29b01446
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680663"
---
# <a name="hardware-and-software-requirements-odbc"></a>Requisitos de hardware y Software (ODBC)
En este tema se enumera los requisitos para usar los controladores de base de datos de escritorio de ODBC.  
  
## <a name="hardware-requirements"></a>Requisitos de hardware  
 Para usar los controladores de base de datos de escritorio de ODBC, debe tener:  
  
-   Un PC compatibles con IBM.  
  
-   Un disco duro con 6 MB de espacio libre en disco.  
  
-   Al menos 16 MB de memoria de acceso aleatorio (RAM).  
  
## <a name="software-requirements"></a>Requisitos de software  
 Para obtener acceso a datos con un controlador ODBC, debe tener:  
  
-   El controlador ODBC.  
  
-   El Administrador de controladores de ODBC de 32 bits, versión 3.51 o versiones posteriores (Odbc32.dll).  
  
-   Microsoft Windows 95 o versiones posteriores, o Windows NT 4.0 o Windows 2000.  
  
-   Un tamaño de pila de al menos 20 KB para una aplicación mediante el controlador ODBC de Microsoft.  
  
 Al utilizar Microsoft Windows NT 4.0 o Windows 2000, el controlador de 32 bits es segura para subprocesos, pero solo mediante el uso de un semáforo global que controla el acceso al controlador. Uso simultáneo del controlador es muy limitada en Windows NT. Todo el acceso a la capa de Jet ISAM será un subproceso único para todas las aplicaciones mediante el motor Microsoft Jet.  
  
 Cuando se ejecutan varias aplicaciones de 16 bits en Windows en Windows (WOW) en Microsoft Windows NT 4.0, se deben ejecutar las aplicaciones en espacios de memoria distintos. (El mismo espacio de memoria no se puede usar porque ODBC no es compatible con varios entornos en el mismo proceso.) Para ejecutar una aplicación en un espacio de memoria independiente, seleccione el icono de la aplicación en el Administrador de programas, abrir el **archivo** menú y haga clic en **propiedades**y, a continuación, haga clic en **ejecutar memoria independiente Espacio**.  
  
 No se admite el uso de estos controladores, las aplicaciones de 16 bits en Windows 95.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>Requisitos de Software y Hardware específicos del controlador  
  
-   El MicrosoftAccess y dBASEdrivers pueden requerir cambios en los archivos Autoexec.bat y Config.sys.
