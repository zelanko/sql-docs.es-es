---
title: Propiedades de la publicación, Instantánea de FTP e Internet | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.internetsynchronization.f1
ms.assetid: 8e0198c3-5e4e-418c-9920-78ccbbfc1323
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9fcbf216468fd3d42b00daf41e4c9b7d7d97ea79
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48146775"
---
# <a name="publication-properties-ftp-snapshot-and-internet"></a>Propiedades de la publicación, Instantánea de FTP e Internet
  Esta página permite:  
  
-   Establecer propiedades para entregar la instantánea mediante FTP (Protocolo de transferencia de archivos). Para obtener más información, consulte [transferir instantáneas mediante FTP](transfer-snapshots-through-ftp.md) documentación de Windows para obtener más información.  
  
    > [!NOTE]  
    >  Si realiza algún cambio en la configuración del FTP deberá generar una nueva instantánea.  
  
-   Establecer propiedades de sincronización web para replicaciones de mezcla en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, lo que permite sincronizar las suscripciones mediante HTTPS (Protocolo de transferencia de hipertexto seguro). Para poder utilizar la sincronización web deberá configurar un servidor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS). Para más información, consulte [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md).  
  
## <a name="options"></a>Opciones  
 **Obtener acceso a archivos de instantánea a través de FTP**  
 Active **Permitir a los suscriptores descargar archivos de instantánea usando FTP (Protocolo de transferencia de archivos)** y especifique el **Nombre del servidor FTP**, el **Número de puerto**, la **Ruta de acceso de la carpeta raíz del servidor FTP**, el **Inicio de sesión**y la **Contraseña**para permitir a los suscriptores usar el FTP para entregar instantáneas.  
  
 Esta opción permite a los suscriptores usar el FTP para recuperar archivos de instantáneas, pero no les obliga a hacerlo. Si se selecciona esta opción, el Asistente para nueva suscripción establece de forma predeterminada que el suscriptor debe recuperar los archivos de instantáneas mediante el FTP. Puede cambiar esta configuración en el cuadro de diálogo **Propiedades de suscripción** . Si permite a los suscriptores tener acceso a los archivos de instantáneas mediante el FTP, debe especificar la carpeta FTP y la ubicación de los archivos de instantáneas en la página **Instantánea** del cuadro de diálogo **Propiedades de la publicación** . Al hacerlo de esta forma, el Agente de instantáneas actualiza automáticamente los archivos en la carpeta FTP cuando se genera una nueva instantánea. Si no establece la carpeta FTP como ubicación, deberá actualizar manualmente los archivos al generar nuevas instantáneas. Para obtener más información, vea [Entregar una instantánea mediante FTP](publish/deliver-a-snapshot-through-ftp.md).  
  
 **Sincronización web**  
 Solo replicación de mezcla. Active **Permitir a los suscriptores sincronizarse mediante la conexión a un servidor web**y especifique la dirección de un servidor web para permitir a los suscriptores de mezcla utilizar la sincronización web. El servidor web debe usar SSL (Capa de sockets seguros) y la dirección web debe ser completa (por ejemplo, https://server.domain.com/synchronize). Para más información, consulte [Configure Web Synchronization](configure-web-synchronization.md).  
  
## <a name="see-also"></a>Vea también  
 [Create a Publication](publish/create-a-publication.md)   
 [Ver y modificar propiedades de publicación](publish/view-and-modify-publication-properties.md)   
 [View and Modify Pull Subscription Properties](view-and-modify-pull-subscription-properties.md)  (Ver y modificar las propiedades de una suscripción de extracción)  
 [Ver y modificar las propiedades de una suscripción de inserción](view-and-modify-push-subscription-properties.md)   
 [Crear y aplicar la instantánea inicial](create-and-apply-the-initial-snapshot.md)   
 [Publicar datos y objetos de base de datos](publish/publish-data-and-database-objects.md)  
  
  
