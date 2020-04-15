---
title: Requisitos de hardware y software (ODBC) Microsoft Docs
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
ms.openlocfilehash: fe69775e379e9a9d661b4ddf81e577b738fcf34d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295245"
---
# <a name="hardware-and-software-requirements-odbc"></a>Requisitos de hardware y Software (ODBC)
En este tema se enumeran los requisitos para usar los controladores de base de datos de escritorio ODBC.  
  
## <a name="hardware-requirements"></a>Requisitos de hardware  
 Para utilizar los controladores de base de datos de escritorio ODBC, debe tener:  
  
-   Un ordenador personal compatible con IBM.  
  
-   Un disco duro con 6 MB de espacio libre en disco.  
  
-   Al menos 16 MB de memoria de acceso aleatorio (RAM).  
  
## <a name="software-requirements"></a>Requisitos de software  
 Para tener acceso a los datos con un controlador ODBC, debe tener:  
  
-   El controlador ODBC.  
  
-   El Administrador de controladores ODBC de 32 bits, versión 3.51 o posterior (Odbc32.dll).  
  
-   Microsoft Windows 95 o posterior, o Windows NT 4.0 o Windows 2000.  
  
-   Un tamaño de pila de al menos 20 KB para una aplicación que usa un controlador ODBC de Microsoft.  
  
 Cuando se usa Microsoft Windows NT 4.0 o Windows 2000, el controlador de 32 bits es seguro para subprocesos, pero solo mediante el uso de un semáforo global que controla el acceso al controlador. El uso simultáneo del controlador es muy limitado bajo Windows NT. Todo el acceso a la capa Jet ISAM será de un solo subproceso para todas las aplicaciones que utilicen el motor Microsoft Jet.  
  
 Al ejecutar varias aplicaciones de 16 bits en Windows en Windows (WOW) en Microsoft Windows NT 4.0, las aplicaciones deben ejecutarse en espacios de memoria independientes. (No se puede usar el mismo espacio de memoria porque ODBC no admite varios entornos en el mismo proceso.) Para ejecutar una aplicación en un espacio de memoria independiente, seleccione el icono de la aplicación en el Administrador de programas, abra el menú **Archivo** y haga clic en **Propiedades**y, a continuación, haga clic en Ejecutar en espacio de **memoria independiente**.  
  
 No se admite el uso de estos controladores por aplicaciones de 16 bits en Windows 95.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>Requisitos de hardware y software específicos del conductor  
  
-   Los controladores MicrosoftAccess y dBASEpueden pueden requerir cambios en los archivos Autoexec.bat o Config.sys.
