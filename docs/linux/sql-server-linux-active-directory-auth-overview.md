---
title: Autenticación de Active Directory para SQL Server en Linux | Documentos de Microsoft
description: Este artículo proporciona información general sobre la autenticación de Active Directory para SQL Server en Linux.
author: rothja
ms.date: 02/23/2018
ms.author: jroth
manager: craigg
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 7f34cda192cbd909ac6c2392ab49acb58038b416
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>Autenticación de Active Directory para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artículo proporciona información general de autenticación de Active Directory (AD) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux. Autenticación de Active Directory también se denomina es la autenticación integrada en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 

## <a name="ad-authentication-overview"></a>Información general de autenticación de AD

Autenticación de Active Directory permite que los clientes Unidos a un dominio de Windows o Linux para autenticarse en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con sus credenciales de dominio y el protocolo Kerberos.

Autenticación de Active Directory tiene las siguientes ventajas sobre [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autenticación:

- Los usuarios se autentican a través de inicio de sesión único, sin que se solicite una contraseña.   
- Al crear los inicios de sesión para los grupos de AD, puede administrar el acceso y permisos en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con las pertenencias a grupos de AD.  
- Cada usuario tiene una identidad única en toda la organización, por lo que no es necesario realizar un seguimiento del que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] los inicios de sesión corresponden a las personas.   
- AD permite aplicar una directiva de contraseña centralizada a través de su organización.   

## <a name="configuration-steps"></a>Pasos de configuración

Para utilizar la autenticación de Active Directory, debe tener un controlador de dominio de Active Directory (Windows) en la red.

Se proporcionan los detalles acerca de cómo configurar la autenticación de AD en el tutorial, [Tutorial: autenticación de uso de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md). En la lista siguiente proporciona un resumen con un vínculo a cada sección del tutorial:

1. [Unirse a un host de SQL Server a un dominio de Active Directory](sql-server-linux-active-directory-authentication.md#join).
1. [Crear un usuario de AD para SQL Server y establecer ServicePrincipalName](sql-server-linux-active-directory-authentication.md#createuser).
1. [Configurar la tabla de claves del servicio de SQL Server](sql-server-linux-active-directory-authentication.md#configurekeytab).
1. [Crear inicios de sesión basados en AD SQL Server en Transact-SQL](sql-server-linux-active-directory-authentication.md#createsqllogins).
1. [Conectarse a SQL Server mediante autenticación de Active Directory](sql-server-linux-active-directory-authentication.md#connect).

## <a name="known-issues"></a>Problemas conocidos

- En este momento, el único método de autenticación admitido para el extremo de reflejo de la base de datos es certificado. Método de autenticación de WINDOWS se habilitarán en futuras versiones.
- Herramientas de AD de terceros como Centrify, Powerbroker, y no se admiten Vintela.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo implementar la autenticación de Active Directory para SQL Server en Linux, consulte [Tutorial: autenticación de uso de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md).