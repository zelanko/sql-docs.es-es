---
title: Instalación de componentes ODBC ? Microsoft Docs
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
ms.openlocfilehash: bbd0a6aeba8073ce14b08b8635396b1f231895fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298985"
---
# <a name="installing-odbc-components"></a>Instalar componentes de ODBC
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar ODBC explícitamente en versiones anteriores de Windows.  
  
 En esta sección se describe cómo se instalan y quitan los componentes ODBC. Dado que los desarrolladores de controladores siempre instalan un componente ODBC (su controlador), deben leer esta sección. Los desarrolladores de aplicaciones deben leer esta sección solo si van a enviar componentes ODBC con sus aplicaciones. Los componentes ODBC incluyen el Administrador de controladores, controladores, traductores, el archivo DLL del instalador, la biblioteca de cursores y los archivos relacionados. Para los fines de esta sección, las aplicaciones ODBC no se consideran componentes ODBC.  
  
> [!NOTE]  
>  Esta sección es específica de las plataformas de Microsoft Windows. La forma en que se instalan los componentes ODBC en otras plataformas es específica de la plataforma.  
  
 Los componentes ODBC se instalan y quitan componente por componente, no archivo por archivo. Por ejemplo, si un traductor consta del propio traductor y de varios archivos de datos, estos archivos se instalan y eliminan como un grupo; no deben instalarse ni eliminarse archivo por archivo. La razón de esto es asegurarse de que sólo existen componentes completos en el sistema.  
  
 Para instalar y quitar componentes, se definen los siguientes componentes ODBC:  
  
-   **Componentes principales.** El Administrador de controladores, la biblioteca de cursores, el archivo DLL del instalador y cualquier otro archivo relacionado componen los componentes principales y deben instalarse y quitarse como un grupo.  
  
-   **Controladores.** Cada controlador es un componente independiente.  
  
-   **Traductores.** Cada traductor es un componente independiente.  
  
 Con la compatibilidad de Unicode en ODBC 3.5 y versiones posteriores, se debe tener en cuenta el uso de componentes OLE DB con ODBC. La versión 1.1 del proveedor OLE DB para ODBC se escribió según especificaciones Unicode específicas dentro de ODBC 3.0. Dado que estas especificaciones cambiaron en ODBC 3.5, es necesario tener la versión 1.5 o posterior del proveedor cuando se usa ODBC 3.5 y versiones posteriores. Esta sección contiene los temas siguientes.  
  
-   [Componentes de instalación](../../../odbc/reference/install/installation-components.md)  
  
-   [Recuento de uso](../../../odbc/reference/install/usage-counting.md)
