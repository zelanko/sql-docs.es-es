---
title: Protección de aplicaciones de RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS security [ADO]
ms.assetid: 82fb1330-d6c6-4c17-ad3e-d417ff822b25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 60f2d64fbb682cf3fcab866d1d76c7990f6b2341
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47798743"
---
# <a name="securing-rds-applications"></a>Protección de aplicaciones de RDS
Este tema proporciona información de seguridad para RDS.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="microsoft-internet-explorer-security-issues"></a>Problemas de seguridad de Microsoft Internet Explorer  
 Con las nuevas mejoras de seguridad agregadas a Microsoft Internet Explorer, algunos objetos ADO y RDS están restringidos para ejecutarse solo en un entorno en modo "seguro". Esto requiere que sean conscientes de estos problemas, incluidas distintas zonas, niveles de seguridad, comportamiento restrictivo, operaciones no seguras y personalizar la configuración de seguridad.  
  
## <a name="security-and-your-web-server"></a>Seguridad y el servidor Web  
 Si usas el [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objetos en el servidor Web de Internet, recuerde que el hacerlo crea un riesgo de seguridad. Los usuarios externos que obtener el nombre del origen de datos válido (DSN), Id. de usuario y la información de contraseña podrían escribir páginas para enviar cualquier consulta a ese origen de datos. Si desea un acceso más restringido a un origen de datos, es una opción anular el registro y eliminar la **RDSServer.DataFactory** objeto (msadcf.dll) y, en su lugar, use objetos de negocios personalizados con consultas codificado de forma rígida.  
  
 Para obtener más información sobre las implicaciones de seguridad de objeto RDSServer.DataFactory, vea el boletín de seguridad de Microsoft MS99-025 en el sitio Web de seguridad de Microsoft.  
  
## <a name="client-impersonation-and-security"></a>Seguridad y la suplantación de cliente  
 Si el **autenticación de contraseña** propiedad para el servidor Web de IIS está establecida como autenticación de desafío/respuesta de Windows NT (para Windows NT 4.0) o a la autenticación de Windows integrada (para Windows 2000) y, después, son objetos de negocios se invoca en el contexto de seguridad del cliente. Se trata de una nueva característica de RDS 1.5 que permite la suplantación del cliente a través de HTTP. Cuando se trabaja en este modo, el inicio de sesión al servidor Web (IIS) no es anónimo pero utiliza el Id. de usuario y la contraseña que se ejecuta el equipo cliente. Si los DSN de ODBC se configuran para usar una conexión de confianza, a continuación, el acceso a bases de datos, como SQL Server, también se produce en el contexto de seguridad del cliente. Pero esto solo funciona si la base de datos se encuentra en el mismo equipo que el IIS; las credenciales del cliente no se puede transferir a otro equipo.  
  
 Por ejemplo, un cliente, John Doe, con userid = "JesúsE" y la contraseña = "secreto" ha iniciado sesión en un equipo cliente. Ejecuta una aplicación basada en explorador que necesita para tener acceso a la **RDSServer.DataFactory** objeto para crear un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) mediante la ejecución de una consulta SQL en el equipo "MyServer" que ejecuta IIS. MiServidor, un sistema que ejecuta Windows NT Server 4.0, está configurado para utilizar la autenticación de desafío/respuesta de Windows NT, su DSN de ODBC tiene seleccionado "Utilizar conexión de confianza" y el servidor también contiene el origen de datos de SQL Server. Cuando se recibe una solicitud en el servidor Web, solicita al cliente para el Id. de usuario y la contraseña. Por lo tanto, la solicitud se registra en MiServidor como procedente de "JesúsE" / "Secreto" en lugar de IUSER_MyServer (que es el valor predeterminado cuando la autenticación anónima de contraseña está activado). De forma similar, al iniciar sesión en SQL Server, "JesúsE" / "Secreto" se utiliza.  
  
 Por lo tanto, el modo de autenticación de Windows NT desafío/respuesta de IIS permite que las páginas HTML se crea sin que el usuario explícitamente que se le pida la información de identificador y la contraseña de usuario necesaria para iniciar sesión en la base de datos. Si se usaban la autenticación básica de IIS, a continuación, esto también sería necesario.  
  
## <a name="password-authentication"></a>Autenticación de contraseña  
 RDS se puede comunicar con un servidor Web de IIS que se ejecuta en uno de los tres modos de autenticación de contraseña: anónimo, básico o autenticación de desafío/respuesta de NT (denominada autenticación de Windows integrada en Windows 2000). Esta configuración define cómo un servidor Web controla el acceso a través de él, como requerir que un equipo cliente tiene privilegios de acceso explícita en el servidor Web de NT.


