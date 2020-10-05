---
description: 'Error del servidor de Internet: Acceso denegado'
title: 'Error de servidor de Internet: acceso denegado | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- access denied error in RDS [ADO]
ms.assetid: e5b43cfa-da8d-430d-a2ab-5443dda47a16
author: rothja
ms.author: jroth
ms.openlocfilehash: 9cf9b2010fdbb20522c774d4c54ce2773cf817c5
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91721566"
---
# <a name="internet-server-error-access-denied"></a>Error del servidor de Internet: Acceso denegado
Si recibe este error, normalmente significa que Microsoft Internet Information Services (IIS) devolvió el siguiente estado:  
  
 HTTP_STATUS_DENIED 401  
  
 Asegúrese de que los directorios a los que tiene acceso IIS tienen los permisos adecuados. RDS puede comunicarse con un servidor Web de IIS que se ejecute en cualquiera de los tres modos de autenticación de contraseñas: desafío/respuesta de NT anónimo, básico o NT (denominado autenticación integrada de Windows en Windows 2000). Además, el servidor Web debe tener permisos para el equipo de origen de datos si se trata de un equipo con Windows NT/Windows 2000.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, los componentes de servidor RDS ya no se incluyen en el sistema operativo Windows (consulte la guía de compatibilidad de Windows 8 y [Windows server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Los componentes de cliente RDS se quitarán en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar al [servicio de datos de WCF](/dotnet/framework/wcf/).  
  
## <a name="see-also"></a>Consulte también  
 [Aspectos básicos de RDS](./rds-fundamentals.md)