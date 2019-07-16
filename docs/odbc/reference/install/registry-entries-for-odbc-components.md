---
title: Entradas del registro de componentes de ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- installing ODBC components [ODBC], registry entries
- registry entries for components [ODBC]
- subkeys [ODBC], for components
- registry entries for components [ODBC], about registry entries
ms.assetid: c90aa8a4-6ece-48de-901c-17d23739a9ff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e7adeb2649575b96fbd8dc7101db93ab3332e06
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093869"
---
# <a name="registry-entries-for-odbc-components"></a>Entradas del registro para los componentes de ODBC
> [!NOTE]  
>  Desde Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. ODBC explícitamente sólo debe instalar en versiones anteriores de Windows.  
  
 El archivo DLL de instalador mantiene información en el registro de cada componente ODBC instalado. En los equipos que ejecutan Microsoft Windows NT y Microsoft Windows 95/98, esta información se almacena en las subclaves de la siguiente clave del registro:  
  
 HKEY_LOCAL_MACHINE  
  
 SOFTWARE  
  
 ODBC  
  
 Odbcinst.ini  
  
 Dado que Odbcinst.ini es una subclave del árbol HKEY_LOCAL_MACHINE, la información acerca de los componentes ODBC está disponible para todos los usuarios de la máquina.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Subclave de ODBC Core](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [Subclave de controladores de ODBC](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [Subclaves de la especificación del controlador](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [Subclave de controlador predeterminada](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [Subclave de traductores de ODBC](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [Subclaves de la especificación del traductor](../../../odbc/reference/install/translator-specification-subkeys.md)
