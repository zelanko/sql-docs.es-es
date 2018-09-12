---
title: Cuadro de diálogo Propiedades de conexión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connectionproperties.f1
helpviewer_keywords:
- Connection Properties dialog box
ms.assetid: 6df812ad-4d80-4503-8a23-47719ce85624
caps.latest.revision: 23
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a8c0f373d8327dd2b4a3f810264fa71925c5b533
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43810981"
---
# <a name="connection-properties-dialog-box"></a>Propiedades de conexión, cuadro de diálogo
  Utilice este cuadro de diálogo para ver las propiedades de la conexión actual. Este cuadro de diálogo está disponible cuando se hace clic en **Ver propiedades de conexión** en varios cuadros de diálogo del Explorador de objetos. Las propiedades que aparecen en esta página son de solo lectura.  
  
 Para cambiar propiedades tales como **Base de datos**, conéctese a la base de datos deseada con el Explorador de objetos antes de abrir el cuadro de diálogo **Propiedades de conexión** .  
  
 Observe que el tiempo de espera de consulta para SQL Azure es de 30 minutos.  
  
## <a name="authentication"></a>Autenticación  
 Vea las propiedades de autenticación de la conexión actual. Las propiedades de autenticación son el inicio de sesión y el método de autenticación cuando se establece la conexión. Para cambiar las propiedades de autenticación, desconéctese de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]y, a continuación, conecte de nuevo el Explorador de objetos al servidor, mediante las opciones de conexión deseadas.  
  
 **Método de autenticación**  
 El método de autenticación que utiliza la conexión actual.  
  
 **Nombre de usuario**  
 El nombre de usuario del inicio de sesión para la autenticación de la conexión.  
  
## <a name="connection-category"></a>Categoría de la conexión  
 Vea las propiedades de la conexión actual. La mayoría de las propiedades de conexión se seleccionaron en la pestaña **Propiedades de conexión** del cuadro de diálogo **Conectar al servidor** durante el proceso de conexión.  
  
 **Base de datos**  
 Nombre de la base de datos a la que está conectado. Para efectuar cambios, use la barra de herramientas del Editor SQL.  
  
 **SPID**  
 Id. de proceso del sistema que asigna el servidor a la conexión. No puede cambiarse para esta conexión.  
  
 **Protocolo de red**  
 Protocolo de red de la conexión [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] . Para cambiar esta opción, conéctese de nuevo con las propiedades de conexión deseadas.  
  
 **Tamaño de paquete de red**  
 Tamaño del paquete que se utiliza en la comunicación con el servidor. Para cambiar esta opción, conéctese de nuevo con las propiedades de conexión deseadas.  
  
 **Tiempo de espera de la conexión**  
 Intervalo de tiempo de espera (en segundos) al conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] antes de que se agote el tiempo y se devuelva un error de conexión al usuario. Para cambiar esta opción, conéctese de nuevo con las propiedades de conexión deseadas.  
  
 **Tiempo de espera de ejecución**  
 Intervalo de tiempo (en segundos) que hay que esperar antes de que finalice la ejecución de una tarea en el servidor. Para cambiar esta opción, conéctese de nuevo con las propiedades de conexión deseadas.  
  
 **Cifrado**  
 Indica si la conexión actual está cifrada. Para cambiar esta opción, conéctese de nuevo con las propiedades de conexión deseadas.  
  
## <a name="product-category"></a>Categoría del producto  
 Vea las propiedades del producto de la conexión actual. Estas propiedades describen el producto, la versión, el nombre de instancia y la intercalación del servidor. Las propiedades se configuran durante la instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Nombre del producto**  
 El nombre del producto [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Versión del producto**  
 Versión del producto [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Nombre de servidor**  
 Nombre del equipo que ejecuta [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Nombre de la instancia**  
 Nombre de instancia del servidor. Está en blanco de forma predeterminada.  
  
 **Lenguaje**  
 La versión de idioma del producto [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Intercalación**  
 La intercalación del servidor.  
  
## <a name="server-environment-category"></a>Categoría del entorno del servidor  
 Vea las propiedades del entorno del servidor de la conexión actual en relación con el hardware del servidor y el sistema operativo. No se pueden configurar las propiedades con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Nombre del equipo**  
 El nombre del equipo servidor que ejecuta [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Plataforma**  
 El nombre del sistema operativo, el nombre del fabricante y la familia de CPU del servidor.  
  
 **Sistema operativo**  
 La versión de [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows instalada en el servidor.  
  
 **Procesadores**  
 Número de procesadores del servidor.  
  
 **Memoria del sistema operativo**  
 La cantidad total de memoria física del servidor, en megabytes.  
  
## <a name="see-also"></a>Vea también  
 [Páginas de propiedades en SQL Server Management Studio](../ssms/property-pages-in-sql-server-management-studio.md)   
 [Conectar al servidor &#40;Página Inicio de sesión&#41; Motor de base de datos](../ssms/f1-help/connect-to-server-login-page-database-engine.md)  
  
  
