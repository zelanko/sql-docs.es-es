---
title: Entradas del registro para componentes ODBC | Microsoft Docs
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
ms.openlocfilehash: cbee5187a7318e0953ea61d92f7478d83e5afaff
ms.sourcegitcommit: 594cee116fa4ee321e1f5e5206f4a94d408f1576
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2019
ms.locfileid: "70009345"
---
# <a name="registry-entries-for-odbc-components"></a>Entradas del registro para los componentes de ODBC
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar explícitamente ODBC en versiones anteriores de Windows.  
  
 La DLL del instalador mantiene información en el registro acerca de cada componente ODBC instalado. En los equipos que ejecutan Microsoft Windows NT y Microsoft Windows 95/98, esta información se almacena en subclaves en la siguiente clave del registro:  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbcinst.ini
 ```

 Dado que Odbcinst. ini es una subclave del árbol HKEY_LOCAL_MACHINE, la información acerca de los componentes ODBC está disponible para todos los usuarios de la máquina.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Subclave de ODBC Core](../../../odbc/reference/install/odbc-core-subkey.md)  
  
-   [Subclave de controladores de ODBC](../../../odbc/reference/install/odbc-drivers-subkey.md)  
  
-   [Subclaves de la especificación del controlador](../../../odbc/reference/install/driver-specification-subkeys.md)  
  
-   [Subclave de controlador predeterminada](../../../odbc/reference/install/default-driver-subkey.md)  
  
-   [Subclave de traductores de ODBC](../../../odbc/reference/install/odbc-translators-subkey.md)  
  
-   [Subclaves de la especificación del traductor](../../../odbc/reference/install/translator-specification-subkeys.md)
