---
title: Elegir los servidores que configurar (Asistente para la configuración de seguridad de la creación de reflejo de bases de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.configdbmsecurwiz.choosesrvrs.f1
ms.assetid: 59e23ff3-d7ee-4e32-9629-0b54d3a258f7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 24e31e60f29970ca1d3a73d3a215447e9dd325bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62807249"
---
# <a name="choose-servers-to-configure-configure-database-mirroring-security-wizard"></a>Elegir los servidores que configurar (Asistente para la configuración de seguridad de la creación de reflejo de bases de datos)
  Utilice esta página para especificar las instancias de servidor que desea configurar ahora. Debe seleccionar al menos una instancia de servidor antes de continuar con el asistente.  
  
 Si desactiva la casilla para una instancia de servidor, el asistente no realizará ningún cambio en ella. Sin embargo, el asistente le solicitará información acerca de esa instancia y guardará esta información como parte de la configuración de las otras instancias de servidor. Por ejemplo, si desactiva la casilla de la instancia de servidor testigo, el asistente le solicitará la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del testigo, ya que debe crearse un inicio de sesión para esa cuenta como parte de la configuración de seguridad que se guarda en las instancias del servidor principal y reflejado.  
  
 **Para configurar la creación de reflejo de la base de datos mediante SQL Server Management Studio**  
  
-   [Establecer una sesión de creación de reflejo de la base de datos mediante la autenticación de Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [Iniciar el Asistente para la configuración de seguridad de la creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>Opciones  
 **Instancia de servidor principal**  
 Seleccione esta opción para configurar la seguridad del servidor principal.  
  
 **Instancia del servidor reflejado**  
 Seleccione esta opción para configurar la seguridad del servidor reflejado.  
  
 **Instancia de servidor testigo**  
 Seleccione para configurar la seguridad del servidor testigo (si está presente).  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de la base de datos &#40;página Creación de reflejo&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Creación de reflejo de la base de datos &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
