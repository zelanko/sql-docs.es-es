---
title: Parches de software de Oracle (Oracle Software Patches) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292955"
---
# <a name="oracle-software-patches"></a>Revisiones de Software de Oracle
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Las revisiones para los productos de servidor de Oracle y su componente de cliente son necesarias para el correcto funcionamiento de varios productos y tecnologías de Microsoft, incluido el controlador ODBC de Microsoft para Oracle, el proveedor OLE DB de Microsoft para Oracle, Internet Information Services (IIS), Servicios de componentes (o Microsoft Transaction Server, si utiliza Windows NT), etc.  
  
> [!NOTE]  
>  Las siguientes instrucciones pueden no ser completamente precisas porque el sitio FTP de Oracle está sujeto a cambios.  
  
### <a name="to-download-the-oracle-software-patches"></a>Para descargar los parches de software de Oracle  
  
1.  Conéctese al sitio FTP público en oracle-ftp.oracle.com. El ID de usuario es "anónimo" y la contraseña es su dirección de correo electrónico.  
  
2.  Vaya al directorio siguiente: /server/wgt_tech/server/windowsNT.  
  
3.  Para descargar los parches más relevantes para Windows 95, Windows 98 y Windows NT/Windows 2000, vaya al subdirectorio de su versión de Oracle - 7.3 u 8.0. Los dos subdirectorios son /73patchsets y /80patchsets.  
  
4.  Para descargar parches para la tecnología de red de Oracle, ya sea SQL*Net o Net8, vaya al directorio siguiente: /network.  
  
 Es posible que el acceso a este sitio FTP desde el explorador web no funcione. Si experimenta problemas, intente utilizar un cliente FTP "tradicional" o utilice el símbolo del sistema de DOS.  
  
> [!NOTE]  
>  Dado que Oracle corrige errores en las versiones actuales y, a continuación, los adapta a versiones anteriores mediante parches de software, se recomienda descargar la última revisión disponible. Esto es especialmente cierto para los componentes de Oracle Server Client. Si tiene preguntas sobre la instalación de estos parches, póngase en contacto con el servicio de soporte técnico de Oracle.
