---
description: Instalar componentes de ODBC
title: Instalando componentes ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0250cc51b76cbda9c1091ebe1d696c2e569c037f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499751"
---
# <a name="installing-odbc-components"></a>Instalar componentes de ODBC
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar explícitamente ODBC en versiones anteriores de Windows.  
  
 En esta sección se describe cómo se instalan y se quitan los componentes ODBC. Dado que los desarrolladores de controladores siempre instalan un componente ODBC (su controlador), necesitan leer esta sección. Los desarrolladores de aplicaciones deben leer esta sección solo si van a enviar componentes ODBC con sus aplicaciones. Los componentes ODBC incluyen el administrador de controladores, los controladores, los traductores, la DLL del instalador, la biblioteca de cursores y los archivos relacionados. Para los fines de esta sección, las aplicaciones ODBC no se consideran componentes ODBC.  
  
> [!NOTE]  
>  Esta sección es específica de las plataformas de Microsoft Windows. La forma en que se instalan los componentes ODBC en otras plataformas es específica de la plataforma.  
  
 Los componentes ODBC se instalan y se quitan componente por componente, no por archivo. Por ejemplo, si un traductor está formado por el propio traductor y varios archivos de datos, estos archivos se instalan y se quitan como un grupo. no deben instalarse y quitarse de forma individual para cada archivo. El motivo es asegurarse de que solo existen componentes completos en el sistema.  
  
 A efectos de la instalación y la eliminación de componentes, se define lo siguiente como componentes ODBC:  
  
-   **Componentes principales.** El administrador de controladores, la biblioteca de cursores, el instalador DLL y cualquier otro archivo relacionado componen los componentes principales y deben instalarse y quitarse como un grupo.  
  
-   **Dispositivos.** Cada controlador es un componente independiente.  
  
-   **Traductores.** Cada traductor es un componente independiente.  
  
 Con la compatibilidad con Unicode en ODBC 3,5 y versiones posteriores, se debe tener en cuenta el uso de componentes de OLE DB con ODBC. La versión 1,1 del proveedor de OLE DB para ODBC se escribió en especificaciones Unicode específicas en ODBC 3,0. Dado que estas especificaciones han cambiado en ODBC 3,5, es necesario tener la versión 1,5 o posterior del proveedor al usar ODBC 3,5 y versiones posteriores. Esta sección contiene los temas siguientes.  
  
-   [Componentes de instalación](../../../odbc/reference/install/installation-components.md)  
  
-   [Recuento de uso](../../../odbc/reference/install/usage-counting.md)
