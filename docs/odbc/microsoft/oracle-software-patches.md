---
title: Revisiones de software de Oracle | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1fb577e7b08f6ef332ed35f6d275a5f7ce543ba
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292955"
---
# <a name="oracle-software-patches"></a>Revisiones de Software de Oracle
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Las revisiones para los productos de servidor de Oracle y su componente de cliente son necesarias para el correcto funcionamiento de varios productos y tecnologías de Microsoft, incluidos Microsoft ODBC driver for Oracle, el Proveedor OLE DB de Microsoft para Oracle, Internet Information Services (IIS), servicios de componentes (o Microsoft Transaction Server, si usa Windows NT), etc.  
  
> [!NOTE]  
>  Las instrucciones siguientes pueden no ser completamente precisas porque el sitio FTP de Oracle está sujeto a cambios.  
  
### <a name="to-download-the-oracle-software-patches"></a>Para descargar las revisiones de software de Oracle  
  
1.  Conéctese al sitio FTP público en oracle-ftp.oracle.com. El ID. de usuario es "Anonymous" y la contraseña es su dirección de correo electrónico.  
  
2.  Navegue hasta el siguiente directorio:/Server/wgt_tech/server/windowsNT.  
  
3.  Para descargar revisiones más importantes para Windows 95, Windows 98 y Windows NT/Windows 2000, navegue hasta el subdirectorio de su versión de Oracle-7,3 o 8,0. Los dos subdirectorios son/73patchsets y/80patchsets.  
  
4.  Para descargar revisiones para la tecnología de red de Oracle, SQL * Net o Net8, navegue hasta el siguiente directorio:/Network.  
  
 Es posible que no funcione el acceso a este sitio FTP desde el explorador Web. Si tiene problemas, intente usar un cliente FTP "tradicional" o use el símbolo del sistema de DOS.  
  
> [!NOTE]  
>  Dado que Oracle corrige errores en las versiones actuales y luego los recoloca en versiones anteriores con las revisiones de software, se recomienda que descargue la revisión más reciente disponible. Esto es especialmente cierto para los componentes de cliente de servidor de Oracle. Si tiene alguna pregunta sobre la instalación de estas revisiones, póngase en contacto con el soporte técnico de Oracle.
