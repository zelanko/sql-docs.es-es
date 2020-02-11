---
title: Publicador de Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.selectoraclepublisher.f1
ms.assetid: 019b7c49-dcca-445d-8969-5982a8ccbc1a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b38b397c0a2128aed5ebaba0b1367ca14ebdcd09
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63022037"
---
# <a name="oracle-publisher"></a>Publicador de Oracle
  A partir [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , permite publicar datos de una base de datos de Oracle mediante la replicación de instantáneas y transaccional. Para obtener más información, vea [Oracle Publishing Overview](non-sql/oracle-publishing-overview.md) (Información general de la publicación de Oracle).  
  
 El publicador de Oracle debe utilizar un distribuidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remoto. Este asistente se debe ejecutar en ese servidor después de que se haya instalado y probado el software de red de Oracle necesario. Para más información, vea [Configurar un publicador de Oracle](non-sql/configure-an-oracle-publisher.md).  
  
> [!IMPORTANT]  
>  Si otro administrador configuró la base de datos de Oracle como publicador, después de hacer clic en **Siguiente** , se le solicitará que escriba la contraseña del inicio de sesión de replicación que se utiliza para conectarse a la base de datos de Oracle. A continuación,[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creará una asignación entre su inicio de sesión y la conexión del servidor vinculado a la base de datos de Oracle. No no será necesario que escriba una contraseña cada vez que vuelva a conectarse a la base de datos de Oracle.  
  
## <a name="options"></a>Opciones  
 **Publicadores de Oracle**  
 Seleccione un publicador de Oracle de la lista. Esta lista contiene los publicadores de Oracle que se configuraron previamente para utilizar el servidor en el que se está ejecutando el asistente como su distribuidor. Si la lista está vacía o si el publicador de Oracle que desea utilizar no figura en la lista, haga clic en **Agregar publicador de Oracle**.  
  
 **Agregar publicador de Oracle**  
 Haga clic en esta opción para abrir el cuadro de diálogo **Propiedades del distribuidor** . En este cuadro de diálogo, haga clic en **Agregar**y, a continuación, en **Agregar publicador de Oracle**. En el cuadro de diálogo **Conectar al servidor** , especifique el nombre del servidor de Oracle y el inicio de sesión y la contraseña correspondientes al esquema de usuario administrativo de replicación. Para obtener más información, vea [Conectar al servidor &#40;motor de base de datos&#41;](connect-to-server-oracle-login.md).  
  
> [!NOTE]  
>  Si el servidor en el que se ejecuta el asistente aún no ha sido configurado como distribuidor, se le solicitará que lo configure ahora.  
  
## <a name="see-also"></a>Consulte también  
 [Crear una publicación a partir de una Oracle Database](publish/create-a-publication-from-an-oracle-database.md)   

  
  
