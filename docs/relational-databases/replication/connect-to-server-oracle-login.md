---
description: Conectar al servidor (Oracle), Inicio de sesión
title: Conexión al servidor (Oracle), Inicio de sesión | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.oracleconnection.login.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 86ed91a1-a07c-46f2-a913-67317ef2255e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b585e2a17e577aab7ade2c5906bdcd184a12e8dd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455600"
---
# <a name="connect-to-server-oracle-login"></a>Conectar al servidor (Oracle), Inicio de sesión
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use la pestaña **Inicio de sesión** del cuadro de diálogo **Conectar al servidor** para especificar la cuenta desde la que se van a realizar las conexiones del distribuidor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el publicador de Oracle. Se debe usar la misma cuenta que se especificó para el esquema de usuario administrativo de replicación al configurar el publicador. Para obtener más información, vea [Configurar un publicador de Oracle](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="options"></a>Opciones  
 **Instancia del servidor**  
 Nombre TNS (Transparent Network Substrate, Sustrato de red transparente) del publicador de Oracle, que se especifica durante la configuración del software de cliente Oracle instalado en el distribuidor.  
  
 **Autenticación**  
 Seleccione **Autenticación estándar de Oracle** (opción recomendada) o **Autenticación de Windows**. Si selecciona **Autenticación de Windows**:  
  
-   El servidor de Oracle debe configurarse de forma que permita conexiones con las credenciales de Windows. Para obtener más información, vea la documentación de Oracle.  
  
-   Debe haber iniciado una sesión con la misma cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que especificó para el esquema de usuario administrativo de replicación.  
  
 **Inicio de sesión** y **Contraseña**  
 Si selecciona **Autenticación estándar de Oracle** para la opción **Autenticación** , especifique el nombre de inicio de sesión y la contraseña; deben coincidir con los especificados para el esquema de usuario administrativo de replicación.  
  
## <a name="see-also"></a>Vea también  
 [Glosario de términos de publicaciones de Oracle](../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)  
  
  
