---
title: Entradas del registro de componentes de ODBC | Documentos de Microsoft
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
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- installing ODBC components [ODBC], registry entries
- registry entries for components [ODBC]
- subkeys [ODBC], for components
- registry entries for components [ODBC], about registry entries
ms.assetid: c90aa8a4-6ece-48de-901c-17d23739a9ff
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f55b3fa2498cca66d36aff4f50b326ff1c9f6e17
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="registry-entries-for-odbc-components"></a>Entradas del registro de componentes de ODBC
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo de Windows. Solo explícitamente debe instalar ODBC en versiones anteriores de Windows.  
  
 El instalador DLL mantiene información en el registro de cada componente ODBC instalado. En equipos que ejecutan Microsoft Windows NT y Microsoft Windows 95 o Windows 98, esta información se almacena en las subclaves de la siguiente clave del registro:  
  
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
