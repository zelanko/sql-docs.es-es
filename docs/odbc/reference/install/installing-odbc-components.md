---
title: Instalar componentes de ODBC | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- installing ODBC components [ODBC]
- installing ODBC components [ODBC], about installing
- ODBC [ODBC], component installation
ms.assetid: b7e48e9c-8912-4003-b4ef-30aa44de06a7
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 383a3a17abb969a57eb2de68b304da4b1bde9a6b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="installing-odbc-components"></a>Instalar componentes de ODBC
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo de Windows. Solo explícitamente debe instalar ODBC en versiones anteriores de Windows.  
  
 Esta sección describe cómo instalar y quitar componentes de ODBC. Dado que los programadores de controladores siempre instalación un componente ODBC (su controlador), deben leer esta sección. Los desarrolladores de aplicaciones necesitan leer esta sección solo si se se incluyen componentes ODBC con sus aplicaciones. Componentes ODBC incluyen el Administrador de controladores, controladores, traductores, el archivo DLL del programa de instalación, la biblioteca de cursores y los archivos relacionados. Para los fines de esta sección, las aplicaciones ODBC no se consideran como componentes de ODBC.  
  
> [!NOTE]  
>  Esta sección es específica de plataformas de Microsoft Windows. Cómo se instalan los componentes de ODBC en otras plataformas es específica de la plataforma.  
  
 Componentes de ODBC se instalan y se quitan con un componente por componente, no en una base por cada archivo. Por ejemplo, si un traductor consta del traductor de sí mismo y un número de archivos de datos, estos archivos están instalados y eliminar, ya que un grupo; debe no se instala y se quita de forma por cada archivo. La razón para esto es para asegurarse de que existen componentes sólo completados en el sistema.  
  
 Para fines de instalación y eliminación de componentes, a continuación se define como componentes de ODBC:  
  
-   **Componentes principales.** El Administrador de controladores, biblioteca de cursores, installer DLL y cualquier otro relacionados con archivos constituyen los componentes principales y deben estar instalados y eliminar, ya que un grupo.  
  
-   **Controladores.** Cada controlador es un componente independiente.  
  
-   **Traductores.** Cada traductor es un componente independiente.  
  
 Con la compatibilidad de Unicode en ODBC 3.5 y versiones posteriores, algunos prestar al uso de componentes de OLE DB con ODBC. La versión 1.1 del proveedor OLE DB para ODBC escribió en las especificaciones de Unicode específicas dentro de ODBC 3.0. Dado que estas especificaciones cambian en ODBC 3.5, es necesario tener la versión 1.5 o posterior del proveedor cuando se utiliza ODBC 3.5 y versiones posteriores. Esta sección contiene los temas siguientes.  
  
-   [Componentes de instalación](../../../odbc/reference/install/installation-components.md)  
  
-   [Recuento de uso](../../../odbc/reference/install/usage-counting.md)
