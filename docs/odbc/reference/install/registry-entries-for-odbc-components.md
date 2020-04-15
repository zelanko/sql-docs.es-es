---
title: Entradas del Registro para Componentes ODBC ( Registry Entries for ODBC Components) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bead63f11b253342cd444e1d5bd0697ee00cfbc1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296185"
---
# <a name="registry-entries-for-odbc-components"></a>Entradas del registro para los componentes de ODBC
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar ODBC explícitamente en versiones anteriores de Windows.  
  
 El archivo DLL del instalador mantiene información en el registro sobre cada componente ODBC instalado. En equipos que ejecutan Microsoft Windows NT y Microsoft Windows 95/98, esta información se almacena en subclaves bajo la siguiente clave del Registro:  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbcinst.ini
 ```

 Dado que Odbcinst.ini es una subclave del árbol de HKEY_LOCAL_MACHINE, la información sobre los componentes ODBC está disponible para todos los usuarios del equipo.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Subclave de ODBC Core](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [Subclave de controladores de ODBC](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [Subclaves de la especificación del controlador](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [Subclave de controlador predeterminada](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [Subclave de traductores de ODBC](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [Subclaves de la especificación del traductor](../../../odbc/reference/install/translator-specification-subkeys.md)
