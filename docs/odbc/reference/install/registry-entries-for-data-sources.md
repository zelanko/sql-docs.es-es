---
title: Entradas del registro para orígenes de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC]
- data sources [ODBC], registry entries
- registry entries for data sources [ODBC], about registry entries
- data sources [ODBC], configuring
- registry entries for data sources [ODBC]
ms.assetid: 78aaa3d3-d081-4550-80e3-720c910d5996
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1fe76ba3926f2883e2518e255eddf0d567134f4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "70009353"
---
# <a name="registry-entries-for-data-sources"></a>Entradas del registro para los orígenes de datos
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar explícitamente ODBC en versiones anteriores de Windows.  
  
 La DLL del instalador mantiene información en el registro sobre cada origen de datos. En Microsoft Windows NT/Windows 2000 y Microsoft Windows 95/98, esta información se almacena en subclaves en una de las dos claves siguientes en el registro:  

 ```console
 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\Odbc.ini  
 ```

 ```console
 HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini
 ```

 La clave que se usa depende de si el origen de datos es un origen de datos *del sistema,* que está disponible para todos los usuarios o un *origen de datos de usuario,* que solo está disponible para el usuario actual. Los orígenes de datos del sistema se almacenan en el árbol de HKEY_LOCAL_MACHINE y los orígenes de datos de usuario se almacenan en el árbol de HKEY_CURRENT_USER. En todos los demás aspectos, los orígenes de datos del sistema y los orígenes de datos de usuario son idénticos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Subclave de orígenes de datos de ODBC](../../../odbc/reference/install/odbc-data-sources-subkey.md)  
  
-   [Subclaves de la especificación del origen de datos](../../../odbc/reference/install/data-source-specification-subkeys.md)  
  
-   [Subclave predeterminada](../../../odbc/reference/install/default-subkey.md)  
  
-   [Subclave ODBC](../../../odbc/reference/install/odbc-subkey.md)
