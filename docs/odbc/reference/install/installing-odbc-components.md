---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5f033ac12569c7de61af071930d6c8d58d8b611
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47693425"
---
# <a name="installing-odbc-components"></a>Instalar componentes de ODBC
> [!NOTE]  
>  Desde Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. ODBC explícitamente sólo debe instalar en versiones anteriores de Windows.  
  
 En esta sección se describe cómo instalar y quitar componentes de ODBC. Dado que los desarrolladores de controladores siempre instalación un componente ODBC (su controlador), que necesitan leer esta sección. Los desarrolladores de aplicaciones deben leer esta sección solo si enviará a los componentes ODBC con sus aplicaciones. Componentes ODBC incluyen el Administrador de controladores, controladores, traductores, el archivo DLL de instalador, la biblioteca de cursores y los archivos relacionados. Para los fines de esta sección, las aplicaciones ODBC no se consideran como componentes ODBC.  
  
> [!NOTE]  
>  En esta sección es específica para las plataformas de Microsoft Windows. Cómo se instalan los componentes de ODBC en otras plataformas es específico de la plataforma.  
  
 Componentes de ODBC se instalan y se quitan según el componente a componente, no es una base por archivo. Por ejemplo, si un traductor consta del traductor de sí mismo y un número de archivos de datos, estos archivos están instalados y quitados como un grupo; deben no instalados y quitan según el archivo por archivo. La razón de esto es para asegurarse de que existen componentes sólo completados en el sistema.  
  
 Para fines de instalación y desinstalación de componentes, el siguiente se define los componentes ODBC:  
  
-   **Componentes principales.** El Administrador de controladores, biblioteca de cursores, instalador de DLL y cualquier otro relacionados con archivos constituyen los componentes principales y deben estar instalados y quitar como grupo.  
  
-   **Controladores.** Cada controlador es un componente independiente.  
  
-   **Traductores.** Cada translator es un componente independiente.  
  
 Con la compatibilidad de Unicode en ODBC 3.5 y versiones posteriores, debe proporcionarse cierta consideración al uso de componentes OLE DB con ODBC. La versión 1.1 del proveedor OLE DB para ODBC se escribió para las especificaciones de Unicode específicas dentro de ODBC 3.0. Dado que estas especificaciones cambian en ODBC 3.5, es necesario tener la versión 1.5 o posterior del proveedor cuando se usa ODBC 3.5 y versiones posteriores. Esta sección contiene los temas siguientes.  
  
-   [Componentes de instalación](../../../odbc/reference/install/installation-components.md)  
  
-   [Recuento de uso](../../../odbc/reference/install/usage-counting.md)
