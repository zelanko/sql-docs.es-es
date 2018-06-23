---
title: Conexión al servidor (Oracle), Inicio de sesión | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rep.oracleconnection.login.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 86ed91a1-a07c-46f2-a913-67317ef2255e
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e5170f517b3ae8e16103e8b0fa6ccbea5505c078
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196429"
---
# <a name="connect-to-server-oracle-login"></a>Conectar al servidor (Oracle), Inicio de sesión
  Use la pestaña **Inicio de sesión** del cuadro de diálogo **Conectar al servidor** para especificar la cuenta desde la que se realizarán las conexiones del distribuidor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el publicador de Oracle. Se debe usar la misma cuenta que se especificó para el esquema de usuario administrativo de replicación al configurar el publicador. Para obtener más información, vea [Configurar un publicador de Oracle](non-sql/configure-an-oracle-publisher.md).  
  
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
 [Glossary of Terms for Oracle Publishing](non-sql/glossary-of-terms-for-oracle-publishing.md)  
  
  