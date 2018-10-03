---
title: Revisiones de Software de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], Oraclesoftware patches
- Oracle software patches [ODBC]
ms.assetid: 1275157b-f4e1-4c24-b273-c02555e261c2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afd5a20d99692c1a623b13b53218f62c00cb218a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845923"
---
# <a name="oracle-software-patches"></a>Revisiones de Software de Oracle
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 Las revisiones para los productos de servidor de Oracle y su componente de cliente son necesarias para que funcione correctamente en varios productos y tecnologías Microsoft, incluido el controlador ODBC de Microsoft para Oracle, el proveedor Microsoft OLE DB para Oracle, Internet Information Services (IIS), servicios de componentes (o Microsoft Transaction Server, si está utilizando Windows NT), y así sucesivamente.  
  
> [!NOTE]  
>  Las siguientes instrucciones no es posible que sea completamente exacta, porque el sitio FTP de Oracle está sujeta a cambios.  
  
### <a name="to-download-the-oracle-software-patches"></a>Para descargar las revisiones de software de Oracle  
  
1.  Conectarse al sitio FTP público en oracle ftp.oracle.com. El identificador de usuario es "anónimo" y la contraseña es la dirección de correo electrónico.  
  
2.  Navegue hasta el siguiente directorio: /server/wgt_tech/server/windowsNT.  
  
3.  Para descargar las revisiones más relevantes para Windows 95, Windows 98 y Windows NT o Windows 2000, desplácese hasta el subdirectorio de la versión de Oracle: 7.3 u 8.0. Los dos subdirectorios son /73patchsets y /80patchsets.  
  
4.  Para descargar las revisiones para la tecnología de red de Oracle, SQL * Net o Net8, navegue hasta el siguiente directorio: de red.  
  
 Obtener acceso a este sitio FTP desde el explorador Web no funcionen. Si tiene problemas, pruebe a usar a un cliente FTP "tradicional" o use el símbolo del sistema de denegación de servicio.  
  
> [!NOTE]  
>  Dado que Oracle corrige los errores en las versiones actuales y, a continuación, los retrofits a versiones anteriores con las revisiones de software, se recomienda que descargue la revisión más reciente disponible. Esto es especialmente cierto para los componentes de cliente del servidor de Oracle. Si tiene preguntas acerca de cómo instalar estas revisiones, póngase en contacto con soporte técnico de Oracle.
